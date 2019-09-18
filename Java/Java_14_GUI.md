# GUI

* AWT : O/S 마다 UI 다른 모습
* SWING : O/S 마다 U/I 같은모습 , 다양한 UI 컴포넌트 지원

#### UI 설계(스케치)

* 요구사항 분석
* 설계
* 구현
* 테스트

#### Component

---

* 추상 클래스
* 각각 독립된 모듈

##### Container

* 컴포넌트를 효율적으로 배치할 수 있도록 해주는 영역

* 화면의 파티션 지정

* **Frame**
  * 독립접으로 띄워질 수 있는 창(책상 서랍)
* **Panel**
  * 독립적으로 실행된 창 안에서 파티션을 도와주는 역할

##### LayoutManager (배치 관리자)

* **BorderLayout(크기 가변, 위치 고정)**

  * 5개의 영역 - 한 영역에 한개의 Component
  * North, South, Center, West, East
  * 안쓰는 영역은 공간 차지 X
  * **frame의 default Layout**

* **FlowLayout( 크기 고정 , 위치 가변)**

  * 가로 배치 
  * 왼쪽에서 오른쪽으로 다차면 개행
  * Component의 제한이 없다
  * **Panel의 default Layout**

* **GridLayout(크기 가변, 위치 고정)**

  * 동일한 사이즈로 영역 분할 

  * 각 영역을 Component로 채운다

  * 특정 위치 지정 못함 Flow같은 배치

    

#### Event

---

* **Event**
  * 발생한 사건 정보
* **Event Source**
  * Event 발생한 근원지(대상)
* **EventHandler**
  * Event 처리기(catch와 비슷)
  * 해당 Event에 등록을 해줘야 한다
  * 한 component에 여러가지 Handler 등록 가능

callback Method

JVM 이 이벤트가 발생할 때 자동으로 부르는 메서드(Handler)