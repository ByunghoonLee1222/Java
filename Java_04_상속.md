# Java

### import

* 다른 패키지에서 클래스를 참조할때 => package명.클래스명(ex.chapter03.MethodTest)
* 편리하게 쓰기위해 import package명.클래스명;
* import package명.*; (클래스만 import)
* 다른  패키지에 동일한 클래스명이 있으면 (java.util.Date d = new java.util.Date();)
* javac -d path 소스파일

---

### Inheritance(상속)

1. interface 상속
2. class 상속
   * 모든 속성과 모든 메서드를 상속받음
   * 단일 상속만 지원
   * 생성자는 상속되지 않는다 (호출은 가능)
   * **재사용**
     * 객체 생성(재사용만)
     * 상속(재사용 + **변경(추가,수정)**)

#### 상속 과정

* 부모 (상위) , super
* 자식 (하위), sub
* [modifiers] class sub클래스명 [extends 부모클래스명]

---

### Method Override(함수 재정의)

 * 상속 받은 메서드와 동일한 이름의 함수를 선언할 수 있다.

 * **목적**

   * 상속 받은 메서드와 기능이 동일하지만 상세 구현이 조금 다른 경우

   * 반영하기 위해 새로운 메서드를 작성해야 하는데 이때 메서드 이름과, 인자, 리턴타입을 상속 받은

     메서드와 동일하게 선언한다.

* **효과**

  1. 상속 받은 메서드와 이름, 인자가 같으므로 메서드 호출하는 방법이 같고 리턴 타입이 같으므로 호출후 

     처리 방법이 같아지므로 기존 코드를 변경하지 않고 수정된 내용을 반영할 수 있다.

  2. 기능이 동일한 경우 부모 객체, 자식 객체 구별하지 않고 같은 이름으로 함수를 호출한다.
     * 호출에 대한 편리성
  3. 다형성 관계에서는 Override된 메서드가 호출됨(Virtual Invocation)
     * 기존 코드를 변경하지 않고 수정된 내용을 반영할 수 있다.

* **규칙**
  1. 메서드 이름과 인자는 반드시 같아야 한다.
  2. **리턴 타입**
     * 1.7 리턴 타입이 반드시 같아야 한다.
     * 같은 타입이거나 sub를 리턴해야 됨
       * 부모 : public Customer getCustomer(){}
       * 자식 : public Customer getCustomer(){} or public MainCustomer getCustomer(){}
  3. access modifier는 **같거나 보다 넓은 범위(public)**로 선언한다.
     * access modifier를 줄이면 컴파일 오류 발생
  4. 예외는 같은 예외를 던지거나 안던져도 됨.
     * super를 던지면 컴파일 오류 발생

---

### super

* 재정의에 의해 무시된 부모의 멤버(속성,함수)에 접근할 때 **super**를 사용

  - super.함수명()   // super.속성명

* 생성자는 상속 되지 않지만 재상요을 위해 호출 가능

* super(~); ***주의점 : 생성자의 첫번째 명령에서만 호출 가능***

  ```java
  	public MainCustomer(String name, int age, String address,String hobby) {
  //		setName(name);			//상속받은 속성
  //		setAge(age);			//상속받은 속성
  //		setAddress(address);   //상속받은 속성
  		super(name,age,address);
  		this.hobby=hobby;
  	}
  ```

* 부모의 기본생성자가 없으면 오류
  * 컴파일러가 자동으로 super();호출
* 해결방법 : 인자있는 생성자를 명시적으로 호출해 준다. (ex. super("ssafy",2,"역삼"); )

---

### Polymorphism(다형성)

* Method (**호출에 대한 편리성 제공**)
  * 인자에 따라서 : Method Overloading
  * 부모 or 자식 따라서 : Mehtod Overriding

* Data
  * Primitive : (***자동 형변환***)byte => short(char) => int => long => float => double
    * double, boolean 두 인자로 모든 인자 포함 가능
  * **Reference** :  Super Type의 변수가 Sub Type의 객체를 참조할 수 있다.
    * Super 타입 = new Sub 객체

* **Shadow Impact**
  * 다형성 관계에서 sub에 추가된 속성이나 메서드에 접근 불가

* **Reference type 형변환**

  * 자동 형변환(Up casting)

    * sub type에서 super type으로 형변환될 때 자동 형변환 됨
    * 모든 sub는 super로 자동 형변환 됨

  * 명시적 형변환(Down casting)

    * super type에서 sub type으로 형변활될 때 명시적으로 형변환 해야 한다

    * super type이 참조하고 있는 객체의 sub타입으로만 형변환 됨

```java
		Manager mgr2 = new Manager(); // up casting
		Employee emp2 = mgr2;
		
		Engineer eng2 = new Engineer(); // up casting
		emp2 = eng2;
		
		Engineer eng3 = (Engineer)emp2; // down casting
		/**down casting 아님. ClassCastException 발생*/
		Manager mgr3 = (Manager) emp2;
		
```

#### instanceof

* Reference type 형검사
* 객체가 해당 클래스 타입이면 true, 아니면 false
  * 형식]
  	 * 		객체 instanceof 클래스타입 
  	 * **주의점** : super타입부터 검사하면 모든 sub는 super타입 검사된다 **형검사는 sub타입부터**!

