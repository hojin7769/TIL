# Vue.js 에 Vuetify 설치 하기

오늘은 Vue.js에 Vuetify UI Tool을 설치해 볼 시간이다.

## 1. 현 버전
------------------
1. Vue - 2.6.4
2. Vue/Cli - 5.0.6

-------
이렇게 vue 버전을 가지고 있다

첫번째로 해야 할 내용은
vue/cli로 프로젝트를 생성하는 것이다

vs 코드를 켜고 터미널을 연다.

![image](https://user-images.githubusercontent.com/85658845/175459840-8e24eed5-500b-4b9d-be2d-70790ca19e38.png)

현재 나의 작업 공간이다

여기에 

```
  vue create [프로젝트 이름]
```
이렇게 프로젝트를 생성한다.

만들면 

![image](https://user-images.githubusercontent.com/85658845/175460008-534cd8ce-c89d-4e7a-a2c6-e13a20edbaa8.png)

이런 화면이 나타나는데 작성자는 디폴트로 생성하겠다.

설치가 다 되면 

해당 설치 파일로 경로를 변경해 준다.

![image](https://user-images.githubusercontent.com/85658845/175460214-7a21263d-0703-45c4-b768-dd2a3a77b5d4.png)

그리고 서버를 실핼 시켜준다.

실행 커멘드는 해당 vue 프로젝트 경로에서
```
npm run serve
```
위 코드를 치면 실행이 가능하다

<실행 성공시 화면><br>
![image](https://user-images.githubusercontent.com/85658845/175460350-8276ae10-2922-4649-ad99-031856672593.png)

켜지는걸 확인 했다면 뷰 서버를 종료 시켜준다 종료는 Cltr + c 를 두번 눌러준다

다음으로 할 작업은 vuetify를 추가해 줄 것이다.

현재 뷰 프로젝트 경로에    
vue add vuetify 코드 실행   

![image](https://user-images.githubusercontent.com/85658845/175460611-7ac1a853-f091-4b79-a09f-cc7c1dee613c.png)


![image](https://user-images.githubusercontent.com/85658845/175460631-072c521b-76e8-4257-91e0-46b39ee47d22.png)

해당 화면에서 현 버전이 아닌 낮은 버전이면 Default를 눌렀겠지만 현 뷰티파이는 vue3를 지원하지 않는다. 하여 작성자는   
Vuetify 3를 깔아야 한다 이 버전은 아직 베타 버전이라 사용법이 좀 다르다.   
[Vuetify 3](https://next.vuetifyjs.com/en/getting-started/installation/)   
해당 사이트를 올려두겠다.

다음 
```
Would you like to install Vuetify 3 nightly build? (WARNING: Nightly builds are intended for development testing and may include bugs or other issues.) (y/N) 
```
이렇게 묻는 질문이 나온다 이질문은 버그가 있어도 깔거냐는 질문이다 무조건 y다 안그러면 안깔린다.

다 깔리면

![image](https://user-images.githubusercontent.com/85658845/175460972-bbc4187e-06d5-405b-bdff-214b54cd0d02.png)

이런 화면이 출력된다.

깔리고 나서 확인해볼 파일들

<package.json>   
![image](https://user-images.githubusercontent.com/85658845/175461166-986e88f1-69c7-452d-b82a-a503a7c205ca.png)

<vue.config.js>

![image](https://user-images.githubusercontent.com/85658845/175461220-ed6826ec-e3e1-4d02-a346-38735c8a2bab.png)

<main.js>

![image](https://user-images.githubusercontent.com/85658845/175461253-cf8e5005-794f-470e-860b-5272c2aca2be.png)

<App.vue>

![image](https://user-images.githubusercontent.com/85658845/175461280-7f73a1a5-4456-45cb-a9ee-afe7b1aa7200.png)

등 확인 할수 있다.

마지막으로 서버를 실행하여 확인해 보자

![image](https://user-images.githubusercontent.com/85658845/175461473-6454f39d-22c7-482a-9ec8-aedcba700c3f.png)

잘 실행된다.

이상으로 오늘 배울 내용을 

