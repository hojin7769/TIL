# Mavern vs Gradle

![image](https://gradle.org/images/gradle-vs-maven.gif)

-------

## Maven

> Apache의 이름 아래 2004년 출시   
> [Ant](https://k39335.tistory.com/53)를 사용하던 개발자들의 불편함을 해소 + 부가기능 추가   
> ***Maven은 무엇인가?***
> - 빌드를 쉽게 (Making the build process easy)
> - pom.xml을 이용한 정형화된 빌드 시스템
> -뛰어난 프로젝트 정보 제공 (Providing quality project information)
>   - Change log document created directly from source control ( 소스 제어에서 직접 작성된 로그 문서 변경)
>   - Cross referenced sources (상호 참조된 소스)
>   - Mailing lists (메일 목록)
>   - Dependency list(의존성 목록)
>   - Unit test reports including coverage (커버리지를 포함한 단위 테스트 보고서)
>  - 개발 가이드 라인 제공 (Providing guidelines for best practices development)
>   - Keeping your test source code in a separate, but parallel source tree (테스트 소스 코드를 별도의 병렬 소스 트리에 보관)
>   - Using test case naming conventions to locate and execute tests(테스트 사례 명명 규칙을 사용하여 테스트 찾기 및 실행)
>   - Have test cases setup their environment and don’t rely on customizing the build for test preparation. 
(테스트 사례를 통해 환경을 설정하고 테스트 준비를 위해 빌드를 사용자 정의할 필요가 없습니다.)
>  - 새로운 기능을 쉽게 설치할 수 있고 업데이트 할 수 있음(Allowing transparent migration to new features)

------
## Gradle

> Ant와 Maven의 장점을 모아모아 2012년 출시
> Android OS의 빌드 도구로 채택 됨
> ***Gradle이란 무엇인가?***
>   - Ant처럼 유연한 벙용 빌드 도구(A very flexible general purpose build tool like Ant.)
>   - Maven을 사용할 수 있는 변환 가능 컨벤션 프레임 워크 (Switchable, build-by-convention frameworks a la Maven. But we never lock you in!)
>   - 멀티 프로젝트에 사용하기 좋음 (Very powerful support for multi-project builds.)
>   - Apache Ivy에 기반한 강력한 의존성 관리 (Very powerful dependency management (based on Apache Ivy))
>   - Maven과 Ivy 레파지토리 완전 지원 (Full support for your existing Maven or Ivy repository infrastructure.)
>   - 원격 저장소나,pom , ivy 파일 없이 연결되는 의존성 관리 지원   
>   (Support for transitive dependency management without the need for remote repositories or pom.xml and ivy.xml files.)
>   - 그루비 문법 사용 (Groovy build scripts.)
>   - 빌드를 설명하는 풍부한 도메인 모델 (A rich domain model for describing your build.)
------
## Maven VS Gradle
Maven에는 gradle과 비교 문서가 없지만 , gradle에는 비교문서가 존재한다.   
Gradle이 시기적으로 늦게 나온만큼 사용성,성능 등 비교적 뛰어난 스펙을 가지고 있다.   
***Gradle이 Maven 보다 좋은점***   
  - Build라는 동적인 요소를 XML로 정의하기에는 어려운 부분이 많다.
    -설정 내용이 길어지고 가독성이 떨어짐
    - 상속구조를 이용한 멀티 모듈 구현
    - 특정 설정을 소수의 모듈에서 공유하기 위해서는 부모 프로젝트를 생성하여 상속하게 해야 함(상속의 단점 생김)
   - Gradle은 Groovy를 사용하기 때문에, 동적인 빌드는 Groovy 스크립트로 플러그인을 호출하거나 직접 코드를 짜면 된다.
    - Configuration Injection 방식을 사용해서 공통 모듈을 상속하는 단점을 커버했다.
    - 설정 주입 시 프로젝트의 조건을 체크할 수 있어서 프로젝트별로 주입되는 설정을 다르게 할 수 있다.
------
  ### Gradle vs Maven : Perfomance Comparison
    - 600명의 엔지니어가 1년동안 1분걸리는 빌드를 매주 42번 빌드를 진핼 할 때 들어가는 비용은   
    이때 빌드 속도가 90% 빨라진다면?
    -Gradle 메이븐 보다 최대 100배 빠르다
    
![267F8745595B0BB601](https://user-images.githubusercontent.com/85658845/173749200-d7ad8fb7-e5ab-4dcb-8b4b-0dce93b3adcb.png)
    
 ![262E4845595B0BB60A](https://user-images.githubusercontent.com/85658845/173749351-741aab01-82b1-4c40-bf6e-75736f615736.png)

![25548345595B0BB718](https://user-images.githubusercontent.com/85658845/173749787-000f6bc3-597d-42cb-b211-e29d1ff94b54.png)
![26162D45595B0BB710](https://user-images.githubusercontent.com/85658845/173749816-20e97837-8d8d-4376-90e8-d34b8dbd93dd.png)

