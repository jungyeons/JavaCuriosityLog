# Comparator vs Comparable

## Q1: `Comparable`와 `Comparator`의 차이점은 무엇인가요?

**A1**: 
- `Comparable`과 `Comparator`는 모두 객체를 비교하는 데 사용되지만, 사용 목적과 적용 방식에서 차이가 있습니다.
  - **Comparable**: 객체 자신이 `compareTo()` 메서드를 구현하여 다른 객체와 비교할 수 있게 만드는 인터페이스입니다. 주로 정렬 순서를 자연스럽게 정의할 때 사용합니다.
  - **Comparator**: 외부에서 객체를 비교할 수 있도록 `compare()` 메서드를 정의하는 인터페이스입니다. 비교 로직을 별도의 클래스로 분리하여 더 유연하게 사용할 수 있습니다.

---

## Q2: `Comparable`을 사용하는 방법은 무엇인가요?

**A2**: 
`Comparable`을 사용하려면 클래스가 `Comparable` 인터페이스를 구현하고, `compareTo()` 메서드를 오버라이드하여 객체 비교를 정의해야 합니다. 

### 예시:
```java
class Person implements Comparable<Person> {
    String name;
    int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int compareTo(Person other) {
        // 나이 기준으로 비교 (오름차순)
        return Integer.compare(this.age, other.age);
    }
}
