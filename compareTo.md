
# Q&A

## Q: Comparable을 상속해야만 compareTo를 쓸수있는거같은데 나는 분명 string 클래스에서도 비슷한 걸 했던거같단말이지..
A: 맞습니다! `compareTo()` 메서드는 `Comparable` 인터페이스의 메서드로, 클래스가 이 인터페이스를 구현해야 사용할 수 있습니다. 그런데, `String` 클래스도 `compareTo()`를 제공하는데, 이는 `String` 클래스가 이미 `Comparable<String>`을 구현하고 있기 때문입니다.

즉, `String` 클래스는 `Comparable` 인터페이스를 구현하고 있으며, 이로 인해 `compareTo()` 메서드를 사용할 수 있습니다.

```java
String str1 = "apple";
String str2 = "banana";
int result = str1.compareTo(str2); // "apple"과 "banana"를 비교
```

`String` 클래스에서 `compareTo()` 메서드는 두 문자열을 사전순으로 비교하여, 그 결과에 따라 음수, 0, 양수를 반환합니다.

- `str1.compareTo(str2)`가 **음수**이면 `str1`이 `str2`보다 사전순으로 앞에 있습니다.
- **0**이면 두 문자열이 같습니다.
- **양수**이면 `str1`이 `str2`보다 사전순으로 뒤에 있습니다.

이와 같이, `String`은 이미 `Comparable` 인터페이스를 구현했기 때문에 `compareTo()` 메서드를 별도로 정의하지 않아도 사용할 수 있습니다.

만약 자신의 클래스에서 `compareTo()` 메서드를 사용하고 싶다면, 해당 클래스에서 `Comparable` 인터페이스를 구현해야 합니다. 예를 들어:

```java
class MyClass implements Comparable<MyClass> {
    int value;
    
    MyClass(int value) {
        this.value = value;
    }

    @Override
    public int compareTo(MyClass other) {
        return Integer.compare(this.value, other.value); // 'value'를 기준으로 비교
    }
}
```

이렇게 `compareTo()`를 구현하면, `MyClass` 객체들에 대해서도 `compareTo()`를 사용할 수 있게 됩니다.
