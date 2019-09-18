# Exception

* **Error**(System 적 오류)

|       Error        |                      의미                      |
| :----------------: | :--------------------------------------------: |
|  OutOfMemoryError  |            heap 메모리 부족인 경우             |
| StackOverFlowError | Stack 메모리 부족인 경우(잘못된 재귀함수 호출) |
| NoSuchMethodError  |            실행시 main이 없는 경우             |

* **Exception**(S/W적 오류)

  * RuntimeException(UncheckedException)

    |            예외 명             |                             설명                             |
    | :----------------------------: | :----------------------------------------------------------: |
    | ArrayIndexOutOfBoundsException |                배열의 접근 범위를 벗어난 경우                |
    |   NegativeArraySizeException   |               배열의 size를 음수로 생성한 경우               |
    |      NullPointerException      | 객체를 생성하지 않고 선언만 한 상태에서 속성이나 메서드에 접근(객체명.속성or 객체명.함수명(~))한 경우 |
    |       ClassCastException       |                  객체 형변환을 잘못 한 경우                  |
    |     NumberFormatException      |        문자열 데이터를 잘못된 format으로 변환시 발생         |
    |   IndexOutOfBoundsException    |        List에서 잘못된 index에 데이터를 추가하는 경우        |
    |    IllegalArgumentException    |                  잘못된 인자를 전달한 경우                   |
    |      InterruptedException      |             동작 중인 쓰레드를 중단 시킬때 발생              |

  * CheckedException (개발자 실수 x)

    |        예외명         |                설명                |
    | :-------------------: | :--------------------------------: |
    | FileNotFoundException |   지정한 경로에 파일이 없는 경우   |
    |      IOException      |         io중 발생하는 오류         |
    |     SQLException      | DB에서 데이터 처리중 발생하는 오류 |



* **예외발생시 디버깅 해야한다**
* 개발자 실수 => 디버깅
* 사용자 실수(입력 오류) = > 예외 처리
* Exception 클래스들이 상속 관계일 경우 서브 클래스부터 정의해야 한다

```java
	public static void main(String[] args) {
		int result = 0;
		try {
		result = 256/ Integer.parseInt(args[0]);
		}
//		catch(Exception e) {
//			System.out.println("0이 아닌 정수를 입력해 주세요");
//		}
		/**
		 * 오류마다 처리 방법이 다른경우 각각 처리한다.*/
		catch(ArrayIndexOutOfBoundsException e){
			System.out.println("처리할 데이터를 입력해 주세요.");
		}catch(ArithmeticException e) {
			System.out.println("0이 아닌 정수를 입력해 주세요");
		}catch(NumberFormatException e) {
			System.out.println("정수를 입력해 주세요");
		}finally {
			/**
			 * finally문은 try문이 수행되면 반드시 수행되는 문장
			 * 	-반드시 처리해야 하는 기능을 작성 ex) 자원밤납
			 * 	-finally문이 수행되는 경우
			 * 		-오류가 발생하지 않아도 수행됨
			 * 		-오류가 발생해도 수행됨
			 * 		-오류가 발생했지만 처리되지 않은 경우에도 수행됨
			 * 		-try문이나 catch문에서 return된 경우에도 수행됨
			 * 	-finally문이 수행되지 않는 경우
			 * 	 System.exit(~)을 통해 JVM을 종료시킨 경우
			 */
			System.out.println("finally문이 수행됨....");
		}
		System.out.printf("수행 결과 : %d\n",result);
		
	}
```



### 선언적 예외처리

---

* 메서드 호출한 곳으로 오류 던져서, 메서드 호출한 곳으로 예외 처리하도록 위임

 * 		메서드 선언부에 예외 처리
 * 	[modifiers] 리턴타입 메서드명([인자들.])[throws 에외,....]{  }

**목적**

1. 오류가 발생한 곳에서 직접 처리하면 처리방법이 고정되므로 상황에 맞게 처리가 어려움

   => 호출한 곳의 상황에 맞게 처리하도록 위임 => 처리방법의 다양성

2. 한 프로그램의 수많은 기능에서 다양한 오류가 발생하지만

   처리방법은 동일한 경우 오류가 발생한 곳마다 처리하면 코드 재사용성이 떨어지므로 호출한 곳으로 

   던져서 한번에 처리한다.

   (UI : 이벤트 처리하는 곳, Server : 클라이언트 요청 처리하는 곳)

