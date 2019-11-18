# Spring AOP(Aspect Oriented Program)

관점 지향 프로그래밍 - 핵심 관점, 부가적인 관점으로 나누어 보고 관점을 기준으로 각각 모듈화



#### AOP 주요 개념

---

* **Aspect** : 공통코드 / 모듈화 한 것
* **Target** : Aspect를 적용하는 곳(클래스, 메서드..)
* **Advice** 
  * 실질적으로 어떤 일을 해야할지에 대한 것 , 실질적인 부가기능을 담은 구현체
  * Aspect(공통모듈)를 수행할 시점
* **JointPoint** 
  * Advice가 적용될 위치, 메서드 진입 지점, 생성자 호출 시점 등 다양한 시점에 적용
  * 메서드 이름 , 인자, 리턴 값
* **PointCut** : Aspectj 표현식으로 핵심모듈을 찾기 ex) execution()



#### @AOP 추가

```xml
<dependency>    
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
</dependency>
```

|                |     첫번째 인자      |             두번째 인자             |                    리턴                     |
| :------------: | :------------------: | :---------------------------------: | :-----------------------------------------: |
|     Before     |      JointPoint      |                  x                  |                      x                      |
|     After      |      JointPoint      |                  x                  |                      x                      |
| AfterReturning |      JointPoint      |   Object(핵심모듈을 수행한 결과)    |                      x                      |
| AfterThrowing  |      JointPoint      | Throwable(핵심모듈에서 발생한 오류) |                      x                      |
|     Around     | ProceedingJointPoint |                  x                  | Object(핵심모듈을 수행한 결과 or Exception) |



* aop:advisor => spring tx