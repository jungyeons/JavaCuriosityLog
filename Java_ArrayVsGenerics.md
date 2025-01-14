


**질문:** Integer[] 랑 list<Integer>가 뭐가 달라 ?  
**답변:**

`Integer[]`와 `List<Integer>`는 둘 다 Java에서 사용되는 데이터 구조이지만, 몇 가지 중요한 차이점이 있습니다.

---

## 1. 자료형 및 선언 방식
- `Integer[]`: Java의 **배열(array)**입니다. 고정된 크기를 가지며, Java의 기본 자료구조입니다.
  ```java
  Integer[] array = new Integer[5];
  array[0] = 10;
  ```
- `List<Integer>`: Java의 **컬렉션 프레임워크(collection framework)**의 일부분인 **리스트(list)**입니다. 크기가 가변적이며 더 많은 유틸리티 메서드를 제공합니다.
  ```java
  List<Integer> list = new ArrayList<>();
  list.add(10);
  ```

---

## 2. 크기
- **배열 (Integer[])**
  - 크기가 **고정**되어 있습니다. 한 번 생성하면 크기를 변경할 수 없습니다.
  - 배열 생성 시 초기 크기를 반드시 지정해야 합니다.
  ```java
  Integer[] array = new Integer[5]; // 크기 5로 고정
  ```
- **리스트 (List<Integer>)**
  - 크기가 **가변적**입니다. 요소를 추가하거나 제거할 수 있습니다.
  ```java
  List<Integer> list = new ArrayList<>();
  list.add(10);  // 요소 추가
  list.remove(0); // 요소 제거
  ```

---

## 3. 유틸리티 메서드
- **배열 (Integer[])**
  - 유틸리티 메서드가 거의 없습니다. 기본적으로 `Arrays` 클래스의 정적 메서드를 사용해야 합니다.
  ```java
  Arrays.sort(array); // 배열 정렬
  ```
- **리스트 (List<Integer>)**
  - 요소 추가, 삭제, 탐색 등 다양한 유틸리티 메서드를 제공합니다.
  ```java
  list.add(20);    // 요소 추가
  list.remove(0);  // 특정 인덱스 요소 제거
  list.contains(20); // 특정 요소 포함 여부 확인
  ```

---

## 4. 성능
- **배열 (Integer[])**
  - 더 **빠른** 성능을 제공합니다. 메모리 사용량이 적고, 직접적으로 배열에 접근하기 때문에 속도가 빠릅니다.
  - 하지만 크기가 고정되어 있어 유연성이 부족합니다.
- **리스트 (List<Integer>)**
  - 내부적으로 동적 배열을 사용하기 때문에 메모리와 성능 면에서 약간의 오버헤드가 발생할 수 있습니다.
  - 그러나 가변 크기와 다양한 메서드를 제공해 **유연성**이 더 높습니다.

---

## 5. 사용 사례
- **배열 (Integer[])**
  - 고정된 크기의 데이터를 저장해야 할 때 사용됩니다.
  - 예: 다차원 배열, 간단한 데이터 처리.
- **리스트 (List<Integer>)**
  - 동적인 데이터 처리 및 복잡한 컬렉션 작업에 적합합니다.
  - 예: 데이터 추가/삭제가 빈번한 경우.

---

## 6. 코드 비교

```java
// 배열
Integer[] array = new Integer[3];
array[0] = 1;
array[1] = 2;
array[2] = 3;
// 배열은 고정 크기이며 요소 추가는 불가능합니다.

// 리스트
List<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
list.add(3);
list.add(4); // 크기 제한 없이 요소를 추가할 수 있습니다.
```

---

## 요약
- `Integer[]`는 **고정 크기**의 배열.
- `List<Integer>`는 **가변 크기**의 동적 리스트로 더 많은 기능 제공.
