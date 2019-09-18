# Back-End



#### Servlet

---

* **Get**
  * header - 최대 4k 데이터
  * 적은양의 요청 데이터
* **Post**
  * header / body / tail 형태로 전송
  * 많은 양의 데이터 전송 가능
* **요청 데이터 추출 함수**
  * `String getParameter(“name”);` - 하나의 데이터 (get,post)
  * `String getParameterValues(“name”);` - 여러개의 데이터 (get,post)
  * `String getQueryString();` - 한꺼번에 가져온다 (get)



#### JSP (Java Server Pages)

---

* **처리 과정**

  1.  load
  2. Servlet Java 소스파일로 변환되고 다스 클래스 파일로 컴파일(convert)
  3. Instatnce - new 생성
  4. Thread 생성 (invoke)
  5. service

* **Jsp Script 요소**

  * Scriptlet

    * `<%//java code %>`
    * `_jspService(request,response)의 body`로 구현

  * Declaration

    * `<% !속성, 메서드 선언%>` - 선언부에 구현

  * Expression

    * `<%= 내용 %>`

    * 출력
    * `_jspService(request,response)의 body`로 구현

  * Comment
    * `<%-- 	--%>`

* 무거운 단점 => Controller는 Servlet으로  UI는 JSP

* error-page 설정방법

  * web.xml (WEB-INF)

    ```xml
    <error-page>
      	<error-code>404</error-code>
      	<location>/ErrorHandler404.jsp</location>
      </error-page>
    ```

* include

  ```jsp
  <table>
  		<tr>
  		  <td>html include</td>
  		  <td><%@ include file="../FileUpload.html" %></td>
              // html은 글자가 깨진다
  		</tr>
  		<tr>
  		  <td>jsp include</td>
  		  <td><%@ include file="../Login.jsp" %></td>
  		</tr>
  	</table>
  ```



#### JSP 기본객체

---

![JSP기본객체](rsc/Back-End_Servlet,JSP/JSP%EA%B8%B0%EB%B3%B8%EA%B0%9D%EC%B2%B4.PNG)

**시간 순서**

* application => 가장 오래 살아남는다 / 서버 종료 까지
* session => 브라우저 종료까지
* request => 요청이 살아있는동안
* pageContext => JSP의 내장 객체 관리 /가장 짧음



#### ReDirect

---

* Request 정보 유지 X => 새로운 요청 수행 (jsp 로 요청)
  1. 요청 Header
  2. 요청 Data
  3. Cookie
  4. scope에 저장한 Data
* a.jsp => b.jsp(request)
  1. url이 변경
  2. 요청 Data가 유지 X
  3. request scope에 저장한 Data는 유지 x



#### Forward

---

* Request 정보 유지 (jsp 로 요청)
  1. 요청 Header
  2. 요청 Data
  3. Cookie
  4. scope에 저장한 Data



* a.jsp => b.jsp(request)
  1. url이 변경 X
  2. dycjd Data가 유지
  3. request scope에 저장한 Data 유지

* foward 주의사항
  * Insert 사용 시 X 
  * Select 사용 시 O

***Redirect Vs Forward 차이점***

