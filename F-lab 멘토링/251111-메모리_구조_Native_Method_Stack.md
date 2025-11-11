# 자바 메모리 구조

## Native Method Stack

### Native Method Stack의 개념

- 자바가 아닌 Native Method를 실행할 때 사용하는 스택 영역이다
- 자바는 기본적으로 JVM 위에서 돌아가지만 때로는 OS나 하드웨어 자원에 직접 접근해야 할 때가 있다
- 이럴 때 JNI(Java Native Interface)를 통해 C나 C++로 작성된 함수를 호출할 수 있는데, 이 함수들이 Native Method이다
- 예시
    ```java
        public class Example {
            public native void printHello(); // native 키워드
            static {
                System.loadLibrary("nativeLib"); // C/C++ 라이브러리 로드
            }
        }
    ```
    - 이때 `printHello()` 같은 네이티브 메서드를 실행하면, JVM은 자바 스택이 아니라 Native Method Stack을 사용해서 호출 스택을 관리한다

### 내부 구조

- 자바의 스택과 유사하게 스택 프레임 구조를 갖지만, 내용물은 자바 바이트코드가 아니라 C/C++ 함수의 실행 컨텍스트이다
- 즉, 각 스레드마다 다음 두 개의 스택이 따로 존재한다
    - Java Stack -> 자바 메서드용
    - Native Method Stack -> 네이티브(C/C++) 메서드용
- 스레드가 네이티브 함수를 호충하면 그 시점에서 JVM은 Java Stack에서 Native Stack으로 제어를 넘기고, 해당 함수가 끝나면 다시 Java Stack으로 돌아간다

### Native Method Stack 동작 과정

- 전체 흐름
     - `Java Method -> JVM -> JNI -> Native Library -> JVM 복귀`
     - 이때 Java Stack은 자바 코드 실행용, Native Method Stack은 C/C++ 함수 실행용