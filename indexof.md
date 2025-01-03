
Q. indexOf 관련해서 헷갈리네 정리해줘.   
A. 자바의 `indexOf` 메서드는 문자열이나 리스트에서 특정 값의 첫 번째 발생 위치(인덱스)를 찾는 데 사용됩니다. 아래에 메서드에 대한 정리를 제공합니다.



## 1. **`String` 클래스에서 `indexOf`**
### **역할**
`String` 클래스의 `indexOf` 메서드는 특정 문자 또는 문자열이 처음으로 등장하는 **인덱스(위치)**를 반환합니다.

### **메서드 시그니처**
1. **문자 찾기**
   ```java
   public int indexOf(int ch)
   ```
   - 입력된 문자(`ch`)가 문자열에서 처음으로 나타나는 위치를 반환.

2. **문자열 찾기**
   ```java
   public int indexOf(String str)
   ```
   - 입력된 문자열(`str`)이 처음으로 나타나는 위치를 반환.

3. **특정 위치부터 문자 찾기**
   ```java
   public int indexOf(int ch, int fromIndex)
   ```
   - `fromIndex`부터 시작해 해당 문자의 위치를 반환.

4. **특정 위치부터 문자열 찾기**
   ```java
   public int indexOf(String str, int fromIndex)
   ```
   - `fromIndex`부터 시작해 해당 문자열의 위치를 반환.

---

### **특징**
- 인덱스는 **0부터 시작**.
- 찾는 값이 없으면 **`-1` 반환**.
- 대소문자를 구분함.

---

### **사용 예시**
```java
public class Main {
    public static void main(String[] args) {
        String text = "Hello, World!";

        // 문자 찾기
        System.out.println(text.indexOf('o')); // 4

        // 문자열 찾기
        System.out.println(text.indexOf("World")); // 7

        // 특정 위치 이후부터 문자 찾기
        System.out.println(text.indexOf('o', 5)); // 8

        // 특정 위치 이후부터 문자열 찾기
        System.out.println(text.indexOf("World", 10)); // -1 (찾을 수 없음)
    }
}
```

---

## 2. **`List`와 `indexOf`**
### **역할**
`List` 인터페이스의 `indexOf` 메서드는 리스트에서 특정 요소가 **처음으로 등장하는 위치**를 반환합니다.

### **메서드 시그니처**
```java
public int indexOf(Object o)
```
- 리스트에서 `o`가 처음으로 나타나는 위치를 반환.
- 객체가 없으면 **`-1` 반환**.

---

### **특징**
- 리스트가 **중복 값을 가질 수 있는 경우**, 첫 번째로 발견된 값의 위치를 반환.
- 객체 비교 시 **`equals` 메서드**를 사용해 비교.

---

### **사용 예시**
```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");
        list.add("Apple");

        // 요소의 첫 번째 위치 찾기
        System.out.println(list.indexOf("Apple")); // 0

        // 요소가 존재하지 않을 때
        System.out.println(list.indexOf("Grape")); // -1
    }
}
```

---

## 3. **`lastIndexOf` 메서드**
### **역할**
`indexOf`가 첫 번째 발생 위치를 찾는 데 사용된다면, `lastIndexOf`는 **마지막으로 등장하는 위치**를 반환합니다.

### **String 클래스**
```java
public int lastIndexOf(int ch)
public int lastIndexOf(String str)
public int lastIndexOf(int ch, int fromIndex)
public int lastIndexOf(String str, int fromIndex)
```

### **List 인터페이스**
```java
public int lastIndexOf(Object o)
```

---

### **사용 예시**
#### `String`에서 `lastIndexOf`:
```java
public class Main {
    public static void main(String[] args) {
        String text = "Hello, World!";
        
        // 문자 마지막 위치 찾기
        System.out.println(text.lastIndexOf('o')); // 8

        // 문자열 마지막 위치 찾기
        System.out.println(text.lastIndexOf("World")); // 7

        // 특정 위치 이전까지의 문자 마지막 위치
        System.out.println(text.lastIndexOf('o', 5)); // 4
    }
}
```

#### `List`에서 `lastIndexOf`:
```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");
        list.add("Apple");

        // 요소의 마지막 위치 찾기
        System.out.println(list.lastIndexOf("Apple")); // 3
    }
}
```

---

## 4. **에러 방지 팁**
- 찾고자 하는 값이 없으면 **`-1`**을 반환하므로 조건문으로 처리:
  ```java
  int index = text.indexOf("Java");
  if (index != -1) {
      System.out.println("Found at index: " + index);
  } else {
      System.out.println("Not found.");
  }
  ```

- 대소문자를 구분하지 않는 검색은 입력값을 **소문자 또는 대문자로 변환** 후 사용:
  ```java
  String text = "Hello, World!";
  int index = text.toLowerCase().indexOf("hello".toLowerCase());
  System.out.println(index); // 0
  ```

---

## 5. **정리**

| 메서드                              | 설명                                  | 예시 입력                  | 결과    |
|-------------------------------------|---------------------------------------|----------------------------|---------|
| `indexOf(char ch)`                  | 특정 문자의 첫 번째 위치 반환         | `'o'`                      | `4`     |
| `indexOf(String str)`               | 특정 문자열의 첫 번째 위치 반환       | `"World"`                  | `7`     |
| `indexOf(char ch, int fromIndex)`   | 특정 위치 이후 문자의 첫 번째 위치    | `'o', 5`                   | `8`     |
| `lastIndexOf(char ch)`              | 특정 문자의 마지막 위치 반환          | `'o'`                      | `8`     |
| `List.indexOf(Object o)`            | 리스트에서 객체의 첫 번째 위치 반환   | `"Apple"`                  | `0`     |
| `List.lastIndexOf(Object o)`        | 리스트에서 객체의 마지막 위치 반환    | `"Apple"`                  | `3`     |

위 내용을 바탕으로 `indexOf` 메서드를 다양한 상황에서 적절히 활용할 수 있습니다! 😊
