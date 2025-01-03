# 자바 클래스 초기화 방식 관련 질문

## 질문

```java
import java.util.ArrayList;

public class BookShelf {

    ArrayList<Book> BookShelf = new ArrayList<Book>();

    public void addBook(Book book) {
        BookShelf.add(book);
    }

}
```

이렇게 해주면 안되나요? 꼭 생성자에서

```java
class BookShelf {

    private ArrayList<Book> shelf;

    public BookShelf() {
        shelf = new ArrayList<Book>();
    } 
}
```

이렇게 해줘야 하나요?

---

## 답변

두 코드 스타일 모두 기능적으로 동작할 수 있지만, `ArrayList<Book>`를 명시적으로 생성자에서 초기화하는 방식이 일반적으로 더 좋은 관행으로 간주됩니다. 이를 설명하겠습니다:

### 첫 번째 방식:

```java
ArrayList<Book> BookShelf = new ArrayList<Book>();

public void addBook(Book book) {
    BookShelf.add(book);
}
```

#### 문제점:
- **필드 이름과 관례:** 클래스의 필드 이름 `BookShelf`가 대문자로 시작되어 혼란을 줄 수 있습니다. 자바에서는 변수나 필드 이름은 소문자로 시작하는 것이 관례입니다.
- **가독성 문제:** `BookShelf`는 이미 클래스 이름으로 사용되고 있는데, 같은 이름을 필드로도 사용하면 가독성과 유지보수에 부정적인 영향을 미칠 수 있습니다.
- **유연성 부족:** 필드가 생성자 외부에서 즉시 초기화되므로 유연성이 떨어집니다. 나중에 더 복잡한 초기화 논리가 필요할 경우 수정이 어려울 수 있습니다.

#### 기술적 동작:
- 이 방식도 동작은 하지만, 위의 문제들 때문에 권장되지 않습니다.

---

### 두 번째 방식:

```java
private ArrayList<Book> shelf;

public BookShelf() {
    shelf = new ArrayList<Book>();
}
```

#### 장점:
1. **초기화 책임 분리:** 생성자에서 초기화 로직을 담당하기 때문에, `shelf`를 초기화하는 로직이 명확해지고 유연성을 제공합니다. 예를 들어, 생성자에서 초기값을 지정하거나, 특수한 조건에 따라 다르게 초기화할 수 있습니다.
2. **가독성:** 필드 이름과 클래스 이름이 명확히 구분되고, 소문자로 시작하는 관례를 따릅니다.
3. **확장성:** 생성자에 다른 매개변수를 추가하여 다양한 초기화 시나리오를 처리할 수 있습니다.

---

### 요약

1. **권장 방식:** 두 번째 방식이 더 나은 설계로 간주됩니다. 생성자에서 `shelf`를 명시적으로 초기화하면 클래스의 의도가 더 명확해지고, 유지보수성이 높아집니다.
2. **일관성:** 자바 코딩 표준 및 관례에 맞게 설계하려면, 두 번째 방식처럼 생성자를 활용하고 필드 이름에 소문자를 사용하는 것이 좋습니다.
3. **예외 상황:** 아주 간단한 클래스에서 별도의 초기화 로직이 필요하지 않은 경우, 첫 번째 방식도 무리가 없지만, 좋은 코드 습관을 위해 두 번째 방식을 채택하는 것이 일반적입니다.
