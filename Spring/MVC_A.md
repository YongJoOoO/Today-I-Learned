# Spring MVC 프로젝트 구조

# MVC

- MVC는 Model, View, Controller 분리하여 개발함
- 현재 가장 多 사용 중인 개발 패턴
- 서비스를 위해 각 부분을 분리해서 만들고, 이를 통해 개발 및 유지 보수 효율성 높이는 것이 목적

 → **Model** : 데이터 관리하는 부분

 → **View :** 눈에 보이는 부분 구성

 → **Controller :** 요청에 따른 코드 흐름 제어하는 부분

# MVC 프로젝트에서 필요한 Bean 정의

**@Bean** : 메소드를 통해 반환 객체를 Bean으로 등록시킴

**@Component** : 개발자가 만든 클래스 중 아직 빈으로 등록하지 않은 객체를 Scan. Bean 자동 등록함

- **@Controller** : Component의 일종으로, 사용자 요청에 따라 자동 호출 메소드를 갖는 Bean을 등록
- **@RestController** : Component의 일종으로, 사용자 요청에 따라 자동 호출되는 메소드 가지고 있는 Bean 등록함. **Restful API 서버 구성 시 사용**
- **@Service** : Component의 일종으로, Controller에서 호출하는 메소드를 가지고 있는 Bean을 정의
- **@Repository** :  Component의 일종으로, @Service로 정의한 Bean에서 호출하는 메소드를 갖는 Bean 정의함. 이  빈은 **DB 관련 작업을 구현**함.
- **@ConrollerAdvice** : 예외 발생 시 사용할 Global Exception Handler로 사용할 Bean을 등록
- <img width="428" alt="img" src="https://user-images.githubusercontent.com/39732720/169420436-2cbf06a0-f967-4755-b9ff-5405fd826217.png">
