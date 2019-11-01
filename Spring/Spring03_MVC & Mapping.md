# Spring MVC

#### 흐름도

![](C:\Users\student\Desktop\정리\byunghoon\SSAFY_Java\img\springmvc.jpg)

#### mapping

---

1. **mapping**

   - 요청 url에 따른 처리할 controller method를 mapping 시킨다

   - @RequestMapping(value='url', method=RequestMethod.XXXX)

     - *method*
       - 요청 방식
          - 어떤 방식으로 요청하던 모두 처리
        - *value*
             - 요청 url
             - 다른 속성이 없으면 생략이 가능하다
             	- 형식 ] value="url"
               	 		   value="{url, ...}"

   - spring 4.x에서 추가된	=> pom.xml에서 spring version check

     - @GetMapping("url")	: get 방식으로 요청된 경우

     - @PostMapping("url"): post 방식으로 요청된 경우

       

2. **인자** : 요청 데이터

   2.1 **String**

   - 인자명으로 요청데이터를 추출해서 전달
   	 * 		ex) String msg
   	     * 		String msg = request.getParameter("msg");
   	 * 		인자명에 해당하는 요청데이터가 요청 packet에 없어도, 요청데이터명은 있지만 데이터가 없어도 error가 발생하지 않음

   2.2 **Primitive**

   - 인자명으로 요청데이터를 추출해서 해당 format으로 변경 후 전달
   	 *  	ex) int price
   	     *  	int price = Integer.parseInt(request.getParameter("price"));
   	 *  	인자명에 해당하는 요청데이터가 요청 packet에 없으면 500 error 발생
   	 *  	    요청데이터명은 있지만 데이터가 없거나 format이 다른경우 400 error 발생

   2.3 **@RequestParam  String or Primitive**

   * @RequestParam(value='요청데이터명', required, defaultValue)
     * *value* : 추출할 요청 데이터명
     * *required*
        *  		true : 요청 데이터가 없는 경우 error 발생
      * *defaultValue* : 요청 데이터가 없는 경우 지정한 값으로 전달

   2.4 **DTO(Data Transfer Object)**

   * 인자의 객체를 기본생성자로 생성 후 객체의 모든 속성을 요청 패키지에서 데이터를 추출 후 setter 메서드로 데이터를 설정한다. 마지막으로 첫글자를 소문자로 한 클래스 명으로 request에 저장
      *     ex) Board b
             *     Board b = new Board();
             *     b.setNO(Integer.parseInt(request.getParameter("no")));
             *     b.setId(request.getParameter("id"));
             *     b.setTitle(request.getParameter("title"));
             *     b.setRegDate(request.getParameter("regdate"));
             *     b.setContents(request.getParameter("contents"));
             *     request.setAttribute("board",b);

   2.5  **@ModelAttribute("이름") DTO**

   * 인자의 객체를 기본생성자로 생성 후 객체의 모든 속성을 요청 패키지에서 데이터를 추출 후 setter 메서드로 데이터를 설정한다. 마지막으로 지정한 이름으로 request에 저장

   2.6 **@RequestParam Map**

   * 요청 패킷에서 모든 요청 데이터를 추출해서 Map에 요청데이터명이 key, 요청데이터가 value로 해서 데이터 셋팅 후 전달

   2.7 **Servlet API를 인자로**

   * HttpServletRequest, HttpServletResponse, HttpSession, Reader, Writer, ServletInputStream, ServletOutputStream...
   * servlet module 3.0 이상인 경우에만 ServletContext를 인자로 받을 수 있다

   2.8 **Model을 인자로**

   - Model은 인터페이스이므로 인자로만 받을 수 있다
   - service를 수행한 결과를 Model에 저장하면 request에 저장한 효과이다

   2.9 **MultipartFile**

   * 업로드된 파일 정보
   * pom.xml에 파일과 관련된 라이브러리를 추가
     * commons-io-xxx.jar
     * commons-fileupload-xxx.jar
   * web을 위한 bean configuration에 multipartResolver를 추가
   * multipartResolver는 요청 데이터에서 파일 정보만 추출해서 MultipartFile로 전달

   

3. **리턴** : View에 대한 정보

   3.1 **String**

   - 이동할 View에 대한 url을 문자열로
   	 *    	  forward	:	"url"	or	"foward:url"
   	 *    	  redirect	:	"redirect:url"

   3.2 **void**

   * 요청 url에서 .이후를 제거한 이름을 view로 인식해서 등록된 이름의 view로 이동
    * ViewResolver를 설정해서 view 이름을 완성해야 한다
      * ex) @PostMapping("insertBoard.log")인 경우 view 이름은 insertBoard

   3.3 **DTO => REST Ful**

   - REST는 Representational State Transfer라는 용어의 약자로서 **웹의 장점을 최대한 활용할 수 있는 아키텍처**

   * XML 이나 Json 데이터로 출력
   * jackson-databind-xxx.jar

   3.4 **ModelAndView**

   * 모델을 수행한 결과 정보와 View 정보를 표현하는 객체

   

4. **예외 처리**

   * 현재 컨트롤러에서 발생한 오류를 처리
   * 형식]
     * @ExceptionHander
     * public 리턴타입 함수명(Exception e){ }

