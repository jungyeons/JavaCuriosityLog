# Lock & Condition in Java

## 질문
lock & condition 관련해서 설명해주세요. (synchronized랑 비교해서요)

## 답변

`Lock`과 `Condition`은 자바에서 동기화와 스레드 간 협력을 더욱 세밀하게 제어할 수 있는 기능을 제공합니다. 이는 기존의 `synchronized`와 `wait/notify/notifyAll` 메서드에서 제공하는 객체 모니터 기반 동기화를 **더 발전된 형태로 대체**하기 위해 Java 5에서 `java.util.concurrent.locks` 패키지에 추가되었습니다.

---

## **Lock과 Condition의 차별점**

### 1. **Lock (ReentrantLock)**
`Lock`은 `synchronized` 블록/메서드의 대안으로, 동기화의 유연성과 기능성을 증가시킵니다.

- `ReentrantLock`은 `synchronized`와 유사한 방식으로 작동하지만, 추가적인 기능을 제공합니다:
  - **정확한 락 해제**: 락을 명시적으로 해제해야 하므로 더 많은 제어권을 가집니다.
  - **락 상태 확인**: 락이 사용 중인지 확인하거나, 시도 후 실패하는 락 획득 (`tryLock`) 가능.
  - **공정성 제어**: 락을 먼저 요청한 스레드가 우선권을 갖도록 설정 가능 (Fair Lock).

#### 사용 예제
```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class LockExample {
    private final Lock lock = new ReentrantLock();

    public void criticalSection() {
        lock.lock(); // 락 획득
        try {
            System.out.println(Thread.currentThread().getName() + " is executing.");
            Thread.sleep(1000); // 작업 시뮬레이션
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
            lock.unlock(); // 락 해제
        }
    }

    public static void main(String[] args) {
        LockExample example = new LockExample();

        Thread t1 = new Thread(example::criticalSection, "Thread 1");
        Thread t2 = new Thread(example::criticalSection, "Thread 2");

        t1.start();
        t2.start();
    }
}
```

#### 출력 예시
```
Thread 1 is executing.
Thread 2 is executing.
```

---

### 2. **Condition**
`Condition`은 `Object` 클래스의 `wait/notify/notifyAll` 메서드의 발전된 형태로, `Lock` 객체와 함께 사용됩니다.

- **대기 큐 분리**: 객체 모니터는 하나의 대기 큐만 제공하지만, `Condition`은 여러 대기 큐를 사용할 수 있어 더 세밀한 스레드 간 협력 제어가 가능합니다.
- **명시적 제어**: 특정 조건에서만 스레드를 깨우거나 기다리게 할 수 있습니다.

#### 주요 메서드
- `await()`: 현재 스레드를 대기 상태로 전환하며, 락을 해제합니다.
- `signal()`: 대기 중인 스레드 하나를 깨웁니다.
- `signalAll()`: 대기 중인 모든 스레드를 깨웁니다.

#### 사용 예제
```java
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class ConditionExample {
    private final Lock lock = new ReentrantLock();
    private final Condition condition = lock.newCondition();
    private boolean ready = false;

    public void produce() {
        lock.lock();
        try {
            System.out.println("Producer: Producing data...");
            Thread.sleep(1000); // 데이터 생성
            ready = true;
            System.out.println("Producer: Data ready, notifying consumer.");
            condition.signal(); // 소비자에게 알림
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    public void consume() {
        lock.lock();
        try {
            while (!ready) { // 데이터 준비 여부 확인
                System.out.println("Consumer: Waiting for data...");
                condition.await(); // 대기
            }
            System.out.println("Consumer: Consuming data...");
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    public static void main(String[] args) {
        ConditionExample example = new ConditionExample();

        Thread producer = new Thread(example::produce, "Producer");
        Thread consumer = new Thread(example::consume, "Consumer");

        consumer.start();
        producer.start();
    }
}
```

#### 출력 예시
```
Consumer: Waiting for data...
Producer: Producing data...
Producer: Data ready, notifying consumer.
Consumer: Consuming data...
```

---

## **Lock & Condition vs synchronized & wait/notify**

| **기능**                | **synchronized & wait/notify**               | **Lock & Condition**                          |
|--------------------------|---------------------------------------------|-----------------------------------------------|
| **동기화 제어**          | 암묵적으로 JVM이 관리                        | 명시적으로 프로그래머가 제어                   |
| **락 해제 제어**         | 자동 해제                                   | 반드시 명시적으로 해제해야 함                 |
| **공정성 옵션**          | 지원하지 않음                                | 공정한 락(Fair Lock) 사용 가능                 |
| **대기 큐**              | 하나의 큐                                   | 여러 `Condition` 객체로 큐 분리 가능           |
| **성능**                | 단순하고 기본적인 환경에서 빠름              | 복잡한 환경에서 더 유연하고 효율적            |

---

## **요약**
- `Lock`은 동기화 블록보다 더 세밀한 제어와 기능을 제공합니다.
- `Condition`은 여러 대기 큐를 활용하여 스레드 간 협력을 정밀하게 조율합니다.
- 복잡한 멀티스레드 환경에서는 `Lock`과 `Condition`이 더 적합하며, 간단한 경우에는 기존 `synchronized`를 사용하는 것이 좋습니다.