```java
		if (emp2 instanceof Manager) {
			Manager mgr = (Manager) emp2;
			System.out.println("emp2는 Manager입니다. 직위:"+mgr.getPosition());
		}else if(emp2 instanceof Engineer) {
			Engineer eng = (Engineer) emp2;
			System.out.println("emp2는 Engineer입니다. 직위:"+eng.getSkill());
		}
```

#### Virtual Invocation(Dynamic Binding == Dynamic linking)동적 바인딩

* 다형성 관계에서 메서드가 Override된 경우라면 Override된  함수가 호출됨
* 런타임시 결정
*   스태틱(static) 메소드는 컴파일 시에 결정이 된다. 인스턴스 변수 또한 컴파일시에 결정된다

* **정적바인딩**
  * c, c++ : 컴파일시
  * java: 클래스 로딩될 때 메모리에 한번 할당됨

### 다형성 적용

```java
public class EmployeeManager {
	/**
	 * 다형성을 배열에 적용
	 * 다형성에 의해 모든 sub 타입은 super으로 형변환이 자동으로 되기 때문에
	 * super타입의 배열 하나만 선언하면 sub타입의 객체도 저장할 수 있다.*/
	private Employee[] emps;

	/** 다음 저장 위치, 현재 저장된 수 */
	private int empIndex;

	public EmployeeManager() {
		emps = new Employee[15];

	}
	/**
	 * 사원번호에 해당하는 사원 정보가 저장된 배열의 index를 리턴
	 * @param empno 찾을 사원 번호
	 * @return 사원번호에 해당하는 사원이 저장된 index를 리턴
	 * 			못찾은 경우 -1을 리턴
	 */
	public int findIndex(String empno) {
		if(empno !=null) {
			for(int i =0; i<empIndex; ++i) {
				if(empno.equals(emps[i].getEmpno())) {
					return i;
				}
			}
		}
		return -1;
	}
	
	/**
	 * 다형성을 리턴타입에 적용
	 * 다형성에 의해 모든 sub 타입은 super으로 형변환이 자동으로 되기 때문에
	 * 리턴타입을 super로 선언하면 sub도 리턴할 수 있다.
	 * 		public Employee getEmployee() {
				return new Manager();
			}
	 */
	public Employee search(String empno) {
		int index = findIndex(empno);
		if(index >-1) {
			return emps[index];
		}else {
			return null;
		}
		
	}
	/**
	 * 다형성을 메서드 인자에 적용
	 * 다형성에 의해 모든 sub 타입은 super으로 형변환이 자동으로 되기 때문에
	 * 메서드 인자를 super타입으로 선언하면 모든 sub타입의 객체도 인자로 전달 받을 수 있다.
	 * =>메서드 Overloading을 줄일 수 있다.
	 */
	public void add(Employee emp){
		System.out.println("Employee를 저장합니다.");
		if(emp!=null) {
			String empno = emp.getEmpno();
			int index = findIndex(empno);
			if(index > -1) {
				System.out.println("이미 등록된 사원번호입니다.");
			}else {
				if(empIndex >= emps.length) {
					emps = Arrays.copyOf(emps, empIndex+5);
				}
				emps[empIndex++] = emp;
			}
		}
	}
	public void update(Employee emp) {
		if(emp !=null) {
			String empno = emp.getEmpno();
			int index = findIndex(empno);
			if(index>-1) {
				emps[index] = emp;
			}else {
				System.out.println("수정할 사원번호가 등록되지 않았습니다.");
			}
		}else {
			System.out.println("수정할 사원의 정보를 입력해 주세요");
		}
	}
	public void remove(String empno) {
		int index = findIndex(empno);
		if(index > -1) {
			emps[index] = emps[--empIndex];
		}else {
			System.out.println("삭제할 사원번호가 등록되지 않았습니다.");
		}
	}
	
	public void print() {
		for(int i =0; i<empIndex; ++i) {
			System.out.println(emps[i]);
		}
	}
}
```

### Static

* 정적인 특성 부여

* 클래스가 로딩되는 시점에 결정됨

* 객체 생성없이 클래스로만 접근 가능 Class.속성명, Class.메서드명(~)

* **속성** 

  * 클래스가 로딩될 때 메모리에 한번 할당됨

  * 공유변수가 됨

* **메서드**

  * 클래스가 로딩될 때 메서드 바인딩을 한다(정적 binding)

  * 유틸리티성 메서드 ( 속성이나, non-static 메서드를 사용하지 않고 전달된 인자로만 처리하는 기능)

*  **static block**

  * 클래스가 로딩될 때 한번 수행됨.
  * static 속성을 초기화 하거나 단 한번 수행될 코드를 작성

* **instance block**

  * 객체가 생성될 때마다 수행되고, 생성자 보다 먼저 수행됨
  * 어떤 생성자로 객체를 생성하던 **공통적으로 수행될 코드**가 있다면 instance block에서 작성

> JVM이 가장 힘들어하는 것은 객체생성, garbage collecting이다.