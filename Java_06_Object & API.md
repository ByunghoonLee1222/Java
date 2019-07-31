# Object & API

### Object

------

- 최상위 클래스

- 모든 클래스가 기본적으로 상속받아야 하기 때문에 extends Object를 사용하지 않아도 컴파일러에 의해 자동 상속

- Object 클래스에는 **모든 클래스의 공통적인 기능을 정의**하고 **자주 사용되는 Method를 정의**하여 필요시 Overriding 해서 사용하도록 권장

- 자주 override 되는 메서드(다형성)

  - toString():String - 객체를 대표하는 문자열을 return

  - hashCode():int - 객체를 구분하는 코드 값을 리턴

  - equals(Object o):boolean - 객체의 내용을 비교

```java
	/**
	 * 객체의 내용이나 객체를 대표하는 문자열을 리턴
	 * - System.out으로 출력할 때 호출된다.
	 * - 문자열 + 객체 => toString() 을 호출ㅐ서 리턴되는 문자열을 연결시킨다.
	 * - 필요시에 Override
	 * - Override하지 않으면 클래스면@해쉬코드가 리턴된다.
	 */
	@Override
	public String toString() {
		return "empno=" + empno + ", name=" + name + ", salary=" + salary;
	}
	/**
	 * 객체의 내용을 비교하는 기능
	 * - 객체의 내용을 비교해야 한다면 반드시 Override 해야 한다.
	 */
	public boolean equals(Object obj) {
		if (obj!=null && obj instanceof Employee) {
			Employee emp = (Employee) obj;
			if(empno!=null && empno.equals(emp.empno)) {
				return true;
			}
			
		}
		return false;
		
	}
```



### String

------

***문자열은 final 이라 새로 생성해서 리턴해준다***

```java
/**	String은 유일하게 new 생성자(~)를 통하지 않아도 객체를 생성할 수 있다.
*	-new 생성자(~) : 매번 heap에 객체가 생성된다.
*	-new 생성자를 사용하지 않은 경우 : Constance Pool에 없으면 생성/ 있으면 해당 객체의 참조값만 전달 받는다.(재사용)
*/
		String str1 = "hello";
		String str2 = "hello";
		String str3 = new String("hello");
		String str4 = new String("hello");
		
		System.out.printf("str1==str2 %b\n",str1==str2);
		System.out.printf("str1==str3 %b\n",str1==str3);
		System.out.printf("str3==str4 %b\n",str3==str4);
		
	}
```

#### StringBuffer, StringBuilder

```java
//새로운 객체를 생성하기 때문에 garbage가 많이 발생
//따라서 StringBuffer, StringBuilder사용 
//차이점 : synchronized(줄세워서 하나씩 먼저하게 하는것,상대적으로 성능 느리다)- buffer에만 있다.

	StringBuffer sb1;
	StringBuilder sb2;
// append
// insert
// reverse()
// setCharAt
// setLength
```

#### String API

```java
		/**
		 * public String[] split(String 구분자)
		 * 문자열을 구분자 기준으로 subString하는 기능
		 * 
		 */
		String [] tokens = "hello world java ssafy".split(" ");
		for(String token : tokens) {
			System.out.println(token);
		}
		/**
		 * format(String format, Object ...o)
		 * %s :문자열
		 * %d :정수
		 * %f :실수
		 * %b :논리
		 * %c :문자
		 */
		String str = String.format("%d번 사원번호", 1);
		System.out.println(str);
	}
```

- concat, replace, **charAt**, substring, toLowerCase(), toUpperCase(),**startsWith**, indexOf, endsWith,**equals**, **compareTo**(String s)

#### Wrapper class

- 객체가 아닌 것 : primitive data type
- primitive type을 객체화 시켜주는 클래스
- Byte, Short, Integer, Long, Float, Double, Boolean, Character

```java
		Integer iPrice = new Integer(5000);
		int price = iPrice.intValue();
		
		// java5부터 자동 변환
		Double IPI = 3.14; //auto boxing // primitive 객체화
		double pi = IPI;   //auto unboxing // 객체를 primitive
		
		Object inum = 256;
		
		/**
		 * 문자열 데이타를 해당 format의 Primitive
		 * parseXXX(String 값)
		 * -잘못된 format으로 변경하면 NumberFormatException발생
		 */
		price = Integer.parseInt("5000");
		double rate = Double.parseDouble("0.1");
	
```



### Collection

------

