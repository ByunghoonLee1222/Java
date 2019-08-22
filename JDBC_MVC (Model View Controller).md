# MVC (Model View Controller)

* web, android, ios ....다양한 OS 로 인한 UI 와 Model을 분리
* UI Processing
* View  |  Controller | Model  패턴 사용 ( 유지보수에 용이)
* **View**
  * *JSP* (back)
  * HTML
  * Javascript
* **Controller**
  * *Servlet*(back)
* **Model**
  * DAO( Data Access Object)
    * DB 서버에 접속해 데이터에 접근
    * Select, Insert, Delete, Update ( table당 1개 )
  * Service
    * Transaction
    * Service에 필요한 기능
    * Network
    * 보안
    * Process(CRUD) 당 1개
  * DTO( Data Transfer Object)
    * table당 1개