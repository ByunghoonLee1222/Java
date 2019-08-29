# HTML5

* Server => Tomcat v8.5
*  Web프로젝트 생성 후 WebContent 밑에 html 파일 생성
* WEB-INF 밑에 html 파일을 만들면 실행 안된다



#### href

---

* 외부 자원으로 연결 `<a href = "url" target="  "> </a>`
* 페이지 내로 이동 `<a href = "#id명" target=""> 본문이름</a>` 해당 아이디로 이동-

#### 경로

---

* 절대 경로
  * 로컬 : Drive부터 파일까지 경로 표시 C:\ssafy\a.txt
  * web : Protocal부터 표시 http://IP:Port/파일경로
* 상대 경로
  * 로컬 : 현재 작업하는 파일을 기준
  * web : 브라우져에 표시된 url 기준
    * . => 현재경로
    * .. => 상위 경로
    * .\ 하위 경로명\ => 하위경로
    * 상위 경로 제외하고 . 과 .\ 은 생략 가능

#### UL

----

* Unordered List
* 목록앞에 기호가 표시됨
* type을 지정하지 않으면 기본적으로 disc 설정



#### OL

---

* Ordered List
* 목록에 순서를 표시
* -type을 지정하지 않으면 기본적으로 아라비아 숫자로 설정
  *  1:  아라비아 숫자
  *  i : 소문자 로마 숫자
  * Ⅰ: 대문자 로마 숫자
  *  a : 소문자 알파벳
  *  A : 대문자 알파벳



### table

---

* th : 굵고, 중앙 정렬
* tr : 행 하나 , 왼쪽 정렬 ( 다른 정렬시 align= ' ' 사용)
* td : 한 행에 들어가는 data , 왼쪽정렬 
* rowspan = 행 병합
* colspan = 열 병합



#### image

---

* <img src='../images/이미지명.jpg'/ width = "300">

* width , height 중 하나만 설정 시 이미지 기본 비율에 맞게 조정
* alt = 이미지 없을 시 대체 문구



#### form 태그

---

*   `<form method=" " action="url" enctype=" "></form> `
* action => 입력 받은 Data를 전송할 Server url

* enctype => File: multipart/form-data
* `<form> <input type=" " name=" " value=" "/> </form>`
* 반드시 form 안에 넣어야 한다
* name => 값을 구별할 이름
* value => 서버에 전송될 값



#### inline 요소

---

* content의 width, height를 지정할 수 없다
* inline 요소의 크기는 데이터의 크기에 의해 결정됨
* 한 행에 여러개의 inline 요소를 표시
* a, span, img, input ...

#### block 요소

---

* content의 width, height를 지정할 수 있다
* 한 행에 block 요소 하나만 표시
* table, div, li, p, h6~h1

