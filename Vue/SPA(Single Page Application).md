# SPA(Single Page Application)

* 기존 비동기 통신 => 가져올 필요도 없는 내용도 다시 가져온다. response time 길어짐
* 한페이지에 다수 개의 component들의 조립으로 페이지를 구성
* component란?
  * 재사용 가능한 단위(서비스)
  * UI + Data + Behavior
    * UI : 화면
    * Data : 처리할 데이터
    * Behavior : component의 기능들, 메서드
* 프로젝트 생성
  1. vue create 프로젝트명
  2. cd 프로젝트명
  3. npm i --save axios
  4. npm run build
     * 배포 가능한 파일로 정리
  5. npm run serve
     * ui 실행

1. **template**

   * UI 설계

2. **script**

   * Data, Behavior 내용 설계

   * export default => component를 불러쓰는 곳에서 이름을 설정해서 사용 가능

     ```vue
     export default {
      name : 'TodoList',  // name은 디스플레이명으로 실제 이름이 아님 필수요소 X
      data() {			// data
        return {			// 반드시 새로운 객체를 반환해야 한다. 
     					//	component가 자기만의 데이터를 보유하기 위해
          todoItems: []
        };
      },
      created() {
        this.getTodoList();
      },
      methods: {		// data처리 메서드 or UI event 처리 메서드  // behavior
       getTodoList() {
           http.get('/todolist/user/java')
           .then((response)=>this.todoItems = response.data)
           .catch(exp=>alert('처리에 실패하였습니다.'+exp));
       },
       removeTodo(no) {
            http.delete('/todolist/todo/'+no)
            .then()
            .catch(exp=>alert('처리에 실패하였습니다.'+exp));
       },
       checkTodo(no){
            http.put('/todolist/todo/done/'+no)
            .then()
            .catch(exp=>alert('처리에 실패하였습니다.'+exp));
       }
      }
     };
     ```

3. **style**

   * template의 style을 담당 (css)



step1_todolist

* public
  * index.html => single page

* src

  * components

    * 각 component들

  * App.vue

    * 최상위 component

  * main.js

    * 최상위 component인 App.vue와 index.html을 연결시켜주는 역할

    ```
    new Vue({
      render: h => h(App), // h => 화면에 그리는 역할 App => 최상위component 이름
    }).$mount('#app') // id가 app 인 div로 연결
    
    ```

    

* webpack => 브라우저에서 실행 가능한 결과물로 파일 통합해주고 JS 파일 몇개와 index파일 하나로 묶어줌



### Event Bus

---

모든 component들이 공유해서 사용

Bus를 통한 component들의 통신

변화가 발생하면 bus에 신호를 보내 다른 compo들이 그 신호를 보고 판단

` bus.$on('getTodoList',this.getTodoList);` 

이벤트 처리 이름 : getTodoList

해당 이벤트가 발생하면 getTodoList 메서드를 실행시켜라(this.getTodoList)



`@completeTodo="completeTodo"`





* parent componet -> child compo
  * **props를** 이용한 데이터 전달
* child compo -> parent compo
  * event를 발생시켜 데이터를 전송(emit) (event 버스와 유사)