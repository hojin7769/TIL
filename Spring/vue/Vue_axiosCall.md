# 뷰 내에서 REST Api 호출하기 

## axios 로 호출하기
### axios란?
React는 효율적인 UI 구현을 위한 라이브러리입니다.   
HTTP Client(HTTP 상에서 커뮤니케이션 하는 자바기반 컴포넌트)를 내장하고 있는 Angular와 다르게, Vue에는 따로 내장하는 내장클래스가 존재하지 않습니다.   

따라서 리약트에서 AJAX(비동기 웹 애플리케이션)를 구현하기 위햐서 Javascript 내장 객체인 XMLRequest를 사용하거나 HTTP Client를 사용해야만 한다.   

그렇다면 어떤 HTTP Client 라이브러리를 사용하는게 좋을까요? vue.js와 함께 쓰면 좋은 HTTP Client라이브러리는 많지만,   
여기서는 현재 뷰에서 가장 많이 사용하고 있는 Fetch API를 비교하면서 Axios라이브러리가 무엇인지 알아보자


--------
### 선행 되어야 하는 프로젝트
1. vue/cli 프로젝트 만들기
2. spring rest api 만들기

---------

### axios 설치
npm install axios 로 axios를 설치한다.

![image](https://user-images.githubusercontent.com/85658845/174799917-4a625191-d6a5-41ea-8dd9-f65d0ccc632c.png)

axios 가 디펜던시로 추가되어 있는 장면이다 버전과 다른 점이 있는지 확인하자
![image](https://user-images.githubusercontent.com/85658845/174800032-555a006b-56af-40e2-8e48-67545015ddb7.png)

이상으로 axios 준비는 모두 끝이 났다. 이제 통신이 되는지 확인해 보자

------
### axios 써보기

일단 데이터를 받아 올 컨트롤러를 만들어 보자

나는 숫자 리스트를 받아올수 있는 RestController를 만들었다

![image](https://user-images.githubusercontent.com/85658845/174801813-c497d0a5-6715-41c4-9340-6a0eca7c3e9f.png)

두번째 axios를 사용할 뷰 파일을 만들어 보자

![image](https://user-images.githubusercontent.com/85658845/174802667-d21d193f-26d3-425a-a53e-72bd85998829.png)


<img width="209" alt="image" src="https://user-images.githubusercontent.com/85658845/174805568-6d5ac96d-b1a0-43bb-af88-15d1d5399fa3.png">


출력이 되는걸 확인할수 있다.
출력이 되느

