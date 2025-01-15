
## User:
자바 네이티브 메서드가 뭐야

## Assistant:
자바 네이티브 메서드(Native Method)는 자바 코드에서 호출할 수 있는, 자바가 아닌 다른 프로그래밍 언어로 작성된 메서드를 의미합니다. 주로 C나 C++로 작성된 코드가 네이티브 메서드로 사용됩니다.

### 주요 특징:
1. **JNI (Java Native Interface)**: 네이티브 메서드는 Java Native Interface (JNI)를 통해 자바와 다른 프로그래밍 언어(C, C++ 등) 간의 상호작용을 가능하게 합니다. 이를 통해 자바 프로그램이 C나 C++로 작성된 기능을 호출할 수 있습니다.
   
2. **성능 최적화**: 자바는 플랫폼에 독립적인 언어로, 일반적으로 성능이 상대적으로 떨어질 수 있습니다. 하지만 성능이 중요한 부분에서는 네이티브 메서드를 사용하여 자바 외부의 빠른 코드나 하드웨어 자원에 접근할 수 있습니다.

3. **하드웨어 접근**: 자바는 일반적으로 하드웨어와의 직접적인 상호작용을 제공하지 않지만, 네이티브 메서드를 사용하면 하드웨어에 접근하거나 OS의 기능을 호출할 수 있습니다.

4. **호출 방식**: 네이티브 메서드는 자바에서 `native` 키워드를 사용하여 선언합니다. 이 메서드는 실제로는 자바 외부에서 정의되며, 자바 코드에서 호출할 수 있게 됩니다.

### 예시 코드

자바에서 네이티브 메서드를 선언하는 방법은 다음과 같습니다.

```java
public class Example {
    // 네이티브 메서드 선언
    public native void exampleMethod();
    
    static {
        // 자바가 실행될 때 네이티브 라이브러리 로드
        System.loadLibrary("exampleLib");
    }

    public static void main(String[] args) {
        Example obj = new Example();
        obj.exampleMethod();  // 네이티브 메서드 호출
    }
}
```

위 예제에서 `exampleMethod`는 네이티브 메서드로 선언되었고, 이 메서드는 C나 C++로 구현되어야 합니다. `System.loadLibrary("exampleLib")`는 `exampleLib`라는 네이티브 라이브러리를 로드하는 코드입니다.

### 네이티브 메서드의 구현 (C 예시)

```c
#include <jni.h>
#include <stdio.h>
#include "Example.h"  // 자바 클래스 헤더 파일

// 네이티브 메서드 구현
JNIEXPORT void JNICALL Java_Example_exampleMethod(JNIEnv *env, jobject obj) {
    printf("Hello from native code!
");
}
```

### 요약:
- 자바 네이티브 메서드는 자바 외의 언어로 작성된 메서드를 자바 코드에서 호출할 수 있도록 합니다.
- JNI를 통해 자바와 다른 언어 간의 상호작용을 가능하게 하며, 성능 최적화나 하드웨어 접근 등 다양한 용도로 사용됩니다.
