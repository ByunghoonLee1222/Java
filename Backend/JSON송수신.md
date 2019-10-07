# JSON

* gson
* jackson

* 서버단에서 json 생성



* response로 보낼때는 text 

* 따라서 클라이언트로 전송시 이 데이터의 MIME 타입을 설정해 줘야 한다

  ```java
  	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
  		String name = request.getParameter("name");
  		String age = request.getParameter("age");
  		Map<String,Object> resultMap = new HashMap<>();
  		if(name!=null && name.length()>0) { // 성공한 상황
  			Person p = new Person(name,Integer.parseInt(age));
  			resultMap.put("status", "ok");
  			resultMap.put("data", p);
  		}else {			// 실패하는 상황
  			resultMap.put("status", "fail");
  			resultMap.put("data", "name is null");
  		}	
  		// 객체 --> 전송을 위한 문자열로 변환, --> 데이터 구조화를 위해 JSON 채택
  		Gson gson = new Gson();
  		String jsonStr = gson.toJson(resultMap);
  		System.out.println(jsonStr);
  		response.setContentType("application/json;charset=utf-8");
  		response.getWriter().write(jsonStr);
  	}
  ```

  ```jsp
  ///json.jsp//////////
  $("#send").on("click",function(){
  		$.ajax({
  			url:"JSONTest",
  			//type:"get",
  			data:$("#myform").serialize(), // form 내부의 input 요소들을 query string으로..
  			success: function(res){
  				console.log(res);
  			},
  			error: function(){
  				alert("ajax 실패");
  			}
  		})
  	})
  ```



### JSP

---

* java server page

* 서블릿의 최대 단점: business + presentation logic

* presentation 로직에 script를 통해 자바 코드 삽입

* <% scriptlet %>, <%! declaration %>,<%= expression tag%>, <%-- 주석 --%>
  * scriptlet 특징 :_jspService의 로컬 영역에 들어간다!!!
  * declaration : member 변수, 메서드에 대한 선언
  * expression: 출력 전문
  * comment : html comment <!--  --> vs jsp comment? <%--  --%>

  ```jsp
  <body>
  	<%
  		// 로컬 영역
  		int i = 0;
  		// 내장 객체들의 이름은 이미 선점되어있다.
  		//int session = 10;
  		// 내장 객체의 활용
  		out.print(request.getServletPath());
  		out.print(session.getAttribute("loginId"));
  	%>
  	<%! // member 영역에 작성되는 코드
  		int i = 100;
  	%>
  	<%-- 여기서 출력되는 i는 얼마일까요? --%>
  	<!-- i는 로컬 영역의 값이 출력된다. -->
  	<%=i %>
  </body>
  ```



* **directive**

  * page : 이 페이지에 대한 속성 설정

    * contentType
    * import
    * errorPage : 문제가 발생했을 때 문제를 처리해주는 페이지
    * isErrorPage : 에러를 보여주는 페이지 --> exception 내장 객체 추가!!

    `<%@ page  contentType="text/html; charset=UTF-8" import="java.util.*" %>`

    `<%@ page errorPage="sorry.jsp" %>`

  * `@include`:  메서드, 변수등 자바 코드를 재사용, 두개의 jsp가 하나로 묶여서 컴파일

    * ```jsp
      	<%@ include file="snippet.jsp" %>
      	<%=msg %>
      	<%=now() %>
      ```

  * taglib :

* **action tag**

  * `<jsp:include>` : 포함하다! => 화면의 재사용, 필요한 시점에 해당 jsp를 참조한다.
    * `<jsp:include page="header.jsp"></jsp:include>`

* **내장 객체**

  * 내장객체의 종류, 특성

    * pageContext > request > session > application

      javax.servlet.jsp.PageContext

      javax.sevlet.http.HttpServletRequest						servlet

      javax.servlet.http.HttpSession 							// request.getSession()

      javax.servlet.ServletContext  								// request.getServletContext()

*  예외 페이지 연결 처리

*Validation 중요!!! server , client 모두*