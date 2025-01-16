# 자바 객체 모니터 (Java Object Monitor)

## 질문
자바 객체 모니터에 대해서 설명해줘요

## 답변

자바에서 "객체 모니터(object monitor)"는 동기화(synchronization)와 관련된 개념으로, 특정 객체가 **스레드 간의 상호작용**을 조율하는 역할을 합니다. 이는 주로 멀티스레드 환경에서 데이터 일관성을 보장하거나, 스레드 간의 협력을 가능하게 만들기 위해 사용됩니다.

### 객체 모니터의 역할
자바에서 모든 객체는 **모니터 락(monitor lock)**이라는 고유한 잠금을 가지고 있습니다. 이 잠금을 사용하여 스레드 간에 자원에 대한 **동기화 접근**을 제어할 수 있습니다.

1. **동기화된 메서드나 블록 실행 제어**
   - `synchronized` 키워드를 사용하면 해당 코드 블록이나 메서드를 실행하기 위해 객체의 모니터 락을 확보해야 합니다.
   - 한 스레드가 모니터를 소유하고 있으면 다른 스레드는 락이 해제될 때까지 대기합니다.

2. **wait/notify/notifyAll 메서드 지원**
   - 자바의 `Object` 클래스에는 스레드 간 통신을 위해 `wait`, `notify`, `notifyAll` 메서드가 있습니다. 이 메서드들은 객체의 모니터와 함께 작동합니다.
   - `wait`: 스레드가 모니터 락을 풀고 대기 상태로 전환.
   - `notify`: 대기 중인 스레드 중 하나를 깨움.
   - `notifyAll`: 대기 중인 모든 스레드를 깨움.

---

### 객체 모니터의 동작 방식
1. **모니터 락 획득**
   - 스레드가 `synchronized` 메서드나 블록에 진입하려면 먼저 객체의 모니터 락을 얻어야 합니다.
   - 락이 이미 다른 스레드에 의해 소유 중이라면, 현재 스레드는 대기 상태로 전환됩니다.

2. **코드 실행**
   - 모니터 락을 얻은 스레드는 `synchronized`로 지정된 코드 블록이나 메서드를 실행할 수 있습니다.

3. **락 해제**
   - 스레드가 `synchronized` 블록이나 메서드를 종료하면, 객체의 모니터 락이 자동으로 해제됩니다.
   - 그 다음에 대기 중인 다른 스레드가 락을 얻을 수 있습니다.

---

### 코드 예제

```java
class SharedResource {
    public void synchronizedMethod() {
        synchronized (this) {
            System.out.println(Thread.currentThread().getName() + " is executing.");
            try {
                Thread.sleep(1000); // 작업 시뮬레이션
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(Thread.currentThread().getName() + " is done.");
        }
    }
}

public class MonitorExample {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();

        Thread t1 = new Thread(() -> resource.synchronizedMethod(), "Thread 1");
        Thread t2 = new Thread(() -> resource.synchronizedMethod(), "Thread 2");

        t1.start();
        t2.start();
    }
}
```

#### 실행 결과
```
Thread 1 is executing.
Thread 1 is done.
Thread 2 is executing.
Thread 2 is done.
```

- `synchronized (this)`로 인해 `Thread 1`이 작업을 끝낼 때까지 `Thread 2`는 기다립니다.

---

### 요약
- 자바 객체 모니터는 동기화와 스레드 간 협력을 지원하기 위해 존재합니다.
- `synchronized` 키워드와 `wait/notify` 메서드는 모니터 메커니즘에 기반을 둡니다.
- 모니터를 활용하면 멀티스레드 환경에서 자원에 대한 안전한 접근과 스레드 간 통신을 구현할 수 있습니다.


