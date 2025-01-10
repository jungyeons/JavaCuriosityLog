### Q: Java Stream의 중간 연산(Intermediate Operations)이란 무엇인가요?

**A:** 중간 연산은 스트림을 변환하거나 필터링하는 데 사용됩니다. 지연(lazy) 실행되며, 최종 연산이 호출될 때까지 실제로 실행되지 않습니다. 이러한 연산은 복잡한 스트림 파이프라인을 체인 방식으로 구축할 수 있도록 합니다.

---

### Q: 중간 연산의 주요 특징은 무엇인가요?

**A:**
1. **지연 실행:** 최종 연산이 호출될 때까지 스트림을 처리하지 않습니다.
2. **스트림 반환:** 각 중간 연산은 새로운 스트림을 반환합니다.
3. **무상태 또는 유상태:**
   - 무상태(Stateless): 각 요소를 독립적으로 처리합니다(예: `filter`, `map`).
   - 유상태(Stateful): 다른 요소에 대한 정보를 필요로 합니다(예: `sorted`, `distinct`).

---

### Q: 일반적인 중간 연산은 무엇인가요?

**A:**

| 메서드          | 설명                                           | 예제                                 |
|-----------------|-----------------------------------------------|-------------------------------------|
| `filter`        | 조건에 따라 요소를 필터링                     | `stream.filter(x -> x > 10)`       |
| `map`           | 각 요소를 변환                                | `stream.map(x -> x * 2)`           |
| `flatMap`       | 중첩된 구조를 평면화                          | `stream.flatMap(Collection::stream)` |
| `distinct`      | 중복된 요소를 제거                            | `stream.distinct()`                |
| `sorted`        | 요소를 정렬                                   | `stream.sorted()`                  |
| `limit`         | 스트림 크기를 제한                            | `stream.limit(5)`                  |
| `skip`          | 지정된 수의 요소를 건너뜀                     | `stream.skip(2)`                   |
| `peek`          | 각 요소에 대해 동작 수행(디버깅용)             | `stream.peek(System.out::println)` |

---

### Q: 중간 연산의 예제를 보여주시겠어요?

**A:**
```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class IntermediateExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        List<Integer> result = numbers.stream()
                .filter(x -> x % 2 == 0)   // 짝수 필터링
                .map(x -> x * 2)          // 각 숫자를 2배로 변환
                .limit(5)                 // 최대 5개 요소 제한
                .collect(Collectors.toList());

        System.out.println(result); // 출력: [4, 8, 12, 16, 20]
    }
}
```

---

### Q: Java Stream의 최종 연산(Terminal Operations)이란 무엇인가요?

**A:** 최종 연산은 스트림을 처리하여 결과를 생성하거나 동작을 수행합니다. 스트림을 **소모**하므로, 이후에 스트림을 사용할 수 없습니다.

---

### Q: 최종 연산의 주요 특징은 무엇인가요?

**A:**
1. **즉시 실행:** 즉각적으로 실행됩니다.
2. **스트림 소모:** 실행 후 스트림은 더 이상 사용할 수 없습니다.
3. **결과 생성:** 결과를 반환하거나 부수 효과를 수행합니다.

---

### Q: 일반적인 최종 연산은 무엇인가요?

**A:**

| 메서드            | 설명                                           | 예제                                   |
|------------------|-----------------------------------------------|---------------------------------------|
| `forEach`        | 각 요소에 대해 동작 수행                      | `stream.forEach(System.out::println)` |
| `collect`        | 요소를 컬렉션이나 구조로 수집                  | `stream.collect(Collectors.toList())` |
| `toArray`        | 요소를 배열로 변환                            | `stream.toArray()`                    |
| `reduce`         | 요소를 단일 결과로 축소                        | `stream.reduce(0, Integer::sum)`      |
| `count`          | 요소 개수를 계산                              | `stream.count()`                      |
| `findFirst`      | 첫 번째 요소 반환(Optional)                   | `stream.findFirst()`                  |
| `findAny`        | 임의의 요소 반환(Optional)                    | `stream.findAny()`                    |
| `anyMatch`       | 조건에 맞는 요소가 하나라도 있는지 확인         | `stream.anyMatch(x -> x > 5)`         |
| `allMatch`       | 모든 요소가 조건에 맞는지 확인                 | `stream.allMatch(x -> x > 0)`         |
| `noneMatch`      | 조건에 맞는 요소가 없는지 확인                 | `stream.noneMatch(x -> x < 0)`        |
| `max` / `min`    | 최대값 또는 최소값 반환                        | `stream.max(Comparator.naturalOrder())` |

---

### Q: 최종 연산의 예제를 보여주시겠어요?

**A:**
```java
import java.util.Arrays;
import java.util.List;
import java.util.Optional;

public class TerminalExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // 1. forEach: 모든 요소 출력
        numbers.stream().forEach(System.out::println);

        // 2. count: 짝수 개수 계산
        long evenCount = numbers.stream()
                .filter(x -> x % 2 == 0)
                .count();
        System.out.println("짝수 개수: " + evenCount);

        // 3. reduce: 모든 요소의 합 계산
        int sum = numbers.stream()
                .reduce(0, Integer::sum);
        System.out.println("합계: " + sum);

        // 4. findFirst: 첫 번째 짝수 찾기
        Optional<Integer> firstEven = numbers.stream()
                .filter(x -> x % 2 == 0)
                .findFirst();
        System.out.println("첫 번째 짝수: " + firstEven.orElse(-1));
    }
}
```

---

### Q: 중간 연산과 최종 연산은 어떻게 함께 동작하나요?

**A:** 중간 연산은 변환 파이프라인을 구축하고, 최종 연산은 이 파이프라인의 실행을 트리거합니다. 아래는 예제입니다:

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");

        List<String> result = names.stream()
                .filter(name -> name.startsWith("A")) // 중간 연산: 'A'로 시작하는 이름 필터링
                .map(String::toUpperCase)             // 중간 연산: 대문자로 변환
                .sorted()                             // 중간 연산: 이름 정렬
                .collect(Collectors.toList());        // 최종 연산: 결과 수집

        System.out.println(result); // 출력: [ALICE]
    }
}
```

---

### Q: 중간 연산과 최종 연산의 주요 차이점 요약해주세요 

| 특징                 | 중간 연산                        | 최종 연산                        |
|---------------------|--------------------------------|--------------------------------|
| **실행 시점**        | 지연 실행 (필요 시 실행)          | 즉시 실행                       |
| **반환값**           | 스트림                           | 결과 또는 부수 효과              |
| **체이닝 가능 여부**   | 가능                             | 불가능                           |
| **스트림 재사용 여부** | 스트림 유지                      | 스트림 소모                     |

---

