# 얕은 복사(Shallow Copy)와 깊은 복사(Deep Copy) in Java

## 얕은 복사 (Shallow Copy)

### 정의
- 얕은 복사는 객체의 필드 값을 복사하지만, **필드가 참조형(객체를 참조)** 인 경우, 그 참조만 복사됩니다. 
- 복사된 객체와 원본 객체가 **같은 참조**를 공유하게 됩니다.

### 특징
- 복사된 객체와 원본 객체가 같은 참조를 공유합니다.
- 원본 객체에서 참조형 필드의 값을 변경하면 복사된 객체에도 영향을 미칩니다.

### 구현 방법
- `Object` 클래스의 `clone()` 메서드를 기본적으로 사용하면 얕은 복사가 수행됩니다.
- 기본 자료형은 값이 복사되고, 참조형 필드는 참조 주소가 복사됩니다.

### 예제
```java
class Book {
    String title;
    
    public Book(String title) {
        this.title = title;
    }
}

class BookShelf {
    Book book;
    
    public BookShelf(Book book) {
        this.book = book;
    }
}

public class Main {
    public static void main(String[] args) {
        Book book1 = new Book("Java Programming");
        BookShelf shelf1 = new BookShelf(book1);
        
        // 얕은 복사
        BookShelf shelf2 = shelf1; // 참조 주소 복사
        
        shelf2.book.title = "Python Programming"; // shelf2를 수정
        
        System.out.println(shelf1.book.title); // "Python Programming" (원본도 영향받음)
    }
}
```

### 결과
- `shelf1`과 `shelf2`는 같은 `Book` 객체를 참조하므로, 한쪽에서 데이터를 변경하면 다른 쪽도 영향을 받습니다.

---

## 깊은 복사 (Deep Copy)

### 정의
- 깊은 복사는 객체의 필드 값뿐만 아니라, 필드가 참조형인 경우 **그 참조 대상까지 새롭게 복사**합니다.
- 결과적으로 복사된 객체는 원본 객체와 완전히 독립적인 상태가 됩니다.

### 특징
- 복사된 객체와 원본 객체가 **완전히 독립적**입니다.
- 원본 객체를 변경해도 복사된 객체에 영향을 미치지 않습니다.

### 구현 방법
- 참조형 필드를 수동으로 복사하여 새로운 객체를 생성합니다.
- `clone()` 메서드를 오버라이드하여 깊은 복사를 구현할 수 있습니다.

### 예제
```java
class Book {
    String title;

    public Book(String title) {
        this.title = title;
    }
}

class BookShelf implements Cloneable {
    Book book;

    public BookShelf(Book book) {
        this.book = book;
    }

    @Override
    protected BookShelf clone() {
        // 깊은 복사 구현
        return new BookShelf(new Book(this.book.title));
    }
}

public class Main {
    public static void main(String[] args) {
        Book book1 = new Book("Java Programming");
        BookShelf shelf1 = new BookShelf(book1);
        
        // 깊은 복사
        BookShelf shelf2 = shelf1.clone();
        
        shelf2.book.title = "Python Programming"; // shelf2를 수정
        
        System.out.println(shelf1.book.title); // "Java Programming" (원본 영향 없음)
    }
}
```

### 결과
- `shelf1`과 `shelf2`는 각각 독립적인 `Book` 객체를 참조하므로, 한쪽에서 데이터를 변경해도 다른 쪽에 영향을 미치지 않습니다.

---

## 얕은 복사와 깊은 복사의 차이

| 특징                    | 얕은 복사                          | 깊은 복사                          |
|-------------------------|-------------------------------------|-------------------------------------|
| **복사 방식**           | 참조 주소만 복사                   | 참조 객체까지 복사                  |
| **독립성**              | 원본과 복사본이 서로 의존적         | 원본과 복사본이 서로 독립적         |
| **구현 복잡도**         | 상대적으로 간단                    | 상대적으로 복잡                     |
| **적용 예**             | `Object.clone()` 기본 구현          | 수동 구현, Serializable, 라이브러리  |

---

## 사용 시 고려사항
- 얕은 복사는 속도가 빠르고 메모리를 적게 사용하지만, 참조 객체의 공유로 인해 데이터 불일치 문제가 생길 수 있습니다.
- 깊은 복사는 메모리를 더 많이 사용하며 구현이 복잡하지만, 안전한 데이터 복사를 보장합니다.
- 사용 사례에 따라 얕은 복사와 깊은 복사를 선택해야 합니다.
