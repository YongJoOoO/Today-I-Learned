# MVC에 MyBatis 연동

# MyBatis

- JDBC : Java 언어 이용하여 데이터베이스 연동하는 프로그래밍 기술
- MyBatis는 JDBC 프로그래밍 보다 쉽게 구현하기 위해 설계된 라이브러리

---

### **📍 MyBatis 사용을 위한 세팅 →**

# Properties 파일 작성

- 데이터베이스 접속 정보를 갖는 properties 파일을 작성해야 한다.

### **▶️ 오라클 DB 연동**

```xml
database.classname = oracle.jdbc.OracleDriver
database.url = jdbc:oracle:thin:@localhost:1521:orcl
database.username = scott
database.password = 1234
```

# Mapper 인터페이스 생성

- **Mapper 파일** : 쿼리문 작성 파일
- 추후 MyBatis 세팅할 때, 어떤 Mapper 파일을 사용할 것인지 정해주어야 하므로 미리 만들어 줌.

```java
public interface MapperInterface {
  @Insert("insert into SpringMVCTable (data1, data2, data3) values (#{data1}, #{data2}, #{data3})")
  void insert_data(DataBean1 dataBean1);

  @Select("select data1, data2, data3 from SpringMVCTable")
  List<DataBean1> select_data();
}
```

# **BasicDataSource Bean 빈 등록**

- **BasicDataSource 객체** : DB 접속 정보 관리 객체

```java
@Bean
public BasicDataSource dataSource() {
    BasicDataSource source = new BasicDataSource();
    source.setDriverClassName(database_classname);
	  source.setUrl(database_url);
	  source.setUsername(database_username);
    source.setPassword(database_password);
 
    return source;
}
```

# SqlSessionFactory Bean 빈 등록

- **SqlSessionFactory 객체** : DB 접속, 쿼리 관리 객체

```java
//쿼리문과 접속 관리하는 SqlSessionFactory 등록하기
	@Bean
	public SqlSessionFactory factory(BasicDataSource source) throws Exception{
		SqlSessionFactoryBean factoryBean = new SqlSessionFactoryBean();
		factoryBean.setDataSource(source);
		SqlSessionFactory factory = factoryBean.getObject();
		
		return factory;
	}
```

# **Mapper Bean 빈 등록**

- **쿼리문을 관리할 Mapper를 빈으로 등록**한다
- 이 Mapper를 주입받아서 실질적인 쿼리를 실행하게 된다.
- 인터페이스 자체는 빈 등록 안되므로 MapperFactoryBean에 인터페이스를 set() 처리함

```java
//쿼리문 실행을 위한 객체 : Mapper - 단, 인터페이스는 빈 등록 안되므로 다르 방식으로 등록
	@Bean
	public MapperFactoryBean<MapperInterface> test_mapper(SqlSessionFactory factory) throws Exception{
		MapperFactoryBean<MapperInterface> factoryBean = new MapperFactoryBean<MapperInterface>(MapperInterface.class);
		factoryBean.setSqlSessionFactory(factory);
		return factoryBean;
	}
```

---

### **📍 실질적인 DB 사용**

# Mapper 주입받기

- 쿼리 동작시켜야 하는 곳에서 Mapper를 주입받을 것.

# **main() 에서 쿼리 실행**

- 필요한 쿼리를 주입받은 Mapper를 토대로 실행한다.