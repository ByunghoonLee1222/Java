# Front-end

* jQuery -> form 처리

  * $(선택자) => jQuery 객체

* jquery의 용도

  * 속성 편집

    * text()
    * html()
    * val()
    * attr() - html이 가지고 있는 속성(고정적)
    * prop() - javascript 속성 (유동적)

    ```html
    //jquery 객체 vs dom 객체
    	console.log(document.querySelector("#first"));
    	let domObj = document.querySelector("#first");
    	console.log($("#first").get(0)); 
    	let jqueryObj = $("#first");
    	
    	console.log(domObj.innerHTML);
    	console.log(jqueryObj.html());
    	
    	//input 요소의 값
    	console.log($("#id").val());
    	
    	//attr,prop
    	let checkBox = $("#check");
    	console.log(checkBox.attr("checked")+" : "+checkBox.prop("checked"));
    ```

    

  * dom 편집

    * before() - 형제 레벨 앞에 추가
    * after() - 형제 레벨 뒤에 추가
    * append() - 자식레벨로 뒤에 추가
    * prepend() - 자식레벨 앞에 추가
    * empty() - 해당 내용 삭제(clear)

    ```html
    	$("#btn1").on("click",function(){
    		$("#first").before("<h1>before</h1>");
    		$("#first").after("<h1>after</h1>");
    		
    		$("#first").append("<h1>append</h1>");
    		$("#first").prepend("<h1>prepend</h1>");
    	});
    ```

    

  * 이벤트 처리

    * on - 이벤트 처리

    ```html
    $("#btn1").on("click",function(){
    		$("#first").before("<h1>추가됨</h1>");
    	});
    ```



#### ajax

---

```html
<body>
	<h1>더해주세요.</h1>
	<!-- form을 이용한 submit: 동기 방식으로 하면 전체가 클라이언트에게 전달 -->
	<form id="addForm" action="CalcServlet">
		<input type="number" name="num1" id="num1">
		<input type="number" name="num2" id="num2">
		<input type="submit" id="calc" value="sync">
	</form>
		<input type="submit" id="calc2" value="async">
	<h1>계산결과</h1>
	<ul id="result">
		
	</ul>
</body>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
<script>
	//calc2에 클릭 이벤트 등록
	$("#calc2").on("click",function(){
		$.ajax({
			url:"CalcServlet",	// servlet or jsp 경로
			//type:"get", get방식이면 생략해도 무방 // get or post, default: get
		//	data:"num1="+$("#num1").val()+"&num2="+$("#num2").val(),//서버로 전송할 data: string( key=value&key=value), json 객체
			data: $("#addForm").serialize(), // 쿼리스트링 자동 완성
			success: function(resTxt){
				//console.log(resTxt);
			//	$("#result").empty();
				$("#result").append("<li>"+$("#num1").val()+"+"+$("#num2").val()+"="+resTxt);
			},
			error: function(){
				alert("계산 실패");
			}
		});
	});
</script>
```

### boxoffice 조회

---

```html
<body>
	<h1>박스오피스 조회</h1>
	<input type="date" id="date">
	<input type="button" id="get" value="조회">
	<h2>조회 결과</h2>
	<table border="1">
		<thead>
			<tr>
				<th>rank</th>
				<th>title</th>
			</tr>
		</thead>
	<tbody></tbody>
	</table>
</body>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
<script>
	//id가 get인 버틍니 클릭될 때 date의 값을 console에 출력하세요.
	$("#get").on("click",function(){
		// 선택된 값이 없을 경우에는 선택 alert, 아니면 풀력
		let date = $("#date").val();
		if(date){
			let targetDt = date.replace(/-/gi,""); //정규표현식, - => 삭제
			console.log(targetDt);
			//제대로 값이 왔다면 --> ajax 호출
			$.ajax({
				url: "http://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json?key=430156241533f1d058c603178cc3ca0e",
			//	type: "",
				data: "targetDt="+targetDt,
				success: function(resTxt){
			//		console.log(resTxt);
					let list = resTxt.boxOfficeResult.dailyBoxOfficeList;
					console.log(list);
					$("tbody").empty();
					list.forEach(function(item){
						//console.log(item);
						$("tbody").append("<tr><td>"+item.rank+"</td><td>"+item.movieNm+"</td></tr>")
					})
				},
				error: function(){
					alert("정보 조회 실패");
				}
			});
		}else{
			alert("date를 선택하세요.");
		}
	})
</script>
```

