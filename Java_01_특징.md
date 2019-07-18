# Java

* network에 강하다
* 임베디드시스템에 쉽게 포팅하기위해 개발
  * 임베디드시스템에 JVM을 설치
  * JVM을 통해 Java실행

### 메모리 관리

1. PC Register
2. Native Stacks ( C, C# )
3. ***Java Stacks***
4. ***Heap***
5. ***Method Area ( c = class Area)***

***JVM 명령코드 - class(byte code)***

* JVM이 OS에 맞는 코드로 interpreting을 한다.
* interpreting 속도가 느려 git code 개발
* 한번 interpreting 되면 binary code를 git code에 저장 - (재실행시 속도 향상)



### Java 특징

1. 객체지향 - **유지보수에 용이**(구조적 언어는 유지보수가 힘들다)
2. 플랫폼에 **독립적** - *but,* HW에 **JVM 필수**로 설치
3. **자동 메모리 관리** - garbage collector
4. 포인터를 쓰지 않는다.
5. Java는기본으로 **동적**이다. (C++ 은 기본이 정적)
   * 클래스 로딩, 메모리 할당 , 메소드 binding(lingking)을 동적으로
   * Type은 정적
   * 변화에 용이하기 위해 동적으로 로딩
   * 정적으로 사용하고 싶을때만 Static
   * 실행중에 로딩가능 (Reflection)
6. **멀티 쓰레드** 지원
   * 기존은 Process 복제(fork)
   * 따라서, 메모리 사용 증가 ,성능 저하
   * Java는 멀티쓰레드 기능으로 성능 향상

7. Stack(Thread 당 1개)
   * local 변수, this
8. Code Verify (In JVM)
   * 보안을 위해 장치접근 불가, Exception( 허가를 받아야 한다.)
   * 그외에 여러 규칙들 유효성 검사 후 Process에 Verification 호출 

### 객체 생성 과정

1. 객체 생성 시 reference Type 4byte 생성
2. Method Area에 클래스 생성
3. Heap영역에 메모리 할당 (Hash code 생성)
4. Hash code를 통해 객체를 참조한다(참조값)

> ***Hash code 란?*** - 특정한 메모리에 빠르게 접근하기 위한 code(실제주소 x)



### Java 단축키

* |          기능           |        단축키         |
  | :---------------------: | :-------------------: |
  |   소스코드 화면 확대    |       Ctrl + M        |
  |      소스코드 확인      |      Ctrl + 클릭      |
  |        코드 이동        |     Alt + 방향키      |
  | 한줄 아래 복사, 위 복사 | Ctrl + Alt + Down, Up |
  |        한줄 삭제        |       Ctrl + D        |
  |         import          |   Ctrl + Shift + O    |
  |        코드 이동        |     Alt + 방향키      |
  |      코드 Generate      |     Ctrl + Space      |
  |        코드 정리        |   Ctrl + Shift + F    |

### Code

* **ASCII**
  * 영어 대,소 문자, 숫자, 특수기호 128개를 0 ~ 127까지 부여
* **ISO-8859-1**
  * ASCII를 확장(몇가지 특수기호 추가)하여 1byte로 코드화(국제 표준)
* **유니코드**
  * 전세계 언어를 코드화
    * UTF-8(bit) : 영어 대,소 문자, 숫자, 특수기호만
    * UTF-16 : (2byte로 전세계 언어를 코드화)
    * UTF-24 : 중국어..

