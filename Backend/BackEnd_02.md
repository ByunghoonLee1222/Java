# BackEnd02

#### url pattern : servlet, filter에서 적용

* 시작 문자 : / or *
  * 특정 servlet 연결 : /path/servlet_name  (우선순위 1)
  * folder 기반 연결 : /path/*  (우선순위 2)
  * 확장자 기반 : *.do, *.log ... (우선순위 3)
  * 여기까지의 url은 request를 통해서 수집  **servletPath**
  * queryString : 서버로 전달되는 모든 파라미터 정보
  * parameter : queryString 중에서 특정 파라미터 정보



http://localhost:8080/0924/some/test?name=andy&action=read

* ? 뒤의 문장 = QueryString
* contextPath = /0924
* ServletPath = /some/test



#### ExtensionBaseUrlMapping

* *.do
* 중분류를 나타냄 => 어떤기능을 할건지 나타낸다
* 사용자의 의도를 전달하기 위해서 확장자 기반의 servletPath + 특정 parameter 활용

* ex) board.do?action=insert   : board관련 일 중에서 insert를 할것이다



#### Front controller pattern

* 서버의 얼굴되는 서블릿을 하나 만들고 모든 클라이언트 요청 처리

  

---

### Servlet

* 모든 요청을 받기 위해 **확장자 기반**(*.do) 으로 생성

```java
// annotation의 속성 : key = value
// 언제 value 생략? 사용하려는 속성이 value 딱 하나일때!!
// 배열 표현에서 중괄호 생략?? 배열의 요소가 딱 하나일 때 !!!
@WebServlet("*.do")
@WebServlet({"*.do"})
@WebServlet(value="*.do")
@WebServlet(value={"*.do"})// 모두 가능하다
@WebServlet(value={"*.do","*.check","*.log"}) //확장자 추가도 가능
```



#### JSP Parameter 전달

```jsp
	<a href="board.do?action=read">글읽기</a>
	<form action="board.do" method="get">
		<input type="hidden" name ="action" value="write">
		<input type="submit">
	</form>
```

### session

- 서버에 사용자의 정보를 저장하기 위한 기법
- request < session < application
- setAttribute(), getAttribute(), removeAttribute(String name), invalidate()
- 세션 종료
  - timeout(5분)
    - tomcat 서버의 web.xml (우선순위 가장 낮음)
    - 프로젝트 web.xml(권장)
    - setMaxInActiveInterval()
  - 사용자가 웹 페이지를 왔다갔다 할때마다 연장

