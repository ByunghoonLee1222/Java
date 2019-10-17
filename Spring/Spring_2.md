# Spring_2

**bean 설정**

```xml
<bean id='boardDao' class="com.ssafy.model.dao.BoardDaoImpl"/>
	<bean id='memberDao' class="com.ssafy.model.dao.MemberDAOImp"/>
	
	<bean id='boardService' class="com.ssafy.model.service.BoardServiceImpl">
		<constructor-arg	ref="boardDao"/>
	</bean>
	
	<bean id='memberService' class="com.ssafy.model.service.MemberServiceImp">
		<property name="dao"	ref='memberDao'/>
	</bean>

<!-- autowire : 의존 객체를 자동 주입 
		 
		 byType   
		 	- 속성의 타입과 동일한 객체를 자동 주입
		 	- 기본 생성자로 생성해서 setter메서드로 주입
		 	- 동일한 타입으로 객체가 2개 이상 등록되어 있는 경우 error 발생 
		 
		 constructor
		 	- 생성자에 인자 타입과 동일한 객체를 자동 주입
		 	- 동일한 타입으로 객체가 2개 이상 등록되어 있는 경우 spring version마다 틀림
		 
		 byName
		 	- 동일한 타입으로 객체가 2개 이상 등록되어 있는 경우
		 	속성의 이름과 bean에 설정된 id 또는 name이 같으면 자동 주입됨
	-->
	<bean id='boardService' class="com.ssafy.model.service.BoardServiceImpl"
		autowire="constructor">
	</bean>
	
	<bean id='memberService' class="com.ssafy.model.service.MemberServiceImp"
		autowire="byType">
	</bean>
```

