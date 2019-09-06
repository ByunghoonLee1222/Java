# JavaScript

```javascript
<script type="text/javascript">
	<!-- 알림창 -->
	alert('알림창입니다.');
	<!-- 콘솔에 출력 -->
	console.log('콘솔에 출력하기');
	
</script>
```

```javascript
<title>script 사용하는 방법 3가지</title>
<!-- 1.file로 작성된 js 적용 -->
<script type="text/javascript" src="../test2.js"></script>
<script type="text/javascript" src="../js/test.js"></script>
<!-- 2.html 내부에서 script 선언 -->
<script type="text/javascript">
	console.log('html 내부에서 script 작성...');
</script>
</head>
<!-- head에서 작성한 함수를 body에서 호출 -->
<body onload='alert("body tag에서 수행")'>
	<script type="text/javascript">
		console.log('body 내부에서 script 작성')
	</script>
	<a href="javascript:alert('a tag에서 수행')">script 수행</a>
	<a href="#" onclick="alert('a tag에서 수행')">script 수행</a>
</body>
```

```javascript
	function openWindow(){
		//open (url,창이름, 옵션) 옵션은 299page 참조
		var newWind = window.open('../chapter11/addFileForm.html'
									,'','width=300,height=300,location="no"');
		newWind.moveTo(window.screenX+event.clientX, screenY+event.clientY);
	}
////////////////////////////////////////////////
window.onload=function(){
	//현재 창을 띄운 창(opener)에서 id를 찾아 오기
	var openerId = opener.document.getElementById('id');
	var id = document.getElementById('id');
	id.value = openerId.value;
	
	var selectId = document.getElementById('selectId');
	addEvent(selectId, 'click',useId);
}
function useId(){
	//Opener : 새창을 띄워준 창 
	var openerId = opener.document.getElementById('id');
	var id = document.getElementById('id');
	openerId.value = id.value;
	self.close();  //현재 창 닫기
}
////////////////////////////////////////////////
	function addContent() {
		var content = document.getElementById('content');
		//innerHTML : 태그 바디
	//	content.innerHTML +='<h1>hello</h1>';
		//innerTEXT : 태그 바디를 문자로
		content.innerText +='<h1>hello</h1>';
	}
/////////////////////////////////////////
```

#### event

```javascript
function eventHandle(){
	var content = document.getElementById('content');
	content.innerHTML='Hello';
}
function eventHandle2(){
	var content = document.getElementById('content');
	content.innerHTML='';
}
/////////////////////////////////////////////////
	window.onload = function() {
		var click = document.getElementById('click');
		click.onclick = function() {
			var content = document.getElementById('content');
			content.innerHTML += '<h2>hello</h2>';
		}
		var clear = document.getElementById('clear');
		clear.onclick = eventHandler;
	}
	function eventHandler() {
		var content = document.getElementById('content');
		content.innerHTML = '';
	}
///////////////////////////////////////////////////
	window.onload = function() {
		var click = document.getElementById('click');
		click.addEventListener('click', function(e) {
			console.log(this); // this => event 처리하는 함수에서 this는 event가 발생한 대상
			var content = document.getElementById('content');
			content.innerHTML = '<h2>hello</h2>';
		})
		var cancel = document.getElementById('cancel');
		cancel.addEventListener('click',eventHandler);
	}
	
	function eventHandler() {
		var content = document.getElementById('content');
		content.innerHTML='';
	}
```

