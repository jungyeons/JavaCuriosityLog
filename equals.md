
# Q&A: equals vs == in Java

## Q: 	class Student implements Comparable<Student> {

	 

		int age;			// 나이

		int classNumber;	// 학급

		

		Student(int age, int classNumber) {

			this.age = age;

			this.classNumber = classNumber;

		}

		

		@Override

		public int compareTo(Student o) {

	    

			// 자기자신의 age가 o의 age보다 크다면 양수

			if(this.age > o.age) {

				return 142352;

			}

			// 자기 자신의 age와 o의 age가 같다면 0

			else if(this.age == o.age) {

				return 0;

			}

			// 자기 자신의 age가 o의 age보다 작다면 음수

			else {

				return -1324;

			}

		}

	}에서 == 대신 equals를 써도되나? 또 헷갈림 ㅠㅠ
A: 좋은 질문입니다! `compareTo()` 메서드 내에서 `==` 대신 `equals()`를 사용할 수 있는지에 대해 헷갈릴 수 있습니다. 그러나 **`compareTo()` 메서드 내에서는 `==`와 `equals()`를 다르게 사용해야 합니다.**

### `==` vs `equals()`

- **`==` 연산자**: 객체의 **참조**를 비교합니다. 즉, 두 객체가 **같은 메모리 주소**를 참조하는지를 확인합니다. 기본 타입의 경우 값 자체를 비교하지만, 객체에서는 두 객체가 **동일한 객체인지** 비교합니다.
  
- **`equals()` 메서드**: 객체의 **값**을 비교합니다. 이 메서드는 일반적으로 객체가 의미하는 "내용"이 같은지를 비교하는 데 사용됩니다. 예를 들어, `String` 클래스의 `equals()`는 문자열의 **내용**이 같은지를 비교합니다.

### `compareTo()`에서의 사용

`compareTo()` 메서드는 두 객체를 **비교**하는 메서드이기 때문에, **값을 기준으로 비교**해야 합니다. 이때 `==`는 참조 비교이므로 두 객체의 내용을 비교하려면 `equals()`를 사용하는 것이 적절합니다.

### 주어진 코드에 대한 설명:

```java
@Override
public int compareTo(Student o) {
    if (this.age > o.age) {
        return 142352;  // 양수 반환
    } else if (this.age == o.age) {
        return 0;  // 두 나이가 같으면 0 반환
    } else {
        return -1324;  // 음수 반환
    }
}
```

위 코드에서는 `this.age`와 `o.age`를 비교하고 있으므로, `age`가 같은지 확인할 때 `==`를 사용하는 것이 적합합니다. 여기서 `equals()`를 사용할 필요는 없습니다. `age`는 `int` 타입이기 때문에 `==`로 값을 비교하는 것이 올바릅니다.

그러나 **객체**나 **복잡한 데이터 타입**을 비교할 때는 `equals()`를 사용해야 할 수 있습니다. 예를 들어, 두 `String` 객체가 **내용**이 같은지 확인할 때는 `equals()`를 사용하는 것이 적합합니다.

### 결론:
- **`age`처럼 기본 타입(int)을 비교할 때는 `==`를 사용합니다.**
- **복잡한 객체를 비교할 때는 `equals()`를 사용해야 합니다.**

따라서, 현재 코드에서는 `==`를 그대로 사용하는 것이 맞습니다! `age`는 기본 타입이므로 `equals()`를 사용할 필요는 없습니다.
