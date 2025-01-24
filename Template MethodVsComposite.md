# Q&A: Template Method 패턴과 Composite 패턴의 차이

## Q: Template Method 패턴과 Composite 패턴의 차이애 대해서 설명해주세요
### A:
Template Method 패턴은 **상위 클래스에서 알고리즘의 기본 뼈대를 정의**하고, **구체적인 구현은 하위 클래스에서 처리하도록** 설계된 패턴입니다. 알고리즘의 "일부 단계"만 서브클래스에서 오버라이드하도록 허용하며, 공통적인 알고리즘 흐름은 상위 클래스에 고정됩니다.

### 특징:
- 알고리즘의 구조(골격)를 상위 클래스에서 정의.
- 일부 세부 구현은 하위 클래스에서 재정의.
- 상속을 기반으로 동작.

### 예시 코드:
```python
from abc import ABC, abstractmethod

class Game(ABC):
    def play(self):
        self.initialize()
        self.start_play()
        self.end_play()

    @abstractmethod
    def initialize(self):
        pass

    @abstractmethod
    def start_play(self):
        pass

    @abstractmethod
    def end_play(self):
        pass

class Football(Game):
    def initialize(self):
        print("Football Game Initialized!")

    def start_play(self):
        print("Football Game Started!")

    def end_play(self):
        print("Football Game Ended!")

# 사용
game = Football()
game.play()
```

---

### A:
Composite 패턴은 **객체의 계층 구조(특히 트리 구조)를 다룰 때** 사용됩니다. 클라이언트가 개별 객체(Leaf)와 복합 객체(Composite)를 **동일한 방식**으로 다룰 수 있도록 설계됩니다.

### 특징:
- 객체를 트리 구조로 구성.
- 개별 객체(Leaf)와 복합 객체(Composite)를 동일하게 처리 가능.
- "부분-전체 관계"를 처리하며, 재귀적으로 구성된 구조를 다룸.

### 예시 코드:
```python
from abc import ABC, abstractmethod

class Component(ABC):
    @abstractmethod
    def operation(self):
        pass

class Leaf(Component):
    def __init__(self, name):
        self.name = name

    def operation(self):
        print(f"Leaf {self.name} operation")

class Composite(Component):
    def __init__(self):
        self.children = []

    def add(self, component):
        self.children.append(component)

    def operation(self):
        for child in self.children:
            child.operation()

# 사용
leaf1 = Leaf("A")
leaf2 = Leaf("B")
composite = Composite()
composite.add(leaf1)
composite.add(leaf2)
composite.operation()
```

---

## Q: Template Method 패턴과 Composite 패턴의 주요 차이점은 무엇인가요?

### A:
| **비교 항목**           | **Template Method 패턴**                          | **Composite 패턴**                              |
|--------------------------|---------------------------------------------------|------------------------------------------------|
| **목적**                | 알고리즘 구조를 정의하고 세부 사항을 하위 클래스에 위임 | 객체를 트리 구조로 구성하고 부분-전체 계층을 동일하게 다룸 |
| **사용 상황**           | 알고리즘의 일부를 재정의하거나 확장해야 하는 경우      | 객체를 재귀적으로 구성하고, 클라이언트가 개별/복합 객체를 동일하게 다뤄야 하는 경우 |
| **구성 요소**           | 상위 클래스(템플릿)와 하위 클래스                   | Component(추상화), Leaf, Composite           |
| **패턴의 핵심 메커니즘** | 상속을 통해 알고리즘 단계 재정의                    | 재귀적인 트리 구조 처리                          |
| **유연성**              | 알고리즘의 흐름이 고정됨                          | 객체를 자유롭게 추가/구성 가능                   |

---

## Q: 두 패턴은 어떤 상황에서 사용하나요?
- **Template Method 패턴**은 알고리즘의 큰 흐름을 고정하고, 세부 단계를 커스터마이즈해야 할 때 적합합니다.
- **Composite 패턴**은 트리 구조를 다루는 경우, 개별 객체와 복합 객체를 동일하게 취급해야 할 때 사용합니다.
