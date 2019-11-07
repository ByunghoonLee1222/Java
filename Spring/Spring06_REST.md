# REST(Representational State Transfer)
![img](img/RestFul.JPG)

- Front-End : 사용자의 입력을 받아들어거나 보여주는 역할 (I/O) interaction

  - Browser
  - App (Android , IOS)
  - Back과의 통신
    - HTTP
      - 요청 방식과 URL이 있으면 가능
      - URL - Data

- Back-End

  - Controller - UI와의 완전한 독립을 위해 데이터만 보낸다.
    - XML
    - JSON - XML 보다 파싱하기 쉽고 데이터 양이 적다
    - Primitive
    - CSV

  - service
  - DAO
  - DBMS

```
**MVC**

모델과 뷰의 종속성을 끊어 주기 위한 구조(분리)

뷰는 자주 바뀐다 / 언어에 국한되지 않는 기법
```



uri와 http 메서드를 이용해서 URL 구성

rest 이전 방식  

- http://localhost:8080/selectUser?id=hong

rest 방식

- http://localhost:8080/user/hong + get



**get : url**

- http://localhost:8080/user/hong
- http://localhost:8080/user/

**post : request body**

- http://localhost:8080/user/

**put : url request body**

- http://localhost:8080/user/hong
- http://localhost:8080/user/

**delete: url**

- http://localhost:8080/user/hong

restful 하다



REST API : rest 방식으로 제공되는 api

- 데이터의 전달 --> JSON
- @Controller : 어찌어찌해서 ~ 화면을 준다
- @ResponseBody : view resolver를 거치지 않고 바로 body로 데이터 직행!!
- @RestController : rest 전용의 controller --> 언제나 @ResponseBody : 데이터 응답만 한다
  - view 를 리턴하는 메서드는 생성 불가
- @PathVariable : rest 방식의 url에서 데이터 추출
- @CrossOrigin : S.O.P 대책
- @RequestBody : 파라미터가 json 형태로 전달받으려는 경우
