# Spring MVC 소개

# **Spring Web MVC**

- Spring Web MVC는 서블릿 API 기반으로 만들어진 웹 프레임워크
- Spring MVC 개발 방식은 (1) XML 이용한 방식 (2) 자바 설정 이용 방식
- 스프링 MVC 프로젝트는 내부적으로 일반 JAVA 영역(POJO) 와 Web 영역을 모두 연동하여 구동함

# **MVC 개념**

- **MVC(Model-View-Controller) 패턴**

: 사용자 인터페이스와 애플리케이션 로직 분리하는 데 사용되는 패턴

**🟧Model :** 데이터 계층 (Java 클래스로 구성)

**🟧Controller :** 요청 처리 (서블릿으로 구성)

**🟧View:** 처리 결과를 보여줌 (JSP로 구성) 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dce6afdd-b7ae-42b0-be4e-fe8d4210ddd2/Untitled.png)

# Model

- 시스템의 비즈니스 로직을 포함하고, 애플리케이션 상태를 나타내는 ‘데이터 계층’

# Controller

- Controller 계층은 View와 Model의 중간 다리 역할
- View 계층에서 요청을 받고, 필요한 유효성 검사를 포함하여 요청을 처리함
- 요청은 데이터 처리를 위해 모델 계층으로 추가 전송되고, 일단 처리되면 데이터는 컨트롤러로 다시 전송된 다음 View에 표시된다.

# View

- 일반적으로 UI 형식. 컨트롤러가 가져온 모델 데이터 표시 용도로 사용된다.