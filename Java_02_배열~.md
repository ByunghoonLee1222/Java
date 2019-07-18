# Java

### 배열

- **Reference type**

- length 속성이 있고 배열의 크기를 나타냄

- index는 0부터 length-1까지

- 접근범위 벗어나면 **IndexOutOfBoundsException**

- 배열 크기 변경 불가

  ```java
  DataType [] 변수명; //선언  int [] arr;
  변수명 = new DataType[크기]; //생성  arr = new int[10];
  변수명[index] = 값; // 할당  arr[0] = 10;
  //default   정수 :0 	 실수 :0.0		논리:false	문자:\u0000	reference:null
  ```

  ```java
  for(int i=0; size = arr.length; i<size; ++i){
  	//size에 길이를 저장해놓고 반복을 돌리면 참조가 간단해진다.
  }
  ```

* ```java
  Arrays.toString(arr); // [ 0 , 1 , 2]
  ```

* **선언과 생성 할당 동시**

  ```java
  int [] arr= {0,1,2,3,4,5,6};
  ```

---

#### 배열 전달 방식

 * 자바는 변수에 값을 전달할 때, 인자에 값을 전달할 때, 리턴 값을 전달할 때 Pass By Value 형식 한가지 방식으로 전달한다.

 * Pass By Value : 변수를 위해 할당된 메모리에 있는 값을 전달

   * Primitive type : 변수를 위해 할당된 메로리에 실제 값이 저장 됨

 * => 변수, 인자, 리턴 값을 전달할 때 값이 전달 됨 ==> Pass By Value

   * Reference type : 변수를 위해 할당된 메모리에 참조 값(hash code)이 저장됨

 * => 변수, 인자, 리턴 값을 참조할 때 참조 값(hash code)이 전달 됨 

   ​      ==> Pass By Reference

---

#### 배열 인자 전달

```java
public static int[] passRefer2(int[] a, int offset,int len) {
		if(a!= null && offset+len <a.length) {
			int [] newData = new int[len];
			for(int i=0;i<len; ++i) {
				newData[i] = a[offset+i];
			}
			return newData;
		}
		return null;
	}
	public static void main(String[] args) {
		int [] data1 = {0,1,2,3,4,5};
		System.out.println(Arrays.toString(passRefer2(data1,2,3)));
    }
```



#### 배열관련 에러

|             예외명             |                             설명                             |
| :----------------------------: | :----------------------------------------------------------: |
| ArrayIndexOutOfBoundsException |                배열의 접근 범위를 벗어난 경우                |
|   NegativeArraySizeException   |               배열의 size를 음수로 생성한 경우               |
|      NullPointerException      | 객체를 생성하지 않고 선언만 한 상태에서 속성이나 메서드에 접근(객체명.속성 or 객체명.함수명(~))한 경우 |



#### 다차원 배열

* 1차원 배열의 중첩

#### 배열의 복사

```java
//		배열 크기를 변경할 수 없으므로 변경이 필요하다면 새로 생성해서 복사해야 한다.
		/*
		 * System.arraycopy(src, srcPos, dest, destPos, length);
		 * - 배열을 전체 또는 부분 카피하는 기능
		 * src : 복사할 원본
		 * srcPos : 원본의 복사 위치
		 * dest : 복사하는 곳(copy본)
		 * destPos : copy본의 복사할 위치
		 * length : 복사할 데이터 개수
		 */
		int []src= {0,1,2,3,4,5,6,7,8,9};
		int []copy = new int[15];
		int []copy2 = new int[3];
		
		//전체 복사
		System.arraycopy(src, 0, copy, 5, src.length);
		System.out.println(Arrays.toString(copy));
		
		//부분 복사
		System.arraycopy(src, 3, copy2, 0, copy2.length);
		System.out.println(Arrays.toString(copy2));
		
		/*
		 * Arrays.copyOf(orginal, newLength)
		 *  newLength 크기의 배열을 생성해서 새로운 배열에 orginal의 값을 복사해서 			리턴
		 */
		System.out.println(Arrays.toString(Arrays.copyOf(src, src.length+7)));
		
		/*
		 * Arrays.copyOfRange(orginal, from,to)
		 * orginal 배열의 값중 from 위치의 데이터 부터 to위치 전 데이터까지 복사해			서 리턴
		 */
		System.out.println(Arrays.toString(Arrays.copyOfRange(src, 3,6)));
```

