# Thymeleaf

## Thymeleaf의 특징
    서버 사이드 템플릿 엔진입니다.   
    클라이언트가 동적으로 그리는 방식이 아니라 서버가 모든 html을 그려서 내려주는 방식입니다.
    서버에서(유저마다 동적으로 달라질수 있는)데이터들을 구해서 미리 정의된 템플릿에 넣고 서버에서 직접 html을 그려서 클라이언트(브라우저)에게 전달합니다.
    th:text와 같은 문법으로 html에 값을 주입하기 때문에 매우 직관적이며 진입장벽이 낮습니다.
    html로 작성하기 때문에 서버를 띄울필요 없이 바로 브라우저에서 확인 할 수 있습니다.

## 우리 프로젝트에서 Thymeleaf을 사용하면 좋은 점
    Spring WebMVC와 통합이 비교적 쉽습니다.
    spring-boot-starter-thymeleaf를 따로 만들어 두었을 정도로 스프링과의 호환성이 매우 좋습니다.
    간단한 코드로 Spring Security 결과물을 바로 확인할 수 있습니다.

## Thymeleaf 문법

    ${name}
    변수 name 값 불러오기
    @RequestMapping(value = "/example", method = RequestMethod.GET)
    public String newPerson(Model model) {
        model.addAttribute("name","김철수");
        return "example"
    
    html 파일에선 name이 있으면 name의 값이 들어가고 없으면 홍길동이 들어갑니다.
    <p?당신의 이름은 <span th:text="${name}">홍길동</span>입니다</p>
-----
    th:with
        변수값 지정
        <div th:with="temp=${name}"></div>
----
    th:text
        text 수정
            <div th:text="temp=${name}">기본값</div>
---
    th:block / th:if / th:unless
        if else와 유살함
            <th:block th:if = ${age < 3}"><p>당신은 30대가 아닙니다</p></th:block>
            <th:block th:unless = ${age < 3}"><p>당신은 30대입니다.</p></th:block>
-----
    th:switch/th:case
        Switch case 와 유사함
            <th:bloack th:switch="${name}">
                <p th:case="이철수">당신은 이씨 입니다.</p>
                <p th:case="김철수>당신은 김씨 입니다.</p>
            </th:block>
-----
    th:each
        반복문
            <div th:each="data:${datas}">
                <h1 th:text="${data}"></h1>
            </div>
-----