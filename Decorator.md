여기 우리의 대화를 마크다운 파일 형식으로 정리해 드렸습니다:

```markdown
# 데코레이터 패턴에 대한 대화

## 사용자 질문
> 왜 데코레이터 패턴을 쓰지? 그냥 상속이면 상속 포함이면 포함 쓰면되는거 아닌가?

## 나의 답변

### 1. 데코레이터 패턴의 목적
데코레이터 패턴은 **객체의 기능을 런타임에 동적으로 추가하거나 수정**할 수 있게 해줍니다. 이를 통해 코드 재사용성과 유연성을 높일 수 있습니다. 상속이나 포함을 사용하는 경우 고정적인 설계가 강요되는 반면, 데코레이터는 훨씬 더 유연하게 동작을 확장할 수 있습니다.

---

### 2. 상속의 한계
- **클래스 폭발 문제**  
  상속을 통해 기능을 추가하거나 변경하려면, 조합 가능한 모든 경우에 대해 새로운 서브클래스를 만들어야 합니다.  
  예:  
  - `BasicPizza`  
  - `CheesePizza`  
  - `PepperoniPizza`  
  - `CheesePepperoniPizza`  
  조합이 늘어날수록 서브클래스가 기하급수적으로 증가합니다.

- **유연성 부족**  
  상속은 컴파일 타임에 결정되므로, 객체의 행동을 런타임에 변경하기 어렵습니다. 동적으로 객체의 일부 기능만 추가하거나 제거하는 데는 적합하지 않습니다.

---

### 3. 포함(Composition)의 한계
포함을 사용하면 객체 내부에 또 다른 객체를 포함시켜 기능을 확장할 수 있습니다. 하지만 이 경우:
- 기능 추가가 필요한 모든 객체마다 포함된 객체를 관리하는 코드가 중복됩니다.
- 포함된 객체의 인터페이스를 다시 노출하거나 래핑(wrapping)하는 코드가 늘어납니다.
- 새로운 기능이 추가될 때 기존의 포함 관계를 수정해야 할 수 있습니다.

---

### 4. 데코레이터 패턴의 장점
- **조합의 유연성**  
  데코레이터는 객체를 감싸는 방식으로 동작하므로, 여러 데코레이터를 조합하여 다양한 기능을 동적으로 구성할 수 있습니다.
  ```python
  pizza = BasicPizza()
  pizza_with_cheese = CheeseDecorator(pizza)
  pizza_with_cheese_and_pepperoni = PepperoniDecorator(pizza_with_cheese)
  ```
  위와 같은 방식으로 새로운 기능을 추가할 때 기존 클래스를 수정하지 않고 조합만 변경하면 됩니다.

- **열린-폐쇄 원칙(OCP)** 준수  
  기존 코드를 변경하지 않고도 새로운 데코레이터를 추가하여 확장이 가능합니다.

- **기능의 동적 추가 및 제거**  
  데코레이터는 런타임에 객체의 기능을 동적으로 추가하거나 제거할 수 있습니다.  
  예: 특정 조건에 따라 특정 데코레이터를 추가하거나 제거하는 작업이 가능.

- **단일 책임 원칙(SRP) 강화**  
  각 데코레이터는 하나의 책임(기능 추가)만을 수행하므로, 클래스를 더 작고 이해하기 쉽게 분리할 수 있습니다.

---

### 5. 적용 예시
#### 상속 기반 설계의 문제점:
```python
class Beverage:
    def cost(self):
        return 5

class MilkBeverage(Beverage):
    def cost(self):
        return super().cost() + 2

class MilkAndSugarBeverage(Beverage):
    def cost(self):
        return super().cost() + 3  # 코드 중복
```

#### 데코레이터 패턴:
```python
class Beverage:
    def cost(self):
        return 5

class BeverageDecorator(Beverage):
    def __init__(self, beverage):
        self.beverage = beverage

    def cost(self):
        return self.beverage.cost()

class MilkDecorator(BeverageDecorator):
    def cost(self):
        return super().cost() + 2

class SugarDecorator(BeverageDecorator):
    def cost(self):
        return super().cost() + 1

# 조합
beverage = Beverage()
milk_beverage = MilkDecorator(beverage)
milk_and_sugar_beverage = SugarDecorator(milk_beverage)
print(milk_and_sugar_beverage.cost())  # 8
```

---

### 6. 언제 데코레이터를 사용할까?
- 객체의 기능을 런타임에 동적으로 추가하거나 변경해야 할 때.
- 상속으로 인한 클래스 폭발 문제를 피하고 싶을 때.
- 객체의 기능을 조합해서 유연하게 구성하고 싶을 때.
- 변경 가능한 환경에서 기능을 추가 및 제거하는 요구가 있을 때.

---

### 결론
상속과 포함은 여전히 유용하지만, 데코레이터 패턴은 **조합 가능한 객체 설계**를 위한 훨씬 더 유연한 방법을 제공합니다. 특히 런타임에서의 기능 변경, 코드 중복 감소, 확장성 확보라는 측면에서 강력한 도구입니다. 필요에 따라 세 가지 접근 방식을 조화롭게 사용하는 것이 가장 좋은 설계 전략이 될 것입니다.
```

