# 자바의 참조형 매개변수와 기본형 매개변수 Q&A

## Q1. 기본형 매개변수란 무엇인가요?

**A:** 기본형 매개변수는 값 자체를 복사하여 전달하는 방식입니다. 메서드 내부에서 매개변수의 값을 변경해도 원래 값에는 영향을 미치지 않습니다.

### 예시
```java
public class Main {
    public static void main(String[] args) {
        int number = 10;
        modifyValue(number);
        System.out.println("number: " + number); // 출력: number: 10
    }

    public static void modifyValue(int value) {
        value = 20; // 값 변경
    }
}
```

### 설명
- `modifyValue` 메서드에서 `value`를 변경해도 `main` 메서드의 `number`에는 영향을 미치지 않습니다.
- 이는 `number`의 복사본이 메서드에 전달되었기 때문입니다.

---

## Q2. 참조형 매개변수란 무엇인가요?

**A:** 참조형 매개변수는 객체의 참조(주소)를 전달하는 방식입니다. 메서드 내부에서 객체의 속성을 변경하면 원래 객체에 영향을 미칩니다.

### 예시
```java
public class Main {
    public static void main(String[] args) {
        int[] numbers = {10, 20, 30};
        modifyArray(numbers);
        System.out.println("numbers[0]: " + numbers[0]); // 출력: numbers[0]: 100
    }

    public static void modifyArray(int[] array) {
        array[0] = 100; // 배열의 첫 번째 값을 변경
    }
}
```

### 설명
- `modifyArray` 메서드에서 배열의 값을 변경하면, `main` 메서드에서도 변경된 값이 반영됩니다.
- 이는 배열의 참조가 전달되었기 때문입니다.

---

## Q3. 기본형 매개변수와 참조형 매개변수의 차이는 무엇인가요?

**A:**
| 특징               | 기본형 매개변수                            | 참조형 매개변수                          |
|--------------------|------------------------------------------|------------------------------------------|
| 데이터 전달 방식    | 값 자체를 복사하여 전달                     | 객체의 참조(주소)를 복사하여 전달            |
| 메서드 내부 변경 여부 | 원래 값에는 영향을 미치지 않음               | 원래 객체에 영향을 미침                     |
| 사용 예            | `int`, `double`, `char`, `boolean` 등       | 배열, 클래스 객체, `String` 등              |

---

## Q4. 참조형 매개변수로 객체 자체를 변경할 수 있나요?

**A:** 참조형 매개변수를 통해 객체의 속성을 변경할 수는 있지만, 객체 자체를 새로운 인스턴스로 변경하면 원래 객체에는 영향을 미치지 않습니다.

### 예시
```java
public class Main {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");
        modifyObject(sb);
        System.out.println("sb: " + sb); // 출력: sb: Hello, World!

        resetObject(sb);
        System.out.println("sb: " + sb); // 출력: sb: Hello, World!
    }

    public static void modifyObject(StringBuilder builder) {
        builder.append(", World!"); // 객체 속성 변경
    }

    public static void resetObject(StringBuilder builder) {
        builder = new StringBuilder("Reset"); // 새로운 객체 할당
    }
}
```

### 설명
- `modifyObject` 메서드는 `StringBuilder` 객체의 내용을 변경하므로, 원래 객체가 변경됩니다.
- `resetObject` 메서드는 새로운 객체를 할당하지만, 원래 객체에는 영향을 미치지 않습니다. 이는 참조 자체를 변경했기 때문입니다.

---

## Q5. 자바에서 매개변수 전달 방식은 무엇인가요?

**A:** 자바는 **값에 의한 호출(Call by Value)** 방식만을 사용합니다.
- 기본형 매개변수의 경우, 값 자체를 복사하여 전달합니다.
- 참조형 매개변수의 경우, 객체의 참조(주소)를 값으로 복사하여 전달합니다. 따라서 객체의 속성은 변경할 수 있지만, 참조 자체를 변경해도 원래 객체에는 영향을 미치지 않습니다.

---

## 요약
- 기본형 매개변수: 값 복사, 원래 값 변경 불가
- 참조형 매개변수: 참조 복사, 객체 속성 변경 가능
- 자바는 항상 값에 의한 호출 방식을 사용합니다.

