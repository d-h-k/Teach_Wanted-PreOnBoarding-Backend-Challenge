# Precourse

# 원티드 프리온보딩 백엔드 챌린지 6월 과정 사전 과제 제출

## Question
**Java 입문서('이것이 자바다', '자바의 정석' 등)를 완독한 적이 있나요? 기억에 남는 내용을 설명해 주세요!**
- 자바의 신(이상민 님 저) 책 좋아합니다
- 기억에 남는 구절들
```
## static 메소드와 일반 메소드의 차이 & static 블록

## 상속에서의 Polymorphism

## Object 클래스의 equals(), hashCode(), toString()  메서드

## interface 와 abstract class 

## try-catch-resource 문

## Throwable 클래스

## String class 의 immutable 과 이것을 보완하기 위한 StringBuffer와 StringBuilder

## Nested 클래스

## Static nested 클래스

## JVM 관련
- JIT 컴파일러
- HotSpot
- GC 

## 제네릭 톺아보기

## FILE I/O
- File 클래스
- InputStream & OutputStream
- Reader & Writer
- NIO & Buffer
- NIO2
- WatchService 클래스

## Serializable 과 transient 키워드

## 쓰레드& 프로세스 관련
- Fork & Join 클래스

## 잡다한데 잘 모르는거
- classpath
- Formatter
- ThreadLocal

## JDK 17버전 변경사항

```

**Java 공식 문서를 10분 이상 살펴본 적이 있나요? 있다면 어떤 내용을 살펴보셨나요?**
> 

**인터프리터 방식과 컴파일 방식의 차이점을 서술해 주세요.**
```
- 인터프리터 : 한줄한줄 읽어서 실행하는 스크립트에서 한줄한줄을 해석해서 실행해주는 방식
- 컴파일 : 실행 전에 소스코드 전체를 컴퓨터가 알수 있게 번역하는 방식
```

**프로세스와 스레드의 차이점을 서술해 주세요.**
```
- 프로세스 : 운영체제에서 실행 중인 프로그램
- 스레드 : 프로세스에서 실행되는 실행의 단위, 프로세스와 자원(공간/메모리 과 시간/CPU)을 공유함
```

**JVM의 정의와 메모리 구조를 아는 대로 서술해 주세요.**
```
[JVM]
- Java 실행환경. OS 구분없이 같은 Java Code 가 동작하게 해줌
- 메타포로 Java>WebApp , JVM>웹브라우저
[JVM 구성요소]
- Class Loader : Java 클래스를 JVM으로 로딩해줌
- Execution Engine : bytecode instructions 실행기 = JIT compilation + interpretation
- Native Method Interface : C/C++ 같은 네이티브 코드와의 상호작용 + 컴퓨터 시스템 리소스 엑세스
[메모리구조]
- 네이티브 메서드 스택
- ProgramCounter 레지스터
- 스택 공간 : 메서드 호출정보 , 로컬 변수
- 힙 공간 : Object 생성, 모든 스레드가 공유함, JVM 관리 대상 영역
- 메서드 공간 : 바이트 코드, 상수 풀, 필드 및 메서드 참조, static 변수와 같은 클래스 수준 데이터
```

**Java의 GC 알고리즘 중 하나만 선택해 아는 대로 서술해 주세요.**

```
[commonly GC / generational GC]
1) 새로 생성되는 객체가 할당되는 공간(Eden) 에서 메모리를 쓴다
2) Eden 공간이 가득차면 "tinyGC" 로직이 돌면서 Eden 공간을 정리
3) 살아있는 객체(live Object)들은 (S0 / S1) 으로 이동, 여기서 살아있음은 포인터가 유지되고 있는지 여부로 판단
4) 수명이 긴 객체들은  Old-Generation 공간에 위치
5) 메모리 공간 전체가 많이 사용되는 경우 모든공간 ( Old-Generation + S0/S1 + Eden) 을 싹 다 돌면서 메모리를 청소하는데 이를 Full-GC 라고 합니다


[G1/Garbage-First GC 알고리즘]
- Region 개념을 도입해서 Heap 공간을 짤라서 Region 으로 나눠서 관리
- Garbage 가 많은 Region 을 우선적으로 청소해줌
- Heap 공간이 크면클수록, 그러니까 JVM 메모리를 많이 먹는 App 일수록 이 알고리즘이 유리

[CMS(Concurrent Mark Sweep) GC 알고리즘]
- Marking 과 Sweeping 을 동시에 진행하는 GC 알고리즘 
- GC 에 의한 일시정지 현상을 최소화하기 위해 만들어졌음
- 단점으로 CPU 사용량이 높아질수 있지만, 장점으로 전체적으로 빠른 응답속도를 내줌

[Z GC 알고리즘]
- G1 GC 랑 비슷한거같은데 더 빡센거같음.. 잘모름

[GC 가 효율적으로 동작하기 위한 기법들]
- Marking : 어떤 객체가 사용되는지, 더이상 사용되지 않는 객체가 있는지 식별하는 기법
- Compaction : Marking 후 memory fragmentation 줄이기 위해서 live Object 들을 재정렬해서 객체 사이의 거리를 가깝게 함. 일종의 조각모음
- Sweeping : Marking 후 참조되지 않는 객체들은 메모리 할당 해제. 
- Concurrent and Parallel GC : 위 과정들을 동시에 병렬로 처리해서 성능을 최적화 함
```


**세마포어에 대해서 아는 대로 서술해 주세요.**
```
세마포어는 공유자원에 대한 접근을 제한하는데, 접근가능한 스레드의 갯수를 제어
뮤텍스는 공유자원에 대한 상호배제, 딱 하나의 쓰레드만 접근 가능
```

**Java의 `synchronized`에 대해서 아는 대로 서술해 주세요.**
```
synchronized 키워드는 스레드간의 동기화를 제공하는 키워드 입니다
[장점]
여러 스레드가 공유된 자원에 동시에 접근할 때 발생할 수 있는 동시성 문제를 해결해줌 (대신 성능이 떨어짐)
[단점]
성능이 떨어짐(대신 동시성 문제가 해결됨)
[특징]
synchronized 키워드를 붙이면 블록/메서드 단위로 상호 배제 (Mutual Exclusion) 해주는데요, 다른 스레드가 접근하려고 할 때 대기하게 되며, 접근이 완료되면 다음 스레드가 접근할 수 있습니다.
[사족]
print 열어보면 들어있는데, 아마 synchronized 때문에 webApp 에서는 print 를 사용하지 말라고 하는거같습니다.
AtomicInt, AtomicLong 같은걸 최대한 활용하고 synchronized 는 안쓰려고 노력하고 있습니다.
```


**강의 커리큘럼과 관련하여 기대하는 내용이나 다뤘으면 하는 내용이 있나요?**
> 리딩해주시는거 잘 따라가겠습니다

**회사 생활 또는 개발자로서 고민과 질문, 강의에서 바라는 점 등 하고 싶은 말씀을 편하게 남겨주세요!**
> 바라는점 질문은 조금더 생각해봐야할꺼같습니다. 회사생활에 고민은 많고 개발자로써의 고민은 없음.