- **Set**

  - 중복 저장 X
  - index X

  ```java
  		HashSet<Object> set1 = new HashSet<Object>();
  		System.out.println(set1.add("hello"));
  		System.out.println(set1.add("hello"));
  		System.out.println(set1.add(256));
  		System.out.println(set1.add(3.14));
  		System.out.println(set1.add(new Employee("1","ssafy",100)));
  		System.out.println(set1.add(new Employee("1","ssafy",100)));
  		System.out.println(set1);
  		for(Object obj : set1) {
  			System.out.println(obj);
  		
  		}
  ```

- **List**

  - 순서대로 저장

  - 중복 저장 O

  - index 는 0~ size()-1 까지

  - 중간 삽입은 0~size()만 가능

  **List 종류**

  - **ArrayList**
    * 배열의 형태
    * 인덱스 이동이 가능
    * 검색이 빠르다
  - **LinkedList**
    * 다음 데이터에 대한 링크(해쉬)를 가지고있다.
    * 중간삽입, 삭제가 빠르다.
    * 검색속도가 배열보다 느리다.
    * 앞으로 가는 , 뒤로가는 링크가 있다.

```java
		ArrayList<Object> list1 = new ArrayList<>();
		LinkedList list2;//기본생성자만 있다.
		list1.add("hello");	//맨 끝에 추가됨
		list1.add("hello");
		list1.add(256);
		list1.add(3.14);
		list1.add(new Employee("1","ssafy",100));
		System.out.println(list1);
		list1.add(3,true); // 중간삽입 index 0~ size()-1 만큼 가능
		//list1.add(7,true); // IndexOutOfBoundsException 발생 LinkedList도 동일
		System.out.println(list1);
//		get(int index) : index번째 해당하는 데이터 추출
		System.out.println("3's index :"+ list1.get(3));
		
		/** 
		 * indexOf(Object o), lastIndexOf(Object o), contains(Object o),
         remove(Object o) 함수는
		 * 해당 기능을 수행하기 위해 equals(Object o)를 호출해서 객체 비교한다.
		 */
		// eqauls 함수 ovverride 해야한다. (객체 비교시)
		int index = list1.indexOf(new Employee("1","ssafy",100));
		System.out.println(index);
		
		/**
		 * java5부터 Collection에  Generic(객체 생성 시 동적 타입결정)을 적용
		 * - 생성할때 지정한 type만 저장한다.
		 * - 추출시 형변환을 할 필요가 없다.
		 */
		ArrayList<Employee> emps = new ArrayList<Employee>();
//		ArrayList<Employee> emps = new ArrayList<Manager>();//다형성 적용 X
		emps.add(new Employee("1","ssafy",300));
		emps.add(new Manager("2","홍길동",300,"대리")); //데이터 저장시에는 다형성 적용
//		emps.add("hello"); //지정 타입 외에는 컴파일 에러
		
		Employee emp = emps.get(0);
		System.out.println(emp);
		//형변환 없이 바로 추출 가능
```



### equals, hascode override

---

```java
	public boolean equals(Object obj) {
		if (obj!=null && obj instanceof Employee) {
			Employee emp = (Employee) obj;
			if(empno!=null && empno.equals(emp.empno)) {
				return true;
			}
			
		}
		return false;
		
	}
	
	/**
	 * 객체의 hashcode를 리턴하는 기능
	 * - override할 필요가 없음
	 * - override 해야 하는 경우
	 * 	1. Set에 동일한 내용의 객체를 저장하지 않고 싶을 때
	 * 	
	 */
	public int hashCode() {
		int empnoHash = empno != null? empno.hashCode() : 0;
		int nameHash = name !=null? name.hashCode() : 0;
		return empnoHash | nameHash | salary;
	}
```

#### Map

---

```java
		HashMap<Integer,Object>map1 = new HashMap<>();
		/**put(key, value) : 데이터 추가 또는 교체*/
		map1.put(1, "hello");
		map1.put(2, new Employee("1","1",1));
		map1.put(1, "world"); // 키값이 같으면 교체
		System.out.println(map1);
		System.out.println(map1.get(2));
		
		//keySet(): map에 저장된 key값만 추출
		Set<Integer>keys = map1.keySet();
		for( Integer key : keys) {
			System.out.println(key);
		}
		/** values() : map 에 저장된 value값만 추출 */
		Collection<Object> values = map1.values();
		for( Object v: values) {
			System.out.println(v);
		}
```

