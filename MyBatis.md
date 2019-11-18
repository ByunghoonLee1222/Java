# MyBatis

개발자가 지정한 SQL, 저장프로시저 그리고 몇가지 고급 매핑을 지원하는 퍼시스턴스 프레임워크

 JDBC로 처리하는 상당부분의 코드와 파라미터 설정및 결과 매핑을 대신해준다

sqlMapConfig.xml => MyBatis 환경설정

Board_query.xml

Member_query.xml => SQL Query

MyBatis.java => MyBatis 연동하는 클래스

DBCP => 동시접속



mybatis type => mybatis-3.2.8.jar =>ibatis.type =>TypeAliasRegistry.class

* <insert id=" "ParameterType = " " -> Data Setting할 Type
* ParameterMap = " "  -> 

* query

  * insert into member(id,password,name,email) values ( #{id},#{password},#{name},#{email}) =>객체의 속성명
  * `<select id=" " parameterType="string" resultType="member">`
    * select * from member ( * => 원할 시 member 객체 속성명)

  ```xml
  <!--여러 도메인을 위한 쿼리 xml를 작성할 때  도메인을 식별하기 위해 
      namespace 부여 
  => sqlSession.쿼리메서드("식별자", paramdata);
      식별자 =>  namespace.id
    ex)sqlSession.insert("member.insert", member);    
    ex)sqlSession.selectOne("member.search", no);    
  -->	
  <mapper namespace="member" >
     <!--
        insert나 update에 대한 데이타 설정시 버그가 발생하므로 
        문제를 해결하기 위해 데이타 설정시 #{속성:JDBCType} 으로 한다. 
      org.apache.ibatis.type.JdbcType에서 확인
        문자열 VARCHAR
        정수   INTEGER
        실수   DOUBLE
  	-->
     <insert id="insert"		parameterType="member">
     		insert into member (id, password, name, email, address)
     		values ( #{id:VARCHAR}
     		        ,#{password:VARCHAR}
     		        ,#{name:VARCHAR}
     		        ,#{email:VARCHAR}
     		        ,#{address:VARCHAR})
     </insert>
     <delete id="delete" 		parameterType="string">
     		delete from member where id=#{id}
     </delete>
     <update id="update"		parameterType="member">
     		update member set password=#{password:VARCHAR}
     		                , name = #{name:VARCHAR}
     		                , email= #{email:VARCHAR}
     		                , address=#{address:VARCHAR}
     		where  id = #{id:VARCHAR}
     </update>
     
     <select id="search"		 parameterType="string"    resultType="member">
     		select * from member  where id=#{id}
     </select>
     
     <select id="searchAll"	parameterType="pagebean"	resultType="member">
     		select * from member 
     		<!-- 동적 쿼리시 조건에 의해 where 나 and를 붙여주는 태그  -->
     		<where>
     			<if test='key != null and key!="all"'>
     				<if test=" word != null">
     					<choose>
     						<when test="key == 'id'">
     							id = #{word}
     						</when>
     						<when test="key == 'address'">
     							address like  concat('%',#{word},'%')
     						</when>
     					</choose>
     				</if>
     			</if>
     		</where>
     		order by id 
     </select>
     <select id="count"	resultType="int"	parameterType="pagebean">
     		select count(*) as cnt from member
     		<where>
     			<if test=' key != null and key!="all" '>
     				<if test=" word != null ">
     					<choose>
     						<when test=" key == 'id' ">
     							id = #{word}
     						</when>
     						<when test=" key == 'address' ">
     							address like  concat('%',#{word},'%')
     						</when>
     					</choose>
     				</if>
     			</if>
     		</where>
     </select>
  </mapper>
  ```

  

* selectList => 2개 이상

* selectMap, SelectOne(DTO있을 때) => 1개 

* configuration

```xml
<configuration>
  <!-- mapper에서 사용할 타입(parameterType, resultType)  설정
  	   org.apache.ibatis.type.TypeAliasRegistry
  	     - 기본 타입에 대한 alias 설정
   -->
  <typeAliases>
    <typeAlias type="com.ssafy.model.dto.Member" 	alias="member"/>
    <typeAlias type="com.ssafy.model.dto.PageBean"	alias="pagebean"/>
    <typeAlias type="com.ssafy.model.dto.Board"	alias="board"/>
    <typeAlias type="com.ssafy.model.dto.FileBean"	alias="filebean"/>
  </typeAliases>
  <environments default="development">
     <environment id="development">
        <transactionManager type="JDBC"/>
        <dataSource type="POOLED">
              <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
          <property name="url" value="jdbc:mysql://localhost:3306/ssafydb?serverTimezone=UTC&amp;useSSL=false&amp;allowPublicKeyRetrieval=true"/>
          <property name="username" value="ssafy"/>
          <property name="password" value="ssafy"/>
        </dataSource>
     </environment>
  </environments>
  <mappers>
         <mapper resource="com/ssafy/config/Member_query.xml"/>
         <mapper resource="com/ssafy/config/Board_query.xml"/>
  </mappers>
</configuration>
```

