# Back-end

client - server(WAS) 간의 통신 

Get 방식 - default (utf-8) 설정 불필요

Post 방식 - (UTF-8 설정 필요)

* **request ( client => server )**
  * Parameter
  * attribute
  * Cookie
* **response ( server => client )**
  * Stream
  * Cookie



* Tomcat은 WebContent에만 관여

* **Servlet url pattern=> / or *. 로만 시작**



#### 절대경로 vs 상대경로

---

http://localhost:8080/0919/form.html

* / => 절대경로
* container root : http://localhost:8080/       : html , jsp , sendRedirect
* context root : http://localhost:8080/0919/ : servlet, forward, filter



* 상대경로 
  * . => 현재 root 부터 시작

```html
	<h1>by get</h1>
	<!-- 절대경로로 서블릿 호출 -->
	<form action="/0919/sub/form" mehtod="get">
		<input type="text" name="name">
		<input type="submit">
	</form>
	
	<h1>by post</h1>
	<!-- 상대경로로 서블릿 호출 -->
	<form action="./sub/form" mehtod="post">
		<input type="text" name="name">
		<input type="submit">
	</form>
```



#### Filter

---

* Servlet이 수행할 공통작업 (전처리(요청), 후처리(응답))

* 응답할 때도 필터를 거쳐 간다

* encoding
* 기능
* session



#### MVC

---

1. parameter 확인
2. model 연동
3. view 연결



#### Forward VS Redirect

---

* **forward**
  * request, response 전달 O
  * 요청 1번
  * 최초 요청한 URL 유지
  * request 에서 설정한 방식으로 (get, post)
* **sendRedirect**
  * request, response 전달 X
  * 요청 2번
  * 새로운 URL을 가지고 있다.
  * **Get 방식만 가능**

#### Parameter VS Attribute

---

* parameter
  * 최초에 request가 만들어질 때만 생성 이후에는 추가할 수 없다
  * network로 전송 --> String
* attribute
  * 계속 추가 가능
  * 서버의 JVM에서 동작 --> 모든 데이터를 다 관리 가능(객체 관리)

* 서버에서 attribute를 관리할 수 있는 요소들
  * PageContext < HttpServletRequest < HttpSession < ServletContext => Servlet에서
  * page < request < session < application  => JSP에서



* xx.setAttribute(String key, Object v);
* Object xx.getAttribute(String key)
* xx.removeAttribute(String key)

