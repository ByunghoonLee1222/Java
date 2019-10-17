# Spring

엔터프라이즈 어플리케이션에서 필요로 하는 기능을 제공하는 프레임 워크

```
public class ArticleFactory{
	public static ArticleDao getInstance(){
		return new MysqlArticleDao();
	}
}

publci class XXXServiceImp{
	ArticleDao dao = ArticleFactory.getInstance();
}
```



### 주요 기능 및 특징

#### DI (Dependency Injection)

---

의존하는 객체(속성)를 직접 생성하지 않고 생성자나 setter메서드를 통해서 주입 받기

> 의존? 클래스 내에있는 함수나 속성이 아닌 다른 클래스의 함수나 속성을 사용
>
> * 상속, 속성, 인자로 다른 클래스를 사용



#### IoC (Inversion of Control)

---

사용하는 객체를 생성의 Controll을 직접수행하지 않고 전달 받아 사용한다

* IOC Container
  * 사용할 객체들을 미리 생성해서 관리하는 객체



#### AOP (Aspect-Oriented Programming)

---

공통의 관심 사항을 적용해서 발생하는 의존 관계의 복잡성과 코드 중복을 해소해 주는 프로그래밍 기법

* Aspect를 이용하여 핵심 로직으 ㄹ구현한 각 클래스에 공통 기능을 적용



#### 스프링 컨테이너

* **BeanFactory**
  * 빈 객체를 관리하고 각 빈 객체 간의 의존 관계를 설정해주는 기능을 제공
* **ApplicationContext**
  * 파일과 같은 자원처리 추상화
  * 메세지 지원 및 국제화 지원
  * 이벤트 지원
* **WebApplicationContext**
  * 웹 어플리케이션을 위해 추가적으로 제공되는 빈 영역(bean scope)을 정의
  * 하나의 웹 어플리케이션 마다 한개의 WebApplicationContext가 존재



#### Spring Legacy Project

---

* src/main/java  => source code
* src/main/resources => Xml, 이미지,...
* src/test/java => test

**Library**

* pom.xml => Libarary 추가 (dependency) 자동 다운(Mavenrepository)

* 스프링 핵심 라이브러리
  * spring-beans
  * spring-core
* Maven Dependencies



**bean**

---

```xml
1. 기본생성자로 객체 생성하도록 bean 등록하기
			id 
			- bean을 구별하는 이름 (동일한 이름이 있으면 error)
			- 한개만 설정할 수 있다
			
			name
			- bean을 구별하는 이름(동일한 이름이 있으면 error)
			- 공백으로 구별해서 여러개의 이름을 설정 할 수 있다
			
			class
			- 컨테이너가 생성할 객체의 클래스명(패키지를 포함한 클래스명을 쓴다)

			scope
		 	- 객체 사용 범위 지정
		 	- singleton
		 		- 한번 생성된 객체를 getBean(~)할 때마다 전달 => container가 
		 		  종료될 때까지 같은 객체를 공유해서 사용
		 	- prototype
		 		- getBean(~)할때 마다 객체를 생성
		 	- request : web환경에서 새로운 요청에서 getBean(~)할때 마다 객체를 생성
		 	- session : web환경에서 새로운 session에서 getBean(~)할때 마다 객체를 생성
		 				=> 같은 session에서는 공유
		 	lazy-init 
		 	- scope이 singleton인 경우 lazy-init의 속성에 따라 객체 생성 시점을 결정할 수 있다.
		 	- false : Container가 생성될 때 객체가 생성된다.
		 	- true  : 처음 getBean(~)할 때 한번 객체가 생성된다.

	<bean id='board' 	class="com.ssafy.model.dto.Board" lazy-init="true"/>
	<bean id='board2' 	class="com.ssafy.model.dto.Board"	scope="prototype" init-method="test"/>
```

* 기본 생성자가 있다
* encapsulation되어 있는 속성들
* 속성에 대한 getter, setter가 있어햐 한다

```java
	public static void main(String[] args) {
		
		/*Spring Container 생성*/
		
		BeanFactory container = new ClassPathXmlApplicationContext("com/ssafy/config/beans1.xml");
		System.out.println("Spring Container loading 완료.....");
		
		/* getBean(String name)
		 * - name이나 id에 해당하는 객체를 container에서 추출
		 * - 형변환을 해야 한다(Object 리턴)
		 * */
		
		Board board = (Board)container.getBean("board");
		
		/* getBean(Class cls)
		 * - 지정한 클래스 타입과 동일한 객체를 container에서 추출
		 * - 형변환이 필요 없음
		 * - container에 동일한 타입의 객체가 2개 이상 등록된 경우 error 발생
		 * */
		Board board = container.getBean(Board.class);
		
		/* getBean(String name,Class cls)
		 * - name이나 id에 해당하는 객체를 container에서 추출
		 * - 형변환이 필요 없음
		 * 
		 * */
		Board board = container.getBean("board",Board.class);
		System.out.println(board);
	}
```

