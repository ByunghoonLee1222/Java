# XML(Extensible Markup Language)

* 구조와 의미를 설명(서식X)
* **Well-formed Document**
  * 구문의 일반적인 규칙 , 구문의 체크가 까다롭다
  * 일반적인 규칙
    * Case Sensitive
    * Closing Tags
      *  ( <name> 홍길동 </name> | <name/> => Empty tag)
    * No Overlapping Tags
    * Root Element 
      * Root는 반드시 하나
    * Attribute : name='value' or name = "value"
      * tag의 속성값
* **Valid Document**
  * well-formed 문서이면서 DTD(Document Type Definition)나 Schema에 정의된 형식에 맞는 문서

* ISO-8859-1 => 국제 표준 1byte  256가지 영어 대/소 , 숫자 , 특수기호 (ASCⅡ(128) 확장)
* UTF-8 => 한글 포함

##### 내부 Entity

---

* < => &lt
* &gt; => &gt
* ' => &apos
* " => &quot
* &  => &amp

##### 네임스페이스

* xmlns:prefix = "구조 URL"
  * 태크 &lt;prefix:태그명>



* default 네임스페이스
  * xmlns = "구조 URL"
  * <태그명></태그명>

##### XML API

* **SAX**
  * 빠르다 (하나씩 읽어서 처리)
  * 데이터 서치만
* **DOM**
  * 전체를 읽어 트리구조를 만들어 처리
  * 느리지만 읽기 쓰기 수정 삭제 가능
  * 웹브라우저/ 자바스크립트 