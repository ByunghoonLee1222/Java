# Spring MVC

#### 흐름도

![springmvc](C:\Users\student\Desktop\springmvc.jpg)



#### mapping

---

  1. mapping
  	- 요청 url에 따른 처리할 controller method를 mapping 시킨다
      @RequestMapping(value='url', method=RequestMethod.XXXX)
   
   **method**
   
      - 요청 방식
      - 어떤 방식으로 요청하던 모두 처리
   
   **value**
   
    - 요청 url
    - 다른 속성이 없으면 생략이 가능하다
   - 형식 ] value="url"
        value="{url, ...}"
   
- spring 4.x에서 추가된	=> pom.xml에서 spring version check

    @GetMapping("url")	: get 방식으로 요청된 경우
    @PostMapping("url"): post 방식으로 요청된 경우

  2. 인자 : 요청 데이터
    	2.1 String
    	* 인자명으로 요청데이터를 추출해서 전달
    	    		ex) String msg
    	    		String msg = request.getParameter("msg");
    	* 인자명에 해당하는 요청데이터가 요청 packet에 없어도
    	    		    요청데이터명은 있지만 데이터가 없어도 error가 발생하지 않음

   2.2 Primitive

* 인자명으로 요청데이터를 추출해서 해당 format으로 변경 후 전달
  ex) int price
     	int price = Integer.parseInt(request.getParameter("price"));
     	

   - 인자명에 해당하는 요청데이터가 요청 packet에 없으면 500 error 발생
        요청데이터명은 있지만 데이터가 없거나 format이 다른경우 400 error 발생

   2.3 @RequestParam  String or Primitive
    	@RequestParam(value='요청데이터명', required, defaultValue)

   	 - value : 추출할 요청 데이터명
      	 - required
      		true : 요청 데이터가 없는 경우 error 발생
      	 - defaultValue : 요청 데이터가 없는 경우 지정한 값으로 전달

   2.4 DTO(Data Transfer Object)
    - 인자의 객체를 기본생성자로 생성 후 객체의 모든 속성을 요청 패키지에서 데이터를 추출 후 
      setter 메서드로 데이터를 설정한다. 마지막으로 첫글자를 소문자로 한 클래스 명으로 request에 저장
      ex) Board b
      Board b = new Board();
      b.setNO(Integer.parseInt(request.getParameter("no")));
      b.setId(request.getParameter("id"));
      b.setTitle(request.getParameter("title"));
      b.setRegDate(request.getParameter("regdate"));
      b.setContents(request.getParameter("contents"));
      request.setAttribute("board",b);