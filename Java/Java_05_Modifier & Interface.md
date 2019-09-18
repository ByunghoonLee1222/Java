# Modifier & Interface

### Singleton

---

```java
	/**
	 * 2. 객체를 1번 생성해서 참조변수에 저장한다.(참조변수는 static을 작성) 객체를 생성하지 않고 접근 가능 클래스가 메모리에 올라갈때
	 * 딱 한번 생성
	 */
Public class MySingle{
	private static MySingle instance;
	
	pirvate MySingle(){}
	/**
	 * 1.생성자를 private
	 */
	public static getInstance(){
		if(instance == null){
			instance =  new MySingle();
		}
		return instance;
	}
}

/////////////////////////////
// Singletone Pattern
		MySingle s1 = MySingle.getInstance();
```



### final

---

```java
/**
 * final : 값 변경 불가
 * 	클래스 : 상속금지	ex) String, System
 * 	메서드 : override금지
 * 	변수(속성, 로컬변수) : 값 변경 불가
 */

//class SubString extends String{} //final 클래스를 상속 받으면 컴파일 에러 발생

class Super1{
	public final void test() {}
}

class Sub1 extends Super1{
	//public final void test() {} //override 금지
}
/*
 * Blank Final Variable
 * 	-final 속성을 선언시에 값을 할당하지 않고 
 * 	 객체 생성시에 값을 할당해서(생성자에서) 사용
 *  -객체마다 다른 고정값 사용
 *  -모든 생성자에서 Blank Final Variable을 한번 초기화 해야 한다.
 */
class Blank{
	private final int serialNo;
	static int count;
	public Blank(){
		serialNo = ++count;
	}
	public Blank(int sno) {
		serialNo = sno;
	}
	public int getSerialNo() {
		return serialNo;
	}
//	public void setSerialNo(int sno) {
//		this.serialNo=sno;     // 한번 초기화 후 값 변경 불가
//	}
}

public class FinalTest {

	public static void main(String[] args) {
		final double PI = 3.14;
//		PI = 3.141; // final로 선언된 변수는 값 변경 불가
			
	}
}
```



### Abstract

---

```java
/**
 * 추상 : 추상적인 특징 - 메서드 : - 메서드를 선언부만 작성하고 구현을 하지 않는다. - sub에서 추상 메서드를 구현하도록 강제 위임
 * => sub에서 추상 메서드를 Override하지 않으면 컴파일 에러 발생 - 형식] [access modifier] abstract
 * 리턴타입 메서드명 (인자들..);(중괄호 x) static(메서드 고정), final(override금지) 금지
 * 
 * - 목적 1. sub들이 세부 구현이 너무 달라서 공통 코드가 없는 경우 2. 변경을 예상할 수 없는 경우
 * 
 * - 효과 1. 가볍게 상속 2. Override에 대한 성능 저하를 조금 졸일 수 있다. 3. 설계시에 sub에서 반드시
 * Override하도록 제어
 * 
 * - 클래스 : - 객체 생성 불가 - 상속 전용, 다형성 전용 - 클래스 내에 추상 메서드가 있으면 반드시 추상 클래스로 선언해야 한다.
 */
abstract class Animal {
	private String name;
	private String kind;
	private int age;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getKind() {
		return kind;
	}

	public void setKind(String kind) {
		this.kind = kind;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	/**
	 * 객체 생성 못하면 생성자가 필요없다? => 추상 클래스라도 sub 클래스에서 호출될 수 있으므로 필요하다면 생성자를 선언한다.
	 */
	public Animal() {
	}

	public Animal(String name, String kind, int age) {
		this.name = name;
		this.kind = kind;
		this.age = age;
	}

	public abstract void bark();
	public abstract void special();
	
}

class Dog extends Animal {
	public void bark() {
		System.out.println("멍멍");
	}

	public void keep() {
		Calendar today = Calendar.getInstance();
		int time = today.get(Calendar.HOUR_OF_DAY);
		if (time >= 9 && time <= 18) {
			System.out.println("잘 지키고 있어요.");
		} else {
			System.out.println("나도 좀 쉽시다.");
		}
	}

	@Override
	public void special() {
		keep();
	}

}

class Duck extends Animal {
	public Duck() {}
	public Duck(String name, String kind, int age) {
		super(name,kind,age);
	}
	public void bark() {
		System.out.println("꽥꽥");
	}
	public void fly() {
		String kind = getKind();
		if(kind != null && kind.equals("집오리")) {
			 System.out.println("오리는 날수 없다 엄마에게 혼났죠~");
		}else{
			System.out.println("날아올라 저 하늘 날고있어요. 이렇게 멋진 날개를 펴 꿈");
		}
	}
	@Override
	public void special() {
		fly();
	}

}

public class AbstractTest {

	public static void main(String[] args) {
//		Animal ani = new Animal(); //추상클래스로 객체 생성 불가
		
		/**추상 클래스라도 다형성을 적용하여 sub 객체를 참조할 수 있다.*/
		Animal an = new Dog();
		an.bark();
		
		/**추상 클래스라도 배열 객체는 생성할 수 있다.*/
		Animal[] animals =  new Animal[2]; /**sub들을 저장할 수 있다.*/
		animals[0] = new Dog();
		animals[1] = new Duck("채리필터","오리날다",20);
		for (Animal animal : animals) {
			animal.bark();
			animal.special();
//			if ( animal instanceof Dog) {
//				Dog dog = (Dog)animal;
//				dog.keep();
//			}else if( animal instanceof Duck) {
//				Duck duck = (Duck) animal;
//				duck.fly();
//			}
		}
	}
}
```



### Interface

---

* **Polymorphism**
  * 일반 클래스
  * 추상 클래스
  * interface

---

* 특별히 정의하지 않아도 컴파일 시에 아래 제한자가 추가된다
  * public static final 제한자가 상수 앞에 붙는다.
  * public abstract 제한자가 메서드 앞에 붙는다.
  * **메서드 Overriding 시 항상 public 제한자를 갖아야 한다.**

```java
/**
 * interface - 상수와 추상 메서드로만 구성되어 있다. - 속성에 자동으로 public static final이 컴파일때 추가 됨.
 * - 메서드에 자동으로 public abstract이 컴파일때 추가 됨 - 객체를 생성할 수 없지만 다형성에 의해 sub는 참조 가능 -
 * 다중 상속이 가능 - 선언] [public] interface 인터페이스명[extends 슈퍼인터페이스명1,....]{}
 * 
 * - 구현] [modifiers] class 클래스명 [extends 슈퍼클래스명] [implements 슈퍼인터페이스명1,...]{
 * 
 * }
 */
interface Flyer extends Trans, Cloneable {
	void fly();
}

class Human {
		public void start() {
			System.out.println("걸어 갑니다.");
		}
}

class SuperMan extends Human implements Flyer,Serializable{

	@Override
	public void stop() {
		System.out.println("잠깐 쉬어야징!!");
	}

	@Override
	public void fly() {
		System.out.println("하늘을 날라서 지구를 구하장!!");
		
	}
	
}
public class InterfaceTest {

	public static void main(String[] args) {
		/** package가 다른데 접근 가능, 객체 생성없이 접근 가능 => public static이다. */
		System.out.println(Trans.INIT);
//		Trans.INIT =20;  // 값변경 불가 => final 이다.
		
		SuperMan clark = new SuperMan();
		Trans t  = clark;
		Flyer f  = clark;
		Human h  = clark;
		Cloneable c  = clark;
	
	}
}
```

