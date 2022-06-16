## REST 란?
  REST(Representation State Transfer)의 약자로 자원을 이름으로 구분하여 해당 자원의 상태를 주고 받는 모든 것을 의미합니다.   
  
  ### 즉 REST란 
    1. HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고,   
    2. HTTP Method(POST, GET, PUT, DELETE)를 통해
    3. 해당 자원(URI)에 대한 CRUD Operation을 적용하는 것을 의미합니다.
   [여기서 HTTP란?](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview)  
    
    
 ## REST 구성 요소
  REST는 다음과 같은 3가지로 구성이 되어있다.
  
  1.***자원(Resource) : HTTP URL***
  2.***자원에 대한 행위(Verb):HTTP Method***
  3.***자원에 대한 행위의 내용(Repersentations) : HTTP Message Pay Load***
  
  ### 3. REST의 특징
  1)Uniform ( 유니폼 인터페이스)   
  Uniform Interface는 URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일을 말합니다.   
  
  2)Stateless(무상태성)   
  RESR는 무상태성 성격을 갖ㅅ습니다. 다시 말해 작업을 위한 상태정보를 따로 저장하고 관리하지 않습니다.   
  세션 정보나 쿠키정보를 별도로 저장하고 관리하지 않기 때문에 API서버는 들어오는 요청만을 단순히 처리하면 됩니다.     
  때문에 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로써 구현이 단순해 집니다.   
  
  3) Cashable(캐시 가능)
    REST의 가장 큰 특징 중 하나는 HTTP라는 기존 웹표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로 활용이 가능합니다    
    따라서 HTTP가 가진 캐싱 기능이 적용 가능합니다.   
    HTTP 프로토콜 표준에서 사용하는 Last-Modified태그나 E-Tag를 이용하면 캐싱 구현이 가능합니다.   
    
  4) Client-Server 구조
    REST서버는 API 제공, 클라이언트는 사용자 인증이나 컨텍스트(세션, 로그인 정보)등을 직접 관리하는 구조로 각각의 역할이 확실히 구분되기 때문에   
    클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로간 의존성이 줄어들게 됩니다.   
    
  5) Self-descriptiveness(자체표현구조)   
    REST의 또 다른 큰 특징 중 하나는 REST API 메세지만 보고도 이를 쉽게 이해 할 수 있는 자체 표현 구조로 되어 있다는 것 입니다.   
    
  6) 계층형 구조
    REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고 PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있게 합니다.   
  
  ### 4. RESR API 디자인 가이드
  REST API 설계 시 가장 중요한 항목은 다음의 2가지로 요약할 수 있다.
    ***첫번째***, URI는 정보의 자원을 표현해야 한다.
    ***두번째***,자원에 대한 행위는 HTTP Method(GET,POST,PUT,DELETE)로 표현한다.
  #### 4-1 RESR API 중심 규칙
    1)URI는 정보의 자원을 표현해야 한다.(리소스명은 동사보다는 명사를 사용)
     
     ```
      GET /members/delete/1
     ```
  위와 같은 방식은 REST를 제대로 적용하지 않은 URI입니다.   
  URI는 자원을 표현하는데 중점을 두어야 합니다. delete와 같은 행위에 대한 표현이 들어가서는 안됩니다.     
  2) 자원에 대한 행위는 HTTP Method로 표현   
  위의 잘못 된 URI를 HTTP Method를 통해 수정해 본다
  
  ```
    DELETE /members/1
  ```
  으로 수정할 수 있겠습니다.   
  회원정보를 가져올 때는 GET, 회원 추가 시의 행위를 표현하고자 할 때는 POST METHOD를 사용하여 표현합니다.
    
  #### 회원정보를 가져오는 URI  
  
  ```
  GET /members/show/1     (x)
  GET /members/1          (o)
  ```
  
  #### 회원을 추가할 때
  
  ```
    GET /members/insert/2 (x)  - GET 메서드는 리소스 생성에 맞지 않습니다.
    POST /members/2       (o)
  ```
  
 --------
 ### 4-2. URI 설계 시 주의할 점

1) 슬래시 구분자(/)는 계층 관계를 나타내는 데 사용
```
 http://restapi.example.com/houses/apartments
 http://restapi.example.com/animals/mammals/whales
```

2) URI 마지막 문자로 슬래시(/)를 포함하지 않는다.   
URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며 URI가 다르다는 것은 리소스가 다르다는 것이고,역으로 리소스가 다르면 URI도 달라져야 합니다.   
REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않습니다.   

```
    http://restapi.example.com/houses/apartments/ (X)
    http://restapi.example.com/houses/apartments  (0)
```
3) 하이픈(-)은 URI 가독성을 높이는데 사용   
URI를 쉽게 읽고 해석하기 위해, 불가피하게 긴 URI경로를 사용하게 된다면 하이픈을 사용해 가독성을 높일 수 있습니다.   

4) 밑줄(_)은 URI에 사용하지 않는다.   
글꼴에 따라 다르긴 하지만 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 합니다.   
이런 문제를 피하기 위해 밑줄 대신 하이픈(-)을 사용하는 것이 좋습니다.(가독성)   

5) URI 경로에는 소문자가 적합하다.   
URI 경로에 대문자 사용은 피하도록 해야 합니다.   
대소문자에 따라 다른 리소스로 인식하게 되기 때문입니다.   
RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문이지요.   

```
 RFC 3986 is the URI (Unified Resource Identifier) Syntax document
```


6) 파일 확장자는 URI에 포함시키지 않는다.
```
   http://restapi.example.com/members/soccer/345/photo.jpg (X)
```
REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않습니다. Accept header를 사용하도록 합시다.

```
    GET / members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg

```

참고:   
[REST API 제대로 알고 사용하기](https://meetup.toast.com/posts/92)   
[[네트워크] REST API란? REST, RESTful이란?](https://khj93.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-REST-API%EB%9E%80-REST-RESTful%EC%9D%B4%EB%9E%80)   
[[서버] REST API란?](https://hanamon.kr/rest-api/)

