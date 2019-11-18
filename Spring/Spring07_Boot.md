# Spring  Boot

Legacy Spring의 설정을 자동화 --> 개발자가 보다 비지니스 로직에 집중하도록

**특징**

* jar : 독립적으로 동작하도록 tomcat 내장
  * jsp 구동 불가 ( 풀버전이 아니라 )
* 미리 잘 짜여진 라이브러리 의존성
* main method xxApplication
  - @Configuration
    * 환경설정
    * 추가로 필요한 빈이 있다면 여기 등록
    * 하위 패키지 component scan\

* resources/static
  * 정적 파일 위치(css, js, img, ...)
* application.properties
  * spring boot의 대부분 환경 설정



#### 라이브러리

---

- **Boot**(spring starter project)
- Developer Tools
  - Spring Boot DevTools
- SQL
  - JDBC API
  - MyBatis Framework
  - MySQL Driver
- web
  - Spring web



query.sml의 namespace => com.ssafy.pms.model.dao.PhoneDao

phoneDao => Interface명 / DaoImpl만들지 않아도 됨

