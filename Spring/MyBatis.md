# [개념] MyBatis

# **MyBatis**

- Spring Framework에서 제공하는 JDBC 라이브러리를 ‘보다 쉽게’ 작업할 수 있도록 만든 라이브러리
- Mapper의 역할을 확장하여 쿼리문 작성을 ‘모두’ Mapper에서 할 수 있도록 지원함
- Spring Framework의 대표적인 JDBC 라이브러리
- ‘SQL 매핑 프레임워크’
- **반드시 자바 버전 1.8 로 맞춰둘 것**

# **라이브러리 추가**

-mybatis 라이브러리와 mybatis-spring 라이브러리 모두 추가해야 함

-mybatis를 스프링 딴에서 활용 가능하게 만들어 주는 게 mybatis-spring이기 때문

```php
	<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
		<dependency>
			<groupId>org.mybatis</groupId>
			<artifactId>mybatis</artifactId>
			<version>${org.mybatis-version}</version>
		</dependency>

		<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
		<dependency>
			<groupId>org.mybatis</groupId>
			<artifactId>mybatis-spring</artifactId>
			<version>2.0.2</version>
		</dependency>
```

# MyBatis의 핵심 객체들

## 🟦 SQLSessionFactoryBean

- 스프링에 SQLSessionFactory 등록 작업을 SQLSessionFactoryBean이 해준다.
- 이 객체는 mybatis-spring 라이브러리가 제공함.

## 🟦 SQLSessionFactory

- 이 객체가 내부적으로 SQLSession 을 생성한다.
- **JdbcTemplate 대신** 이라고 생각하면 됨
- **MyBatis를 토대로 Jdbc 처리하는 객체**
- 이 객체 빈 등록 시, SQLSessionFactoryBean을 토대로 객체 생성시켜주고, 내부에 DataSource 세팅시켜서 DB와 연동해줌
- 반환은 FactoryBean이 생성한 객체를 getObject() 하여 SQLSessionFactory로 해줌

## 🟦 SQLSession

- 실질적으로 SQLSession 을 통해 Connection 생성하거나 원하는 SQL 전달하고 결과를 리턴받게 된다.

# MyBatis토대로 스프링 DB 처리 절차

## ① 자바 설정 파일에 DataSource 객체 빈 등록

## ② SqlSessionFactory 객체 빈 등록

- SqlSessionFactoryBean에 setDataSource() 토대로 DataSource 객체 주입하여 DB 연동 작업함
- sqlSessionFactory 객체는 SqlSessionFactoryBean이 생성한 객체이므로 getObject() 하여 받고 return 처리

## ③ 데이터 객체 생성

- Scope은 프로토타입으로 생성
- DB 속 테이블 칼럼과 ‘반드시’ 동일 이름의 필드 갖도록 작성할  것. (그러면 @Results 없어도 데이터 간 자동 매핑됨)

```java
@Component
@Scope("prototype")
public class JdbcBean { //데이터 객체
	
	//필드 - DB 속 테이블 컬럼과 '반드시' 동일한 이름으로 해줄 것. (MyBatis 사용)
	private int int_data;
	private String str_data;
	
	//get.set()
	public int getInt_data() {
		return int_data;
	}
	public void setInt_data(int int_data) {
		this.int_data = int_data;
	}
	public String getStr_data() {
		return str_data;
	}
	public void setStr_data(String str_data) {
		this.str_data = str_data;
	}
}
```

## ④ Mapper 인터페이스 생성

- MyBatis에서 Mapper 역할하는 애 : 반드시 **인터페이스로 작성**해야 함
- **이전의  DAO + Mapper의 결합체**
- **DB SQL 관리와 데이터 매핑까지 여기서 모두 처리함**

### 1) 데이터 **매핑 처리 :  @Results**

-DB컬럼 값을 빈 어디에 주입할 지 결정하는 애

-만약 데이터 객체의 필드값이 컬럼 값과 동일한 필드이면 이거 없어도 자동 매핑됨

```java
@Results({
		@Result(column = "int_data", property = "int_data"),
		@Result(column = "str_data", property = "str_data")
	})
```

### **2) SQL문 작성**

-MyBatis 라이브러리 사용 시, **@ 애노테이션으로 간략히 작성 가능**

```java
//MyBatis 사용하면 애노테이션으로 간단하게 sql 작성 가능 
	@Select("select int_data, str_data from jdbc_table")
	List<JdbcBean> select_data(); //이 메소드 실행 시 위의 쿼리문이 실행됨
	
	@Insert("insert into jdbc_table (int_data, str_data) values (#{int_data}, #{str_data}) ")
	void insert_data(JdbcBean bean);

	@Update("update jdbc_table set str_Data = #{str_data} where int_data = #{int_data}" )
	void update_data(JdbcBean bean);
	
	@Delete("delete from jdbc_table where int_data = #{int_data}")
	void delete_data(int int_data);
```

## ⑤ 매퍼로 사용할 Mapper 인터페이스를  MapperFactoryBean에 등록 처리

-스프링에서는 인터페이스는 빈 등록 불가능함

-따라서 MapperFactoryBean에 인터페이스를 set() 처리

```java
// Mapper - 실질적으로 쿼리문 처리 하고 관리함
	@Bean
	public MapperFactoryBean<MapperInterface> test_mapper(SqlSessionFactory factory) throws Exception {
		
		MapperFactoryBean<MapperInterface> factoryBean = new MapperFactoryBean<MapperInterface>(MapperInterface.class);
																																	// 매퍼로 사용할 인터페이스를 세팅
		factoryBean.setSqlSessionFactory(factory);

		return factoryBean;
	}
```

## ⑥ main()에서 mapper 가져와서 SQL 실행

```java
public class MainClass {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(BeanConfigClass.class);
		
		MapperInterface mapper = ctx.getBean("test_mapper", MapperInterface.class);
		
		//insert
		JdbcBean bean2 = new JdbcBean();
		bean2.setInt_data(100);
		bean2.setStr_data("문자열100");
		
		mapper.insert_data(bean2); //DB 세팅
		
		JdbcBean bean3 = new JdbcBean();
		bean3.setInt_data(200);
		bean3.setStr_data("문자열200");
		
		mapper.insert_data(bean3); //DB 세팅  
		
		//update
		JdbcBean bean4 = new JdbcBean();
		bean4.setInt_data(100);
		bean4.setStr_data("문자열300");
		
		mapper.update_data(bean4); 
		
		//delete
		mapper.delete_data(100);
		
		//select
		List<JdbcBean> list = mapper.select_data();
		
		for(JdbcBean bean1 : list) {
			System.out.printf("int_data: %d\n ", bean1.getInt_data());
			System.out.printf("str_data: %s\n", bean1.getStr_data());
			System.out.println("--------------------------------");
		}
		
		ctx.close();
	}
}
```