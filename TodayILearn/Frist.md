# Spring Boot에서 application.yml vs application.properties 
------
## 1. 개요
------
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

## 2-1. Propertiec 파일에서 Placeholder 사용
값 내에서 ${} 구문과 함께 자리 표시자를 사용하여 다른 키, 시스템 속성 또는 환경 변수의 내용을 참조 할 수 있습니다.
```
  app.name = MyApp
  app.description = ${app.name} is a Spring Boot application
```

-----
## 2.2 List 구조
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
 ## 2.3 여러 프로필
 
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
 
