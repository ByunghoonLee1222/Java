# CSS3

#### CSS 설정

1. **css파일을 설정**
   
* `<link rel='styleseet' href='css 경로'/>`
   
2. **내부 css 설정**

   * head 태그에 설정
   * `<head> <style> css </style> </head>`

   - 태그에 설정
   - `<tag style='css설정' />`

---

* `*{ }` = **모든 선택자**
* **기본 선택자**
  1. `태그명{  }  ex) h1{color : red;}`
  2. `#id명 { } ex) #box{color : pink;}`
  3. `.class명{  } ex) .box{color : orange;}`

* 자식 선택
  * ` #header > h1 {color: orange;}`
  * `div > .title {color: orange;}`

* **동위 선택자**
  * 선택자A+선택자B => A바로 다음에 오는 B형제
  * 선택자A~선택자B => A뒤에 오는 B 아래의 모든 형제들

---

#### 여러 기능들(선택자)

* `h1:hover {color:pink;}` => 마우스 올릴경우
* `h1:active {color:purple;} `=> 클릭 시 
* `li > a:first-child { color: red; }` = > 해당 태그의 첫번째
* ` body > *:first-of-type { color: red; }` => 태그별 첫번째
* `li:nth-child(2n) {background: pink;}` => 짝수번째 (2n+1 => 홀수)

* `  P::first-letter {font-size: 3em;}` => 첫번째 글자

* `P::first-line {color:red;}` => 첫번째 줄

* ```html
  p{counter-increment: rint;} //p의 넘버링 1~
  p::before {content: counter(rint)". ";} // p앞쪽에 넘버링 출력
  p::after {content: ' -' attr(data-page) 'page';}// p뒤쪽에 data-page속성값 출력
  ```

* ```html
  	a{text-decoration: none; /* a태그의 밑줄이 없게*/
  	  color: black;
  	 } 
  	a:visited {
  	color: red;
  	}	//선택 후 처리
  	a:link::after {content : ' - 'attr(href)}
  	a:hover{color: orange;}
  ```

* `input:not([type=password]){background: red;}`=> 해당타입은 제외

* **크기단위**

  * em => 글자 크기, 배수 단위
    * 1em : 글자의 원래 크기
    * 2em : 글자의 원래 크기에 2배
  * px => 글자, 이미지나 요소들의 크기를 지정, 화소수 단위
  * % => 백분율 단위



#### display

---

* 요소의 특성을 정의해서 화면에 표시
* **none** 
  * 화면에 안보인다
  * 요소가 자리를 차지하지 않는다
* **inline**
  * element를 inline 특성으로 화면에 표시
* **block**
  * element를 inline 특성으로 화면에 표시
* **inline-block**
  * element를 inline 처럼 한행에 여러 태그가 배치하고 block 처럼 너비 높이를 지정할 수 있다
* **table**
  * element를 table 처럼 표시
* **table-cell**
  * element를 table의 cell로 표시 (기본 1행에 표시되는 컬럼)=> td

* **table-row**
  * element를 table의 row로 표시 => tr

* **table-column**
  * element를 table의 column로 표시 => dr

#### visiblity

---

* element에 대한 가시성을 지정
* **hidden**
  * element를 화면에 보이지 않게한다
  * element의 원래 자리는 그대로 있음
* **visible**
  * element를 화면에 보이게 한다
  * 기본 설정



```html
	div	{width : 100px;
		 height: 100px;
		 background: red;
		 margin : 10px; }
	#box{border:10px solid black;
		padding:10px;
		box-sizing: border-box; <!-- 보더를 포함한 box -->
		}
```
```html
 	.box{border-width: 5px;  	/*테두리 4면에 대한 두께*/
 		 border-style: dotted;  /*테두리 4면에 대한 스타일 */
 		 border-color: orange;  /*테두리 4면에 대한 색상 */
 	}
	.box{border:5px dashed pink;}
```

```html
div {
	background: pink;
	width: 100px;
	height: 30px;
	border: 1px purple solid;
}

.box1 {
	border-radius: 30px;
	text-align: center;
} /* 4개의 꼭지점에 radius를 설정*/
/*왼쪽 상단 오른쪽 상단 오른쪽 하단 왼쪽하단 */
.box2 {
	border-radius: 10px;
	text-align: center;
}

.box3 {
	border-radius: 50px 40px 20px 10px;
	text-align: center;
}
```

#### position

---

* 요소의 위치를 지정

* 종류

  * **fixed** 
    * body의 원점(0, 0)을 기준으로 left, right, top, bottom의 위치를 고정
    * body의 원점을 기준으로 절대 위치에 좌표를 설정
  * **static**
    * position을 지정하지 않으면 기본적으로 static이 적용이 됨
    * x, y좌표를 직접 지정해도 적용이 되지 않고 html engine이 요소의 display 속성에 따라서 알아서 배치
  * **absolute**
    * 부모의 시작위치를 원점으로 해서 절대 위치에 좌표를 설정
  * **relative**
    * static에 의해 표시될 위치를 기준으로 좌표를 설정

  