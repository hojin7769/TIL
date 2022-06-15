# Spring Boot에서 application.yml vs application.properties 

## 목차   
 1. [개요](#1개요)   
 2. [속성 구성](#2-속성-구성)   
  2-1.[Propertiec 파일에서 Placeholder 사용](#2_1-propertiec-파일에서-placeholder-사용)   
  2-2. [List 구조](https://github.com/hojin7769/TIL/edit/main/TodayILearn/Frist.md#2-2-list-%EA%B5%AC%EC%A1%B0)   
  2-3. [여러 프로필](https://github.com/hojin7769/TIL/edit/main/TodayILearn/Frist.md#23-%EC%97%AC%EB%9F%AC-%ED%94%84%EB%A1%9C%ED%95%84)   
  2-4. [여러 파일의 프로필](https://github.com/hojin7769/TIL/edit/main/TodayILearn/Frist.md#24-%EC%97%AC%EB%9F%AC-%ED%8C%8C%EC%9D%BC%EC%9D%98-%ED%94%84%EB%A1%9C%ED%95%84)   
 3. AML 구성   
  3-1. [YAML 형식](https://github.com/hojin7769/TIL/edit/main/TodayILearn/Frist.md#31-yaml-%ED%98%95%EC%8B%9D)   
  3-2 [List 구조](https://github.com/hojin7769/TIL/edit/main/TodayILearn/Frist.md#32-list-%EA%B5%AC%EC%A1%B0)   
  3-3 [여러 프로필](#33-여러-프로필)   
 4 [YAML의 값 참조](#yaml의-값-참조)   
  
------
## 1.개요
Spring Boot의 일반적인 관행은 [외부 구성](http://daplus.net/java-spring-boot-%EB%B0%8F-%EC%97%AC%EB%9F%AC-%EC%99%B8%EB%B6%80-%EA%B5%AC%EC%84%B1-%ED%8C%8C%EC%9D%BC/)을 사용하여 속성을 정의하는 것 입니다.
이를 통해 다른 환경에서 동일한 애플리케이션 코드를 사용할 수 있습니다.
속성 파링 , YAML 파일, 환경 변수 및 명령 줄 인수를 사용할 수 있습니다.

-----
## 2. 속성 구성
기본적으로 Spring Boot는 key-value 형식을 사용 하는 aplication.properties 파일에 설정된 구성에 엑세스 할 수 있습니다.
 ```
  spring.datasource.url=jdbc:h2:dev
  spring.datasource.username=SA
  spring.datasource.password=password
 ```
 여기에서 각 라인은 단일 구성입니다. 따라서 키에 동일한 접두사를 사용하여 계층 적 데이터를 표현해야 합니다. 그리고 예에서 모든 키는 spring.datasource에 속합니다.

------

### 2_1. Propertiec 파일에서 Placeholder 사용
값 내에서 ${} 구문과 함께 자리 표시자를 사용하여 다른 키, 시스템 속성 또는 환경 변수의 내용을 참조 할 수 있습니다.
```
  app.name = MyApp
  app.description = ${app.name} is a Spring Boot application
```

-----
### 2-2 List 구조
값이 다른 동일한 종류의 속성이있는 경우 배열 인덱스로 List 구조를 나타낼 수 있습니다.
 ```
  application.servers[0].ip=127.0.0.1
  application.servers[0].path=/path1
  application.servers[1].ip=127.0.0.2
  application.servers[1].path=/path2
  application.servers[2].ip=127.0.0.3
  application.servers[2].path=/path3
 ```
 
 -----
 ### 2.3 여러 프로필
 
 버전 2.4.0 부터 Spring Boot는 다중 문서 속성 파일 생성을 지원합니다. 간단히 말해, 하나의 실제 파일을 여러 논리 문서로 분할 할 수 있습니다.
 이를 통해 선언해야하는 각 프로필에 대한 문서를 모두 동일한 파일에 정의 할 수 있습니다.
 ```
   logging.file.name=myapplication.log
  bael.property=defaultValue
  #---
  spring.config.activate.on-profile=dev
  spring.datasource.password=password
  spring.datasource.url=jdbc:h2:dev
  spring.datasource.username=SA
  bael.property=devValue
  #---
  spring.config.activate.on-profile=prod
  spring.datasource.password=password
  spring.datasource.url=jdbc:h2:prod
  spring.datasource.username=prodUser
  bael.property=prodValue
 ```
 문서를 분할 할 위치를 나타 내기 위해 '#----' 표기법을 사용합니다.
 이 예에서는 태그가 다른 프로파일을 가진 두 개의 스프링 색션이 있다. 또한 루트 수준에서 공통 속성 집합을 가질 수 있습니다.
 이 경우 logging.file.name 속성은 모든 프로필에서 동일합니다.
 
 ------
 
 ### 2.4 여러 파일의 프로필
 > 동일한 파일에 다른 프로필을 갖는 대신 다른 파일에 여러 프로필을 저장할 수 있습니다. 버전 2.4.0 이전에는 속성 파일에 사용할 수 있는 유일한 방법이 있다.
 > 예를 들어 application-dev.yml 또는 application-dev.properties 와 같은 파일 이름에 프로필 이름을 입력하면 된다.

------
 ## 3. YAML 구성
 
 ### 3.1 YAML 형식
 ------
 > Java 속성 파일뿐만 아니라 Spring Boot 애플리케이션에서 YAML 기반 구성 파일을 사용할 수도 있습니다
 > properties와 다르게 계층 구조로 표현 하여 prefix의 중복 제거가 가능해지고 가독성이 좋다
 > ***YAML은 계츨적 구성데이터를 지정하기 위한 편리한 형식입니다***
 > 이제 속성 파일에서 동일한 예를 가져와 YAML로 변환해 보겠다.
 ```
  spring:
    datasource:
        password: password
        url: jdbc:h2:dev
        username: SA
 ```
 반복되는 접두사가 포함되지 않으므로 대체 속성 파일보다 더 읽기 쉽습니다.
 
 ------
 ### 3.2 List 구조
 YAML에서는 List을 표현하기 위한 보다 간결한 형식이 있다.
 ```
  application:
    servers:
    -   ip: '127.0.0.1'
        path: '/path1'
    -   ip: '127.0.0.2'
        path: '/path2'
    -   ip: '127.0.0.3'
        path: '/path3'
 ```     
 ------
 ### 3.3 여러 프로필
 속성 파일과 달리 YAML은 설계에 따라 다중 문서 파일을 지원하므로 사용하는 Spring Boot 버전에 관계없이 동일한 파일에 여러 프로필을  저장할 수 있다.
 그러나 이 경우 사양은 ***새 문서의 시작을 나타내기*** 위해 ***세개의 대시를 사용해야 함을 나타냅니다.**
 ```
   logging:
  file:
    name: myapplication.log
---
spring:
  config:
    activate:
      on-profile: staging
  datasource:
    password: 'password'
    url: jdbc:h2:staging
    username: SA
bael:
  property: stagingValue
 ```
 ------
 # YAML의 값 참조
 아래와 같은 application.yml이 정의된 상태라고 가정
 ```
 external:
	record-year: 2021
	api:
		name: kakao
		key: 123123
 ```
 ## @value
 > @value 어노테이션을 사용하여 값을 주입할 수 있다.
  ```
  public class ExternalService{
    @Value("${external.record-year}")
	private String recordYear;
  
	@Value("${external.api.name}")
	private String apiName;
  
	@Value("${external.api.key}")
	private Integer apiKey;
}
 ```
 ------
 ## Environment
Environment api를 사용하여 .getProperty("key") 메서드로 값을 가져올 수 있다.
```
@Autowired
private Environment env;

private String apiName = env.getProperty("external.api.name")
 ```
 ------
 ## @ConfigurationProperties
 @ConfiguartionProperties 어노테이션을 사용해 구조화 된 개체에 바인딩 할 수도 있다.   
 @ConfigurationProperties 의 value 로 prefix를 적어줘야 한다. 중첩 클래스 (ex.Api)를 사용하게 되는 경우 이름을 똑같이 일치시켜야 하고 setter를 반드시 정의해주어야 함.
 
 ```
 @ConfigurationProperties("external")
public class ConfigProperties{
    String recordYear;
    String Api api;
    
    @Getter
    @Setter
    public static class Api {
        private String name;
        private Integer key;
    }
}
```
------
## 프로퍼티 우선순위
 프로퍼티를 설정할 수 있는 방법은 여러가지이며 각 방법마다 우선순위가 있다. 여러 방법으로 같은 프로퍼티를 정의하고 있으면 우선순위가 가장 높은 방법으로 정의한 프로퍼티 값이 오버라이딩 된다.
 ### 우선순위
 
 1. 유저 홈 디렉토리에 있는 spring-boot-dev-tools.properties
2. 테스트에 있는 @TestPropertySource
3. @SpringBootTest 애노테이션의 properties 애트리뷰트
4. 커맨드 라인 아규먼트
5. SPRING_APPLICATION_JSON (환경 변수 또는 시스템 프로티) 에 들어있는 프로퍼티
6. ServletConfig 파라미터
7. ServletContext 파라미터
8. java:comp/env JNDI 애트리뷰트
9. System.getProperties() 자바 시스템 프로퍼티
10. OS 환경 변수
11. RandomValuePropertySource
12. JAR 밖에 있는 특정 프로파일용 application properties
13. JAR 안에 있는 특정 프로파일용 application properties
14. JAR 밖에 있는 application properties
15. JAR 안에 있는 application properties
16. @PropertySource
17. 기본 프로퍼티 (SpringApplication.setDefaultProperties)

### application.properties 의 우선순위
application.properties를 같은 위치가 아니라 다른 위치에 둘 경우는 컴파일해도 덮어쓰지 않게된다.

이 때 우선순위는 아래와 같다.

1. file:./config/ :프로젝트 디렉토리 바로 아래에 config라는 디렉토리를 만들고 그 안에 application.properties 만들어주는 방법
2. file:./ :프로젝트 루트 바로 아래에 application.properties 만들어주는 방법
3. classpath:/config/ :classpath 아래에 config라는 디렉토리를 만들고 그 안에 application.properties 만들어주는 방법
4. classpath:/ :classpath 아래에 application.properties 만들어주는 방법

# 참조 사이트
[Using application.yml vs application.properties in Spring Boot](https://www.baeldung.com/spring-boot-yaml-vs-properties)
[Spring Boot에서 properties 값 주입받기](https://bottom-to-top.tistory.com/46)
[Application.propertices](https://velog.io/@max9106/Spring-Boot-%EC%99%B8%EB%B6%80%EC%84%A4%EC%A0%95-uik69crax3)
