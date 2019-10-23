# Spring di



#### di 란?

---

* dependency injection
* dependency ?
  * 목적 : 의존 관계의 제거, 내 코드에서 객체를 만들지 않고 프레임워크가 넣어주는 객체를 사용하자
  * 객체 : 상태를 갖지 않는 stateless 한 bean을 대상 / singleton design pattern
  * 빈 주입 방법 : 생성자, setter
  * DI 방법
    * xml				:  3rd party의 객체
    * annotation   : 소스에 대한 편집 필요 : 소스를 가지고 있는 녀석
    * java config    : 3rd party의 객체



#### spring application

---

* POJO(빈) + 메타 정보( 설명서 - xml, annotation, java config) + 스프링 프레임워크

**bean 설정**

* `<bean id="iMan" class="com.ssafy.heroes.IronMan">`

**bean 값 주입**

* `<constructor-arg value="">` : 생성자를 통한 주입
  * ref : 참조할 때
  * value : scalar 값을 직접 넣을때
* `<property name="" ref="">` : setter를 통한 주입

**bean 값 조회**

* ```java
  ApplicationContext ctx = new ClassPathXmlApplicationContext("application.xml");
  
  public void testBean() {
  		// 기본적으로 타입 기반의 빈 조회
  		HulkBuster hb = ctx.getBean(HulkBuster.class);
  		assertThat(hb, is(notNullValue()));
  		// 동일 타입의 빈이 2개 이상일 경우 이름을 부가적으로 사용 (상속 클래스면 타입 중복)
  		IronMan iman = ctx.getBean("iMan",IronMan.class);
  		assertThat(iman, is(notNullValue()));
  		
  		Avengers avengers = ctx.getBean(Avengers.class);
  		assertThat(avengers, is(notNullValue()));
  		// spring은 모든 빈을 singleton으로 관리해준다!!
  		assertThat(hb, is(avengers.getHb()));
  	}
  ```



#### annotation 기반 di

---

* component-scan : component = bean
  * 용도에 맞는 스테레오 타입 사용
    * @Component	: 아래에 해당하지 않는 경우
    * @Repository      : Repository 즉 sql 처리 객체(DAO)
    * @Service            : Service 계열 : transaction 처리
    * @Controller       : 웹 서비스를 처리하는 컨트롤러
    * @Configuration : Java 기반의 설정 시

* @Autowired : 타입 기반으로 빈을 주입할 때

* @Qualifier : 이름 기반으로 빈을 찾아야 할때

* @Value : 기본형 , 문자열 등 scalar 값을 주입할 때

* ```xml
  <!--xml component scan-->
  <context:component-scan base-package="com.ssafy.heroes"></context:component-scan>
  <context:property-placeholder location="classpath:scalar.properties"/>
  ```

```java
@Component
@Component("iMan") // 고정 이름 값 설정 // refactoring 대비
public class Avengers {
	private String address;
    
	private IronMan iman;
	private HulkBuster hb;
	public Avengers(@Value("뉴욕") String address) {
		this.address = address;
	}
	
	public IronMan getIman() {
		return iman;
	}
	@Autowired 			  // 타입 기반의 빈 주입
	@Qualifier("ironMan") // 이름 기반으로 한정 중복 타입 있을 때
	public void setIman(IronMan iman) {
		this.iman = iman;
	}
	public HulkBuster getHb() {
		return hb;
	}
	
	@Autowired
	public void setHb(HulkBuster hb) {
		this.hb = hb;
	}
}

```



#### 단위테스트

---

단위 : 메서드 - 메서드 단위로 기능 테스트 : junit test

* @Before : 각각의 테스트 동작에 대한 사전 처리 작업
* @Test : 테스트 하고 싶은 내용 작성

```java
public class BeanCreationTest {
	// java templates => logger java 설정
	private static final Logger log = LoggerFactory.getLogger(BeanCreationTest.class);

	@Before
	public void setUp() throws Exception {
		log.trace("모든 @Test 호출 전에 동작 - 사전작업");
	}

	@Test
	public void test() {
		// spring application 잘 만들어지고 있나?
		ApplicationContext ctx = new ClassPathXmlApplicationContext("application.xml");
		assertThat(ctx, is(notNullValue()));
	}

}

```

