STEP1 spring project 
       오라클 jdbc, HikariCP 데이터베이스 커넥션 풀, SqlSessionFactory 준비

![4](https://github.com/dino-21/step1_spring_project1/assets/80396471/4fe1abbf-47f8-4c47-9e29-1562654e973d)




1.  오라클 포트 9090으로 바꿔주기
cmd로 들어가서 sysdba 권한으로 들어가서 오라클 포트번호를 
9090으로 바꿔주기
system으로 접속해서 book_ex user와 비번지정 및 권한주기
book_ex 사용자와 비번으로 접속하기

2. 스프링프로젝트만들기 ex00

3. STS에서 스프링 프로젝트 깔기
- 자바11, 톰캣 9.0확인
- 메이븐 강제 업데이트 

4. pom.xml  라이브러리 3개 깔기 
  Ojdbc8/Lombok/HikariCP
 메이븐 사이트에서 라이브러리 검색
 https://mvnrepository.com/

5. 한글 깨짐 - 필터 추가 
  web.xml파일수정


6.  Update Maven Project 하기

7. 톰캣에서 Server에서 context수정하기 
http://localhost:8282/controller  삭제
http://localhost:8282/ 로만들기

8. 프로젝트에서 우클릭
Run As > Run on Server 
http://localhost:8282/  
hello world와 날짜시간 나옴

9. JDBCTest.java파일 만들어서 JDBC 연결 
콘솔로 오라클과 연결됐는지 확인


10. HikariCP 데이터베이스 커넥션 풀을 설정하는 부분
   root-context.xml 파일 수정  (HikariCP빈등록)

11. 커넥션 풀 HikariCP
  DataSourceTest.java 작업(어노테이션, 롬복 사용)
  콘솔창에서 DB 커넥션 풀 성공 메시지 확인

12. pom.xml 라이브러리 2개 추가 
    오라클과 자바 객체 매핑 
   -  mybatis, mybatis Spring (3.0.0이상이면 에러)
   메이븐 사이트에서 라이브러리 검색
   https://mvnrepository.com/

13. Update Maven Project 하기



14. SQLSessionFactory 빈 등록하기
root-context.xml 파일에서 아래쪽
> namespaces 클릭> 2개 체크 context, mybatis
체크박스 체크하고 코드에 빈등록하기

15. SqlSessionFactory 작업
MyBatis SqlSessionFactory의 연결을 테스트하는 코드작업
DataSourceTest.java파일 수정하기

16. Mapper 인터페이스 파일 만들기(SQL 쿼리를 정의하고 매핑)
	@Select("SELECT sysdate FROM dual")
	public String getTime();

17. TimetMapperTests.java
Spring과 MyBatis를 통합한 환경에서 TimeMapper의 getTime() 메서드를 테스트하는 클래스
testgetTime 메서드에서 getTime() 메서드를 호출하고 
결과를 로그에 출력한다. (시간나옴)

18. pom.xml에서 log4jdbc-log4j2 설정 
   SQL 쿼리를 직관적 확인하는 라이브러리

19. 로그 설정파일 추가 -log4jdbc.log4j2.properties
log4jdbc.log4j2.properties 파일안에 코드 추가
log4jdbc.spylogdelegator.name=net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator

20. jdbc연결정보 수정 – root-context.xml 파일수정
     <!-- 데이터베이스 드라이버 클래스와 접속 URL 설정 -->
<property name="driverClassName" value="net.sf.log4jdbc.sql.jdbcapi.DriverSpy" />
<property name="jdbcUrl" value="jdbc:log4jdbc:oracle:thin:@localhost:1521:XE" />

21. TestMapperTest.java에서 실행해서 콘솔창에서 sql문 확인하기
 

22. pom.xml  
Servlet 3.1.0 높이고
메이븐 업데이트하기

