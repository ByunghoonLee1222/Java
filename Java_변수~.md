# Java

### Data Type

* **Primitive** : 변수를 위해 할당 된 메모리에 **실제 값**이 저장 됨
* **Reference** : 변수를 위해 할당된 메모리에 **참조 값**(Hash code)이 저장됨

>Java는 Pass(call) by value 만 있다.
>
> C- call by value, address / C++ (+call by reference)

### Default

* 정수 : int

* 실수 : double

  #### 형변환

  ```java
  		byte b1 =10, b2=30;
  		int i1 = b1+b2;
  		byte b3 = (byte)(b1+b2);
  ```

