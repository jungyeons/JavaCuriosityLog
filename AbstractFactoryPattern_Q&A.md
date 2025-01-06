# 추상 팩토리 패턴 관련 질문



## Q1. 주어진 코드는 어떤 역할을 하나요?

```java
package factory;

import domain.product.dao.ProductDao;
import domain.product.dao.oracle.ProductOracleDao;
import domain.userinfo.dao.UserInfoDao;
import domain.userinfo.dao.oracle.UserInfoOracleDao;

public class OracleDaoFactory implements DaoFactory {

    @Override
    public UserInfoDao createUserInfoDao() {
        return new UserInfoOracleDao();
    }

    @Override
    public ProductDao createProuctDao() {
        return new ProductOracleDao();
    }
}
```

- **답변**: 이 코드는 `DaoFactory` 인터페이스를 구현하여 Oracle 데이터베이스에 특화된 DAO 객체(`UserInfoOracleDao`, `ProductOracleDao`)를 생성하는 `OracleDaoFactory` 클래스입니다.
- 팩토리 메서드를 통해 클라이언트는 객체 생성 방식에 대한 세부 정보를 몰라도 DAO 객체를 사용할 수 있습니다.

---

## Q2. `createUserInfoDao()`에서 `UserInfo`를 넘기지 않고도 객체가 생성되는 이유는 무엇인가요?

### 답변:
1. **기본 생성자(Default Constructor)**:
   - `new UserInfoOracleDao()` 호출 시, 클래스에 별도로 생성자를 정의하지 않았다면 자바는 자동으로 기본 생성자를 제공합니다.
   - 기본 생성자는 매개변수가 없으며, 객체를 초기화합니다.
     ```java
     public UserInfoOracleDao() {
         // 기본 생성자
     }
     ```

2. **DAO 객체는 무상태(Stateless)**:
   - DAO는 특정 데이터를 보유하지 않고, 데이터베이스 작업만 처리합니다.
   - 데이터를 필요로 할 경우, 메서드 호출 시점에 매개변수로 전달합니다.
     ```java
     userInfoDao.insertUserInfo(userInfo); // 여기서 데이터 전달
     ```

---

## Q3. `createUserInfoDao()`에서 데이터를 넘기지 않는 설계의 장점은 무엇인가요?

### 답변:
1. **책임 분리(Separation of Concerns)**:
   - 객체 생성과 데이터 처리를 분리합니다.
   - 팩토리 메서드는 DAO 객체 생성에만 집중하고, 데이터는 DAO 메서드 호출 시 전달됩니다.

2. **재사용성(Reusability)**:
   - DAO 객체는 특정 데이터에 의존하지 않으므로 여러 데이터 작업에 재사용할 수 있습니다.

3. **유연성(Flexibility)**:
   - 동일한 DAO 객체로 다양한 데이터를 처리할 수 있습니다.

---

## Q4. `OracleDaoFactory`의 구체적인 사용 예는 무엇인가요?

### 답변:
```java
DaoFactory factory = new OracleDaoFactory();
UserInfoDao userInfoDao = factory.createUserInfoDao();
ProductDao productDao = factory.createProuctDao();

// 데이터베이스 작업
UserInfo userInfo = new UserInfo("id123", "John Doe");
userInfoDao.insertUserInfo(userInfo);
```

1. 팩토리를 통해 DAO 객체를 생성합니다.
2. DAO 객체를 사용하여 데이터를 처리합니다.
   - 이 과정에서 `userInfo`와 같은 데이터를 메서드 호출 시 전달합니다.

---

## Q5. 추상 팩토리 패턴과 DAO 패턴의 핵심은 무엇인가요?

### 추상 팩토리 패턴(Abstract Factory Pattern)
- **정의**: 관련 객체의 군을 구체적인 클래스에 의존하지 않고 생성할 수 있는 인터페이스를 제공합니다.
- **장점**:
  1. 클라이언트와 구현 클래스 간의 결합도를 낮춥니다.
  2. 코드 변경 없이 다양한 구현체로 확장이 가능합니다.

### DAO(Data Access Object)
- **정의**: 데이터베이스 접근을 캡슐화하고, 객체 지향적으로 처리하기 위한 패턴입니다.
- **장점**:
  1. 데이터베이스 작업의 표준화와 단순화.
  2. 데이터 접근 로직과 비즈니스 로직의 분리.

---

## Q6. DAO 설계의 핵심 원칙은 무엇인가요?

### 답변:
1. **무상태 설계(Stateless Design)**:
   - DAO 객체는 상태를 가지지 않고, 데이터베이스와의 상호작용에만 집중합니다.

2. **유지보수 용이(Maintainability)**:
   - 데이터베이스 작업이 변경되더라도 DAO 내부에서 처리되므로 클라이언트 코드는 영향을 받지 않습니다.

3. **테스트 용이성(Testability)**:
   - DAO 객체를 Mock 객체로 대체하여 쉽게 테스트할 수 있습니다.

---

## 요약

- **왜 데이터를 넘기지 않는가?**
  - DAO 객체는 무상태(stateless)로 설계되어 생성 시 데이터를 필요로 하지 않습니다.
  - 데이터는 DAO의 메서드 호출 시점에 전달됩니다.

- **이 설계의 장점은?**
  - 객체 생성과 데이터 처리를 분리하여 재사용성과 유연성을 향상.
  - 클라이언트 코드와 구현 세부 사항을 분리하여 결합도를 낮춤.

- **결론**:
  - 추상 팩토리 패턴과 DAO 패턴을 조합하여 유지보수성과 확장성이 높은 코드를 작성할 수 있습니다.
