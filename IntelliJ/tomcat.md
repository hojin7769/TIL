# 인텔리제이 톰켓연동하는법

## 1. Tomcat(톰켓) 설치
1) 톰캣은 아파치 소프트웨어 재단에서 오픈 소스로 무료로 배포하는 서블릿 컨테이너이다.    

2) 다음 링크로 이동하여 설치 파일을 받아 보자.   
 - https://tomcat.apache.org/   
 - 원하는 버전을 선택 하도록 한다.   
   (나와 같은 경우는 Tomcat 9를 선택 하였다. Tomcat9는 Java 8부터 지원하니 참고 하자.)  
   
![image](https://user-images.githubusercontent.com/85658845/173966332-3bd559a8-d0eb-414b-8708-8cc84f9c26c2.png)

3) 본인의 OS 환경등에 따라 원하는 설치 파일을 선택 하도록 한다.   
 - 나와 같은 경우는 64비트 윈도우를 사용한기 때문에 64-bit Windows zip을 클릭하여 다운로드 받았다.   
 - 가장 위 'zip'은 윈도우, 유닉스, 리눅스에서 모두 사용할 수 있는 배포판 이다.   

![img1 daumcdn](https://user-images.githubusercontent.com/85658845/173968969-8c2b06bc-9fea-4d75-b969-682a5f33c020.png)


4) 원하는 경로에 압축을 푼다.   
 - 이로써 IntelliJ 톰캣 연동을 위한 사전 준비는 끝났다.   

## 2. Intellij + Tomcat 설정

1) Run >> Edit Configurations... 클릭

![img1 daumcdn](https://user-images.githubusercontent.com/85658845/173969903-b3603fdf-9c52-46f4-b89c-032ce7bb29f8.png)

2) + 클릭 >> Tomcat Server >> Local 클릭

![img1 daumcdn](https://user-images.githubusercontent.com/85658845/173969924-45582b41-a949-4a74-bb76-26d3344edb7b.png)

3) Tomcat Server >> Configure... 클릭

![img1 daumcdn](https://user-images.githubusercontent.com/85658845/173969955-bb353359-c0cf-4ef6-8bc6-35dcf26665af.png)

4) 본인의 톰캣이 설치된 디렉토리를 선택한다.

![img1 daumcdn](https://user-images.githubusercontent.com/85658845/173969978-1c9195e0-9c73-4e69-983e-04b04806e2e0.png)

5) 부가적인 설정이 가능하다.   
   \- 디포트 브라우저를 선택 할 수 있다.   
   \- 서버 포트를 선택 가능하다   
   \- Warning: No artifacts configured : Deployment 탭에서 나머지 설정을 해주거나, Fix 버튼을 클릭하여 마무리 설정을 해주면 된다.    
   
![img1 daumcdn](https://user-images.githubusercontent.com/85658845/173970137-a40826e2-09a5-4c6e-801a-bc5c4e60a709.png)

6) 배포 설정

![img1 daumcdn](https://user-images.githubusercontent.com/85658845/173970151-f20d4f92-590b-4e17-9312-eb4666eadc3c.png)


## ※ 배포 패키지 유형 참고   
### 1) 아카이브(.war, .ear 등) 파일로 배포 한다.      
   \ - 아카이브는 WAS(Tomcat 등)에 의해 자동으로 압축이 해제된다.     
   \- 파일이 많은 경우 압축을 푸는 시간이 오래 걸릴 수 있다.   
   \- 원격 서버에 배포시 한 개의 파일만 전송하면 된다.   

### 2) exploded(expanded)
 \- 아카이브를 압축 해제하여 디렉토리 형태로 배포 한다.   
 \- 원본 소스를 건드리지 않고 그대로 배포하는 경우에 적합하다.    
 \- 별도 디렉토리에 원본 소스를 복사하여 만들기 때문에 파일이 많은 경우 복사하는 시간이 오래 걸릴 수 있다.   
 \ - Application context가 자동으로 설정될 것이다. 나는 기본 루트("/")로 변경 하였다.

![img1 daumcdn](https://user-images.githubusercontent.com/85658845/173970399-9b0e5b43-6ea7-4437-b7ab-6f7473d03978.png)

6) 웹 프로젝트 실행   
 \- 이로써 기본 설정은 다 끝났고, 서버를 실행하면 본인이 개발중인 웹 프로젝트가 정상적으로 실행될 것이다.   
 ![img1 daumcdn](https://user-images.githubusercontent.com/85658845/173970437-0d68d56c-93ed-4a09-a808-8c2eacf6e7a3.png)

## 출처
https://goddaehee.tistory.com/247