3.  프로그램 수행중 정상 처리된 결과는 return을 통해 전달하고 
    비정상적인 상황은 예외를 통해 전달한다.



-**오류 발생 시키기**

​	throw 오류객체  // 메서드 - throws Exception

```java
class MyUtil{
	public static int div(int i, int j) throws Exception {
		if(j!=0) {
			// 정상적인 상황을 리턴
			return i/j;
		}else {
			//비정상 적인 상황을 예외로 담아 보냄
			/**CheckedException은 반드시 예외 처리해야 한다.*/
			throw new Exception("0으로 나눌수 없습니다.");
		}
	}
	public static int mod(int i, int j) {
		if(j!=0) {
			// 정상적인 상황을 리턴
			return i/j;
		}else {
			/**
			 * UncheckedException은 예외 처리 하지 않아도 컴파일 에러가
			 * 발생하지 않기 때문에 필요할 때만 예외 처리한다.
			 */
			throw new RuntimeException("0으로 나눌수 없습니다.");
		}
	}
```



### 사용자 정의 Exception

---

 * **UncheckedException**

   * **예외 처리하지 않아도** 컴파일 오류가 발생하지 않는 오류들

   * **종류**
     * RuntimeException과 RuntimeException을 상속 받은 sub들

   * **사용자 정의 UncheckedException 만들기**
     * RuntimeException이나 RuntimeException을 상속 받은 sub들을 상속 받는다

   
 * **CheckedException**

   * 예외 처리하지 않으면 컴파일 오류가 발생해서 **반드시 예외 처리해야 하는 오류**

   * **종류**

     * RuntimeException과 RuntimeException을 상속 받은 sub들을 뺀 예외들

       ex) Exception, IOException

   * **사용자 정의 CheckedException 만들기**
     * RuntimeException이나 RuntimeException을 상속 받은 sub들을 뺀 예외들을 상속 받는다

```java
//CheckedException
class MyChecked extends Exception{
	public MyChecked() {
		/**printStacTrace(), getMessage()를 통해 메세지를 전달 받을 수 있다.*/
		super("Checked Exception 발생"); 
	}
	public MyChecked(String msg) {
		super(msg);
	}
}
//UncheckedException
class MyUnChecked extends RuntimeException{
	public MyUnChecked() {
		/**printStacTrace(), getMessage()를 통해 메세지를 전달 받을 수 있다.*/
		super("Checked Exception 발생"); 
	}
	public MyUnChecked(String msg) {
		super(msg);
	}
}

class MyUtil2{
	public static int mod(int i, int j) {
		if(j==0) {
			/** UnChecked라서 예외 처리하지 않아도 컴파일 오류가 발생하지 않는다.*/
			throw new MyUnChecked("0으로 나눌수 없습니다");
		}else {
			return i/j;
		}
	}
	public static int div(int i, int j) throws MyChecked {
		if(j==0) {
			/** Checked라서 예외 처리하지 않으면 컴파일 오류가 발생한다.*/
			throw new MyChecked("0으로 나눌수 없습니다");
		}else {
			return i/j;
		}
	}
}
```

---

```java
public class CanNotFoundException extends Exception {
	public CanNotFoundException() {
		super("등록되지 않은 사원 번호입니다.");
	}
	public CanNotFoundException(String msg) {
		super(msg);
	}
}

public class DuplicateException extends Exception {
	public DuplicateException() {
		super("이미 등록된 사원 번호입니다.");
	}
	public DuplicateException(String msg) {
		super(msg);
	}
}
///////////////////////////////////////////////////////////////
	public Employee search(String empno) throws CanNotFoundException {
		int index = findIndex(empno);
		if(index >-1) {
			return emps.get(index);
		}else {
			String msg = String.format("%s번 사원번호는 등록되지 않았습니다.", empno);
			throw new CanNotFoundException(msg);
		}
		
	}
///////////////////////////////////////////////////////////////
	public void add(Employee emp) throws DuplicateException{
		System.out.println("Employee를 저장합니다.");
		if(emp!=null) {
			String empno = emp.getEmpno();
			int index = findIndex(empno);
			if(index > -1) {
				String msg =
                    String.format("%s번 사원번호는 이미 등록된 사원번호입니다.", empno);
				throw new DuplicateException(msg);
			}else {
				emps.add(emp);
			}
		}else {
			throw new DuplicateException("등록할 사원 정보를 입력해 주세요.");
		}
	}
```

