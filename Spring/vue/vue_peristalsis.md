# [SpringBoot] Vue.JS + SpringBoot 연동하기

스프링부트와 Vue.js 프로젝트를 구성하는 방법을 정리 한다.

-------
Tools
- sts4
- spring boot 2.7.0
- gradle 
- vue-cli
- Vscode
- npm
- java 11

-------

## 1. 프로젝트의 구조 및 간단한 동작 원리

  - 프로젝트 구조
    - Vue 프로젝트에서 개발하 것을 빌드(Build)하여 결과물을 Spring Boot 프로젝트 내의 static 폴더에 저장합니다.
    - 첫번째 이미지는 springBoot 프로젝트 내에서 Vue 프로젝트를 따로 생성한 이미지
    - 두번째 이미지는 위 Vue 프로젝트를 build 할 때 Spring Boot 프로젝트 구조 이미지

![img1 daumcdn](https://user-images.githubusercontent.com/85658845/174507784-5e9c8e55-8341-4859-8f67-579a82e6e8d9.png)

![img1 daumcdn](https://user-images.githubusercontent.com/85658845/174507793-3ab92b35-dc7c-4f41-b871-658d3edfb55c.png)

  - 프로젝트 동작원리
    - Vue 프로젝트 개발 후 Build -> SpringBoot(static 폴더에 생성)
    - Spring Boot 실행
    - 웹 페이지 접속(지정경로) -> Spring Boot 프로젝트 내의 static 폴더에 생긴 Vue 결과물을 실행

------
## 2. Spring Boot 프로젝트 생성하기
  - Spring Boot 프로젝트 생성하기 (링크 넣어야 함)
  - 프로젝트가 생성되면 resources -> static 아래에 아무 이름으로 디렉토리 생성
  - 해당 디렉토리는 vue build 결과물을 저장 할 것이다.

## 3. Vue.js 프로젝트 생성
- SpringBoot 프로젝트 내에 vue프로젝트를 개발할 디렉토리를 생성합니다. (그냥 최상위에 아무 이름으로 폴더 생성하기)
- Vscode를 실행하여 Spring Boot 프로젝트를 열어 위에서 생성한 그 디렉토리로 이동
-   (~/~/경로/SpringBoot프로젝트/생성한 vue 디렉토리)

    ![image](https://user-images.githubusercontent.com/85658845/174508227-6d8a30ae-5013-431c-9e83-0b6473fe10b4.png)
현제 시점 나의 경로이다

![image](https://user-images.githubusercontent.com/85658845/174508353-282553ea-44b4-4e67-9dd4-c20268144f7f.png)


- 아래 명령어를 통해 디렉토리에 vue 프로젝트를 생성합니다.

![image](https://user-images.githubusercontent.com/85658845/174508504-7f30860c-1643-434b-9c65-1c0e64799dcf.png)


![image](https://user-images.githubusercontent.com/85658845/174508712-fd1710db-b106-49f7-babe-4f1e4255f4b1.png)

처음 설치 했을 때 이런 오류를 뛰었지만 이건 vue-cli의 init이라는 기능을 설치하지 않아 그런것이다.

vue init이란 간단히 말하면 2.x Template을 가져오기 위한 vue init기능이다.

![image](https://user-images.githubusercontent.com/85658845/174508800-2149e4e7-e602-44b1-8fd0-7176262a5902.png)

***npm i -g @vue/cli-init*** 명령어로 글로벌에 설치해 준다

그후 다시 vue init webpack 프로젝트명 실행 해 준다.

그럼 나오는 화면에

![image](https://user-images.githubusercontent.com/85658845/174510070-b80a242a-13b0-4b6a-ba2f-1173792875ae.png)

현 시점 나는 이렇게 설정 해 줬다.

- Project name : 프로젝트 이름
- Project description : 프로젝트 설명
- Author : 사용자
- Vue build : Runtime + Compiler 선택합니다.(아마도 아래는 실행만 해주는 옵션 같습니다.)
- Install vue-router : 라우터 설치
- Use ESLint to lint youe code : ESLint 플러그인을 통해 코드 검증을 합니다.
- Set up unit tests : 유닛테스트 설정(해당 글에서는 N으로 사용을 안하였습니다.
- Setup e2e test with Nightwatch : 잘 모르겠습니다... 아마 테스트 관련 인 것 같습니다.
- Shoud we run npm install ~ : NPM을 사용할지 Yarn을 사용할지 선택합니다.

- 모든 설정을 마치시면 프로젝트가 생성이됩니다.

실행 하면 엄청난 설치 후 아래와 같은 화면이 출력된다



<img src="https://user-images.githubusercontent.com/85658845/174510758-15d6b23e-859c-4989-aa6a-ec8f7cc1d2b2.png" width=500px >

<img src="https://user-images.githubusercontent.com/85658845/174510823-8d1185a9-d05b-46a5-827f-dd4719fc7a18.png" width=300px >

## 3. Vue.js 프로젝트 설정하기
- vue 프로젝트를 build 시 결과물을 SpringBoot 프로젝트의 static 폴더로 지정하기 위해 설정
- vue프로젝트 -> config -> index.js 파일을 아래와 같이 수정

![image](https://user-images.githubusercontent.com/85658845/174510973-21e1a72b-97b7-461b-b37a-eb95b1343848.png)

- index: path.resolve(__dirname, 'SpringBoot 프로젝트에 html을 위치할 경로')

<strong style="color:red;">참고!!!)</strong>   
resources/static 아래가 아닌 resources/templates 에 한 이유는    
해당 프로젝트는 현재 thymeleaf를 사용하고 있으며, 기본적으로 html을 읽어오는 경로가 templates 아래 경로이기 때문입니다.     
만약, thymeleaf를 사용을 안하신다면, resources/static 아래로 작성하셔도 무방합니다.     
또한, 따로 프로젝트를 설정하여, vue에 관한 경로를 설정하여 사용하실 경우 원하시는 경로로 작성하시면 됩니다.   

- assetsRoot : path.resolve(__dirname. 'SpringBoot 프로젝트에 build 결과물 저장할 경로')
  - vue 프로젝트를 빌드 시 생성될 css, js 등 파일을 위치할 경로를 설정합니다.   
  - 위 index.html은 해당 경로의 css, js 등 파일을 읽어와 화면에 보여지게 됩니다.   
- assetsPublicPath: 'vue/'

- index.html에서 읽어올 때 의 경로 (default로는 '/' 이지만, 2번에서 static아래에 vue라는 디렉토리를 생성하였기 때문에, 해당 디렉토리를 읽어오기 위해 수정하도록 하겠습니다.)


## 4. 프로젝트 실행하기
- VS Code 내 vue 프로젝트에서 아래 명령어를 통해 빌드(Build)를 진행합니다.
npm run build

![image](https://user-images.githubusercontent.com/85658845/174511384-b9c0e4a9-8af4-4c78-b6e0-baaf57a9e7b5.png)

![image](https://user-images.githubusercontent.com/85658845/174511403-2579fc1a-5fd5-4378-b4d1-27ededb1c20f.png)

- Build가 성공적으로 끝이 났다면, SpringBoot 프로젝트에 정상적으로 Build 결과물이 생성되었는지 확인합니다.\

![image](https://user-images.githubusercontent.com/85658845/174511441-2b19678c-9b48-4125-9b81-d69d98224aa0.png)

- Build 결과물을 확인하기 위해, index.html을 읽어오도록 하겠습니다.

- Controller 를 생성하여 vue/index.html을 읽어옵니다.

![image](https://user-images.githubusercontent.com/85658845/174511466-25066aeb-b9cf-4a05-a559-61b693cc107d.png)

- localhost:포트/vue 로 접속합니다.(ex: localhost:8081/vue)
![image](https://user-images.githubusercontent.com/85658845/174511528-0946bb4f-6000-4600-bff8-3422e475a485.png)
- 정상적으로 Vue 화면을 확인할 수 있습니다.

