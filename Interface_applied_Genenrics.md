```markdown

**질문:**

```java
class FruitBox<T extends Fruit & Eatable>
```

이렇게 `Fruit` 클래스와 `Eatable` 인터페이스를 다중 상속받도록 지정할 수 있습니다. 그렇다면 `Fruit`이 인터페이스인 경우에는 어떻게 해야 하나요? `<T implements Fruit & Eatable>`로 작성하면 되나요?

**답변:**

Java에서 제네릭 타입 파라미터를 정의할 때, 특정 클래스와 인터페이스를 동시에 상속받도록 제한하려면 `extends` 키워드를 사용하고, '&' 연산자를 통해 다중 상속을 지정합니다. 

예를 들어, `Fruit` 클래스를 상속받고 `Eatable` 인터페이스를 구현하는 타입만을 허용하려면 다음과 같이 작성합니다:

```java
class FruitBox<T extends Fruit & Eatable> {
    // 클래스 구현
}
```

이렇게 하면 `Fruit` 클래스를 상속받고 `Eatable` 인터페이스를 구현한 타입만이 `FruitBox`의 타입 파라미터로 사용될 수 있습니다.

만약 `Fruit`이 클래스가 아니라 인터페이스라면, Java에서는 다중 상속을 지원하지 않기 때문에 두 개 이상의 클래스를 동시에 상속받을 수 없습니다.

그러나 여러 인터페이스를 동시에 구현하는 것은 가능합니다.

따라서 `Fruit`과 `Eatable`이 모두 인터페이스라면, 다음과 같이 작성할 수 있습니다:

```java
class FruitBox<T extends Fruit & Eatable> {
    // 클래스 구현
}
```

이 경우에도 `Fruit`과 `Eatable` 인터페이스를 모두 구현한 타입만이 `FruitBox`의 타입 파라미터로 사용될 수 있습니다.

하지만 제네릭 타입 파라미터 선언에서 `implements` 키워드는 사용할 수 없습니다.

제네릭 타입 파라미터의 상한 경계를 지정할 때는 항상 `extends` 키워드를 사용하며, 이는 클래스와 인터페이스 모두에 적용됩니다.

따라서 `T implements Fruit & Eatable`과 같은 선언은 유효하지 않습니다.

**추가 질문:**

그런데 또 헷갈리는 게 `class A implements B, C` 이건 또 가능하잖아?

**추가 답변:**

네, 맞습니다. Java에서는 한 클래스가 여러 인터페이스를 구현할 수 있습니다.

예를 들어:

```java
class A implements B, C {
    // 클래스 구현
}
```

이렇게 작성하면 `A` 클래스는 `B`와 `C` 인터페이스를 모두 구현하게 됩니다.

그러나 제네릭 타입 파라미터를 선언할 때는 `implements` 키워드를 사용할 수 없으며, 항상 `extends` 키워드를 사용해야 합니다.

이는 제네릭 타입 파라미터의 상한 경계를 지정할 때 적용되며, 클래스와 인터페이스 모두에 해당됩니다.

따라서 `T implements Fruit & Eatable`과 같은 선언은 유효하지 않으며, 대신 `T extends Fruit & Eatable`로 작성해야 합니다. 

이러한 차이는 클래스 정의와 제네릭 타입 파라미터 선언에서의 문법적 규칙에 기인합니다.

클래스 정의에서는 `implements` 키워드를 사용하여 여러 인터페이스를 구현할 수 있지만, 제네릭 타입 파라미터 선언에서는 `extends` 키워드를 사용하여 상한 경계를 지정해야 합니다.
``` 
