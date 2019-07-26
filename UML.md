# UML

#### 요구사항분석 -> 설계 -> 구현 -> 테스트

---

* Activity Diagram => 순서도
* Sequence Diagram => 시간의 흐름
* Usecase Diagram => 시스템에 어떤 기능이 있는지 표시
* Class Diagram => 클래스의 구조 , 관계



#### 선종류

---

* Dependency
* Association
* Generalization
* Realization - 실제 구현하는 관계
* Aggregation
* Composite



#### 관계

---

* is a(상속, 일반화)

  * Generalization - 실선 화살표

* has a (소유)

  * Association

    * Aggregation(집합연관) - 흰 마름모 실선

    

    * Composition(복합연관(**강한 집합연관**)) - 검정 마름모 실선
      * 한부분이 한집합에만 속해야 한다.

* use a (사용)

  * Dependency - 점선 화살표