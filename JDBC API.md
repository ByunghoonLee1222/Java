# JDBC API

* DB 통신 프로토콜은 DB제공사 측에서 클라이언트로 제공(jdbc driver)
* 



#### 클래스를 메모리에 Loading

* **JVM** 
  * 객체를 생성
  * static 속성, 메서드 접근
* **직접**
  1. **class.forName("패키지명.클래스명");**
  
  * 패키지명.클래스명 => Properties 를 이용하여 추가
  
  2. ClassLoader로 직접 로딩



#### Statement

---

Statement s = con.createstatement();

1. Query 분석
2. Query를 수행할 Procedure 생성
3. 프로시져 수행
4. 프로시져 폐기



#### Preparedstatement

---

PreparedStatement ps = con.getPrepareStatement("Query");

1. Query 분석
2. Query를 수행할 Procedure 생성
3. 프로시져 수행
4. 프로시져 저장
5. Statement 보다 빠르다 한번에 Procedure를 생성해놓고 사용

* int executeUpdate(); // insert, update, delete
* ResultSet executeQuery(); // select

```java
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

public class SelectTest {

	public static void main(String[] args) {
		Connection con = null;
		PreparedStatement stmt = null;
		ResultSet rs = null;

		try {
			//2. DB 연결
			con = DBUtil.getConnection(); // Driver loading도 수행
			//3. query 수행을 위한 statement 생성
			stmt = con.prepareStatement(" select * from emp ");
			//4. query 수행
			rs = stmt.executeQuery();
			System.out.println("사원번호\t이름\t급여\t부서번호\t업무");
			//5. 결과 처리 next() : 다음행이 있으면 커서를 다음행으로 이동후 true 리턴, 없으면 false
			while(rs.next()) {
				System.out.printf("%d\t%s\t%d\t%d\t%s\n",rs.getInt("empno")
													  ,rs.getString("ename")
													  ,rs.getInt("sal")
													  ,rs.getInt("deptno")
													  ,rs.getString("job"));
				
			}
		} catch (Exception e) {
			e.printStackTrace();
		}finally {
			DBUtil.close(rs);
			DBUtil.close(stmt);
			DBUtil.close(con); // 가장 바깥을 닫으면 나머지도 close
		}
	}

}
```

