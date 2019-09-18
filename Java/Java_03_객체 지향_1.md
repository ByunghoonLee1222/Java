

# Java(객체 지향)

> **Association** - *has a*

> **Dependency** - *use a*

> **Generailiazation**(**Ingeritance**) - *is a*

### 객체(object)

* 객체 지향 Program의 구성(재사용,유지보수) 단위
* **특성**(Data)과 **행위**(method)로 구성



* **modifiers**
  1. access
     - public
     - protected
     - 생략
     - private
  2. usage
     - static
     - final
     - abstract

```java
[modifiers] class class명{

	//속성 (abstract을 뺀 나머지 모두 가능)
		데이터타입 속성명;

	//생성자 
    [access_modifier] 클래스명(인자들..){}
	
	//메서드 선언
	[modifiers] 리턴타입(void) 메서드명(인자들..){return value;}
}
```

* 선언

  * 클래스명 **변수명** = *new 생성자(값)*; (***hash code***)

* 호출

  * ***hashcode***.메서드,속성명
  * **변수명**.메서드,속성명
  * *new 생성자(값)*.메서드,속성명

  ```java
  public class Customer {
  	String name;
  	int age;
  	String address;
  	/*
  	 *  생성자
  	 *  - 객체 생성시 new에 의해 호출
  	 *  - 객체의 초기화를 담당
  	 *  - 클래스에 생성자가 선언되어 있지 않다면 컴파일러가 인자가 없고 내용이 없는 생성자를
  	 *    컴파일시 추가한다 ==> Default Constructor
  	 *    => 클래스 내에 생성자가 있다면 컴파일러는 Default Constructor를 추가하지 않는다.
  	 *    
  	 *    -Constructor Overloading
  	 *    	인자(인자의 개수, 타입, 순서)가 다른 생성자를 1개 이상 선얼할 수 있다.
  	 */
  	public Customer() {
  		
  	}
  	
  	public Customer(String name, int age, String address) {
          /*
  		 * this : this를 사용한 클래스로 부터 생성된 객체 중 현재 사용중인 객체를 참조한다.
  		 * 1. 로컬변수와 속성 이름이 같을 때 구별하기 위해 속성 앞에 this.를 붙인다.
  		 */
  		this.name = name;
  		this.age = age;
  		this.address = address;
  	}
  
  	String customerInfo() {
  		return "이름:" + name + " 나이:" + age + " 주소:" + address;
  	}
  }
  ```

  

  ```java
  	public static void main(String[] args) {
  		Customer cust1;
  //		local변수는 초기화를 하지 않고 연산을 하거나 메서드인자, 리턴 값으로 전달하면
  //      컴파일 오류 발생
  //		System.out.println(cust1);
  		
  		cust1 = new Customer();
  //		속성은 객체가 생성될 때 기본값(정수:0 실수:0.0 문자:/u0000 논리:false 참조형:null)
  //      값으로 초기화 됨.
  		System.out.println(cust1.customerInfo());
  //		이름:null 나이:0 주소:null
  		cust1.name="ssafy";
  		cust1.age=2;
  		cust1.address="서울시 강남구 역삼동";
  		System.out.println(cust1.customerInfo());
  //		이름:ssafy 나이:2 주소:서울시 강남구 역삼동
  		System.out.println(new Customer().customerInfo());
  //		이름:null 나이:0 주소:null
  		System.out.println(new Customer("홍길동",17,"율도국").customerInfo());
  //		이름:홍길동 나이:17 주소:율도국
  	}
  ```

### Access Modifier (접근제한자)

|  Access   | Same class | Same package | Subclass | universe |
| :-------: | :--------: | :----------: | :------: | :------: |
|  private  |     o      |              |          |          |
| (default) |     o      |      o       |          |          |
| protected |     o      |      o       |    o     |          |
|  public   |     o      |      o       |    o     |    o     |



### Encapsulation(캡슐화)

---

* 은닉효과 => decouple => 수정성 증가
* 보호
* getter,setter