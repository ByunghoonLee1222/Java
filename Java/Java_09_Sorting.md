# Sorting

* **Collection(Iterable, Serializable 상속)**
  * List
  * Set
  * Map
    * value값만 - map.values()
    * key값만 - map.keyset()
  
* **Comparable<T>**  ***=>reference type만 Comparable 사용가능***
  
  * **int compareTo(T other)**
    * 3가지 리턴값 (대소비교)
    * 앞에서 뒤를 빼서 음수, 0 이면 그대로(오름차순 정렬)
    * 양수이면 자리를 바꿈(더 큰값 오른쪽)
    * 반대로 뒤에서 앞을빼면 (내림차순)
  * compareTo 를 이용해서 내가 정렬코드를 짠다
  
* **Comparator<T>**(비교 도우미)=>***모든 타입 사용가능***

  * int compare(a, b) - a= 원소 1, b= 원소 2

    

* Arrays.sort(int []arr,Comparator c)
  * 비교도우미 사용
  * 둘다 사용 가능
  
* Arrays.sort(int[]arr)
  
  * compareTo만 사용(Comparable)