

Q. 자바 Scanner 관련 정리해서 제공해줘.

A. 정리한 자바 `Scanner` 클래스 메서드 사용법입니다.



# 자바 Scanner 클래스 메서드 사용법


## 1. `next()`
- **역할**: 공백(스페이스, 탭, 줄바꿈 등) 전까지의 단어를 읽음.
- **특징**:
  - 한 단어 단위로 입력을 처리.
  - 공백을 기준으로 나누어 입력을 구분.
  - 입력 버퍼에 남아있는 공백은 제거하지 않음.
- **사용 예시**:
  ```java
  Scanner scanner = new Scanner(System.in);
  System.out.println("Enter a string:");
  String word = scanner.next();
  System.out.println("You entered: " + word);
  ```

## 2. `nextLine()`
- **역할**: 한 줄 전체를 입력받음 (줄바꿈 문자까지 포함).
- **특징**:
  - 입력 버퍼의 모든 내용을 읽어들임.
  - 줄바꿈(\n)이 입력될 때까지 대기.
  - 이전에 다른 `next()` 메서드로 데이터를 읽은 경우, 입력 버퍼에 남아 있는 줄바꿈 문자 때문에 예상치 못한 결과가 발생할 수 있음.
- **사용 예시**:
  ```java
  Scanner scanner = new Scanner(System.in);
  System.out.println("Enter a line:");
  String line = scanner.nextLine();
  System.out.println("You entered: " + line);
  ```

### `next()`와 `nextLine()` 혼합 사용 시 주의사항
```java
Scanner scanner = new Scanner(System.in);
System.out.print("Enter a word: ");
String word = scanner.next();  // 단어 하나 입력.
System.out.print("Enter a line: ");
scanner.nextLine();            // 버퍼에 남아있는 줄바꿈 처리.
String line = scanner.nextLine();  // 이후에 실제 입력 라인 받기.
```

## 3. `nextInt()`, `nextDouble()` 등
- **역할**: 특정 타입의 데이터를 읽음 (정수, 실수 등).
- **특징**:
  - 입력된 데이터가 해당 타입으로 변환 가능해야 함.
  - 숫자 외의 값 입력 시 예외(`InputMismatchException`) 발생.
  - 숫자 입력 후 남은 줄바꿈 문자가 입력 버퍼에 남아 있어 `nextLine()` 호출 시 문제가 발생할 수 있음.
- **사용 예시**:
  ```java
  Scanner scanner = new Scanner(System.in);
  System.out.print("Enter an integer: ");
  int number = scanner.nextInt();
  System.out.println("You entered: " + number);
  ```

## 4. 버퍼 문제 해결
- 숫자 입력 후 문자열을 읽으려면 `nextLine()`을 호출하여 입력 버퍼를 비워야 함.
- 예시:
  ```java
  Scanner scanner = new Scanner(System.in);
  System.out.print("Enter an integer: ");
  int number = scanner.nextInt();
  scanner.nextLine();  // 남아있는 줄바꿈 문자 제거.
  System.out.print("Enter a line: ");
  String line = scanner.nextLine();
  System.out.println("You entered: " + line);
  ```

## 5. 다양한 입력 메서드 정리

| 메서드               | 설명                               | 예시 입력        | 결과         |
|----------------------|------------------------------------|------------------|--------------|
| `next()`            | 공백 전까지 읽음                  | "Hello World"    | `Hello`      |
| `nextLine()`        | 한 줄 전체를 읽음                 | "Hello World"    | `Hello World` |
| `nextInt()`         | 정수값을 읽음                     | `42`             | `42`         |
| `nextDouble()`      | 실수값을 읽음                     | `3.14`           | `3.14`       |
| `hasNext()`         | 다음 입력이 있는지 확인           |                  | `true/false` |
| `hasNextInt()`      | 다음 입력이 정수인지 확인         |                  | `true/false` |

## 6. 예외 처리
입력 도중 예상치 못한 예외 상황을 대비하려면 `try-catch`를 사용하는 것이 좋습니다.
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        try {
            System.out.print("Enter an integer: ");
            int number = scanner.nextInt();
            System.out.println("You entered: " + number);
        } catch (Exception e) {
            System.out.println("Invalid input. Please enter a valid integer.");
        }
    }
}
```

## 요약
1. **`next()`**: 단어 단위로 입력 처리.
2. **`nextLine()`**: 한 줄 전체 입력.
3. **`nextInt()`, `nextDouble()` 등**: 특정 타입의 입력 처리.
4. **입력 버퍼 문제**: 숫자 입력 후 `nextLine()` 사용 시 버퍼 정리 필요.
5. **예외 처리**: 사용자 입력 오류를 대비한 `try-catch` 사용 추천.
```

위 마크다운 문서는 자바 `Scanner` 클래스의 주요 메서드를 설명하고, 각 메서드의 사용법과 주의 사항을 정리한 것입니다. 이 문서를 사용하여 `Scanner` 클래스를 효과적으로 활용할 수 있습니다!
