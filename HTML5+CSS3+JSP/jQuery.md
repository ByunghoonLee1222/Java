# jQuery

* {1.function | 2. selector | 3. DOM객체(jQuery객체) | 4. ' 태그' }
* $(document) => DOM객체를 jQuery로  // 3
* $(document).ready(function(){});   <=> $(function(){})        // 생성
* window.onload = fucntion(){} 와 같은 기능

```javascript
/*  $(document).ready(function(){})
	 - document가 준비되면(DOM트리가 구성되면) 인자로 전달한 함수를 실행
	 - window.onload = function(){} 과 동일한 효과
*/

/* 	$(document).ready(function(){
		console.log('jQuery 예제 ....')
	}); */
	
	$(function () {
		console.log('jQuery 예제 ....')
	})
```



* selector에 해당하는 태그를 찾아서 jQuery 객체로 생성

#### selector

---

* 태그
  * body ,h1  => 속성[ ]
* 아이디
  * #아이디명 => 자식  > 후손 
* 클래스
  * .클래스명 => :first :last :nth-child  :hover

```javascript
	$(function () {
		$('#content').css('color','pink');
	});
	/////////////////////////////
		$(function() {
		$('span').css('color', '#47C83E');
		$('#a').css('background','#F29661');
		$('.bclass').css('border','1px solid #47C83E');
		$('p[title]').css('border','1px solid gray');
		
		//아이디가 c인 요소 내의 span 태그의 배경색을 blue로 설정
		$('#c>span').css('background','blue');
		
		/*$('selector') : html page내에서 selector에 해당하는 tag들을 다 찾는다.
		  $('selector',content) : content내에서 selctor에 해당하는 tag들을 다 찾는다.
		*/
		var divC = $('#c');
		  $('span',divC)	//
	});
////////////////////////////////////////
   //even odd => 0부터 시작
		$(function(){
			$('tr:even').css('background','pink');// 짝
			$('tr:odd').css('background','purple'); // 홀
			$('tr:first').css('background','black').css('color','white');
			$('tr:last').css('background','orange').css('color','whilte');
		})
```

#### noConflict()

```javascript
	/* $.noConflict()
		prototype도 $를 이용해서 사용하므로 jQuery와 같이 사용하면 충돌이 난다.
		그래서 jQuery에서는 $를 사용 못하고 jQuery()만 사용하도록 설정
	*/
	$.noConflict()
	/*
	 $(function(){
		 console.log('$못쓰도록 설정해서 error남')
	 })
	*/
	
	jQuery(function(){
		console.log('$.noConflict()는 jQuery()만 사용해야한다.')
	})
```

#### val()

```javascript
	/*	val() 		: input양식의 value값을 추출
		val('값') 	: input양식의 value값을 설정
	*/
	$(function () {
		//click(function(){}) 선택자에 해당하는 요소가 click되면 인자로 지정한 함수가 수행됨
		$('#loginb').click(function(){
			console.log($('#id').val())
			var hobby = $('#hobby:checked');
			for(var i=0; i<hobby.length;i++){
				console.log($(hobby.get(i)).val())
			}
			
			
			$('#id').val('ssafy'); //값 설정
		});
	})
```

---

* $('<태그명>') 태그를 생성해서 jQuery 객체로 
* = document.createElement('태그명');
* innerHTML = html() 
* A.append(B)

```javascript
	$(function(){
		/* $('#btn').click(function () {
			$('#content').html($('#content').html()+'<h1 class="header">hello</h1>')
		}) */
        
		// A.append(B) : B를 A에 맨 끝에 추가
	//	$('#content').append('<h1 class="header">hello</h1>');
	//	$('#content').append($('<h1>hello</h1>').css('color','pink').css('border','1px solid purple'));
        
		// B.appendTo(A) : B를 A에 맨 끝에 추가
	//	$('<h1 class="header">hello</h1>').appendTo('#content');
		$('<h1>hello</h1>').css('color','pink').css('border','1px solid purple').appendTo('#content');
	})

/////////////
	$(function () {
		setInterval(function(){
			$('img:first').appendTo('body');
		}, 500);
	})
```

#### remove()

```javascript
	$(function () {
		$('#deleteB').click(function () {
			//remove(): 해당 요소 하나를 삭제
			$('#content> h1:first').remove();
		})
		$('#deleteAllB').click(function () {
			$('#content').empty();
		})
	})
```

---

#### addFile

```javascript
<script type="text/javascript">
var count = 0;
	$(function() {
		$('#addFile').click(function() {
			$("<div id='item'>")
			.append("<input type='file' name='fileup'/>")
			.append("<input type='button' value='삭제'onclick='removeForm(this)'/> ")
			.appendTo('#content');
			
		})
	})
	function removeForm(btn) {
		console.log(btn);
		$(btn).parent().remove();
	}
</script>
</head>
<body>
	<form id='frm' method="post" encType='multipart/form-data'>
		<input type='button' value='파일추가' id='addFile'>
		<article id='content'></article>
	</form>
</body>
</html>
```

---

* $('selector').on('이벤트명', function(){}); => html의 기존 tag만
* $('content').on('이벤트명','selector',function(){}); =>동적으로 추가된 tag도 이벤트 연결

```javascript
$(function(){
/* 	$('#btn1').on('click',function(event){
		console.log('btn1 click... ')
		console.log(event)
		console.log(this) // this: 이벤트가 발생한 대상
	}) */
	$('#btn1').click(function(){
		console.log('btn1 click');
	})
	$('#btn2').click(function(){
		$(this).css('background','pink');
	})
});
```

