# Java에서 `enum`과 `Enumeration`의 차이가 뭐야?

Java에서 `enum`과 "이니머레이션(enumeration)"이라는 용어는 비슷하게 들리지만, 서로 다른 개념을 나타냅니다. 주요 차이를 정리하면 다음과 같습니다:

---

## 1. **`enum` (열거형)**
- Java 5부터 도입된 키워드로, 고정된 상수 집합을 정의하는 데 사용됩니다.
- **목적:** 특정 값 집합을 표현하고, 타입 안정성을 제공.
- **구현:** 클래스처럼 동작하며, 메서드와 필드를 가질 수 있습니다.
- **주요 특징:**
  - 상수 값은 객체로 표현됩니다.
  - switch문에서 쉽게 사용할 수 있습니다.
  - 각 값은 고유한 인스턴스입니다.
  - 추가적인 메서드와 생성자를 정의할 수 있습니다.

```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

public class Main {
    public static void main(String[] args) {
        Day today = Day.WEDNESDAY;
        System.out.println(today); // WEDNESDAY
    }
}
```

---

## 2. **Enumeration (인터페이스)**
- Java 1.0부터 존재하는 인터페이스로, `java.util` 패키지에 포함되어 있습니다.
- **목적:** 컬렉션에서 요소를 순회(iterate)하기 위한 메커니즘 제공.
- **구현:** `Enumeration` 인터페이스를 구현한 객체를 사용.
- **주요 특징:**
  - 컬렉션 요소를 읽기 전용으로 순회할 때 사용.
  - `Iterator`와 비슷하지만 더 오래된 방식.
  - 메서드:
    - `boolean hasMoreElements()`: 다음 요소가 있으면 `true` 반환.
    - `Object nextElement()`: 다음 요소를 반환.

```java
import java.util.Enumeration;
import java.util.Vector;

public class Main {
    public static void main(String[] args) {
        Vector<String> vector = new Vector<>();
        vector.add("Apple");
        vector.add("Banana");
        vector.add("Cherry");

        Enumeration<String> enumeration = vector.elements();

        while (enumeration.hasMoreElements()) {
            System.out.println(enumeration.nextElement());
        }
    }
}
```

---

## **주요 차이점 요약**

| **특징**           | **`enum`**                                | **Enumeration**                            |
|--------------------|------------------------------------------|-------------------------------------------|
| **역할**           | 열거형 상수 정의                          | 컬렉션 요소 순회                           |
| **사용 시점**       | 상수 집합 표현이 필요할 때                  | 컬렉션을 순회할 때                         |
| **타입**           | 키워드 (데이터 타입 정의)                  | 인터페이스                                 |
| **주요 메서드**     | 사용자 정의 가능                           | `hasMoreElements()`, `nextElement()`       |
| **등장 시기**       | Java 5                                    | Java 1.0                                   |
| **대안**           | 상수 집합 표현의 현대적 방식 (`enum`)        | `Iterator`가 현대적 대안                   |

---

결론적으로, `enum`은 상수 집합을 정의하고, `Enumeration`은 컬렉션을 순회하는 데 사용됩니다. 두 개념은 용도와 사용 방법이 완전히 다르므로 문맥에 따라 적합한 것을 사용하면 됩니다.
