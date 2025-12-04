# JDK, JRE, JVM

## 전체 개념 요약

- JVM
    - 자바 프로그램을 실행하는 가상 머신
    - 바이트코드를 해석/컴파일/메모리 관리 하는 엔진
- JRE
    - JVM이 실행될 수 있는 환경
    - JVM + 표준 라이브러리
- JDK
    - 자바 개발용 도구 세트
    - JRE + 개발 도구 (javac 컴파일러, 디버거, javadoc 등)

즉 다음의 관계를 가진다 
```java
JDK = JRE + 개발 도구들
JRE = JVM + 표준 라이브러리
JVM = 자바 실행 엔진
```
## JVM (Java Virtual Machine)

Write Once, Run Anywhere를 가능케 하는 실제 주체

### JVM의 역할 

- JVM의 역할
    1. 바이트코드(.class) 실행
        - javac가 만든 .class 파일을 로딩해 실행한다
    2. 런타임 메모리 관리
        - Heap, Stack, Metaspace 관리
    3. GC
        - 사용하지 않는 객체 자동 해제
    4. JIT 컴파일
        - 반복되는 바이트코드를 네이티브 코드로 컴파일하여 속도 향상
    5. 스레드 관리
        - OS 스레드를 기반으로 자바 스레드를 관리
    6. 예외 처리 및 보안 모델 적용

### JVM의 특징

- 플랫폼 독립적 (.class는 OS와 무관)
- JIT 최적화로 실행 속도가 향상됨
- GC 덕분에 개발자는 메모리 해제 걱정을 크게 줄임
- HotSpot JVM, OpenJ9 등 다양한 JVM 구현체가 존재

## JRE (Java Runtime Environment)

JVM만 있으면 프로그램을 실행할 수 없기 때문에 필요한 실행 환경

### JRE 구성 요소

1. JVM
    - 바이트코드를 실제 실행하는 엔진
2. 자바 표준 라이브러리(Java Class Library)
    - java.lang., java.util., java.io.* 등
    - JDK 8까지는 rt.jar 형태
3. 기타 리소스 파일

### JRE 역할

- 자바 애플리케이션 실행 환경 제공
- 컴파일은 못함(컴파일러가 없음)

### JRE 특징

- 배포용(사용자용)
- 개발자는 설치될 필요가 거의 없다 (JDK가 JRE 포함하기 때문)

## JDK (Java Development Kit)

자바 개발자가 사용하는 개발 도구 모음 + 실행 환경(JRE)

### JDK 구성 요소

1. JRE
    - JVM + 표준 라이브러리
2. 개발 도구
    - javac: 자바 소스(.java) → 바이트코드(.class) 컴파일
    - java: 바이트코드 실행 명령
    - javadoc: 문서 생성 도구
    - jdb: 디버거
    - jar: 압축/배포 도구
    - javap: 바이트코드 역어셈블러

### JDK 특징

- 개발자용
- JRE를 포함한다
- JDK 8 이후부터는 JRE 단독 배포가 줄어들고 JDK만 설치하는 추세

## 한 줄 정리

JDK, JRE, JVM의 차이점은?
- JVM은 자바 바이트코드를 실행하는 가상 머신이고, JRE는 JVM이 실행될 수 있도록 표준 라이브러리와 리소스를 포함한 실행 환경입니다. JDK는 JRE에 컴파일러(javac)와 각종 개발 도구를 포함한 개발 키트입니다. 즉 개발 시에는 JDK, 실행만 한다면 JRE만 필요하며 JVM은 실제 실행 엔진입니다.