# Web(backend)02

### session

* 서버에 사용자의 정보를 저장하기 위한 기법
* request < session < application
* setAttribute(), getAttribute(), removeAttribute(String name), invalidate()
* 세션 종료
  * timeout(5분)
    * tomcat 서버의 web.xml (우선순위 가장 낮음)
    * 프로젝트 web.xml(권장)
    * setMaxInActiveInterval()
  * 사용자가 웹 페이지를 왔다갔다 할때마다 연장

