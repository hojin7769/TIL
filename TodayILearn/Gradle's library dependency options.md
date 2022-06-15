Maven 프로젝트에서 Gradle로 프로젝트를 생성 했을때 다른 부분들이 눈에 들어 오기 시작했다

![image](https://user-images.githubusercontent.com/85658845/173757219-44bdf2a1-178f-424d-b63e-193b8f4480e6.png)

메이븐 dependencies와는 다르게 앞에 무엇인가가 많이 붙기 시작한것이다.    

이를 알아 볼 것이다.    

------
## 공식 홈페이지에 나온  Java Library plugin configurations

![img1 daumcdn](https://user-images.githubusercontent.com/85658845/173757776-e362f06b-d463-4662-8bf8-a1c9ee9dae1c.png)   

-  녹색으로 표시된 구성은 사용자가 종속성을 선언하는 데 사용해야 하는 구성입니다.
- 분홍색 으로 표시된 구성은 구성 요소가 컴파일되거나 라이브러리에 대해 실행될 때 사용되는 구성 입니다.
- 파란색 으로 표시된 구성 은 자체 사용을 위해 구성 요소 내부에 있습니다.

그래프를 보면 우리가 궁금해하는 내용은 초록색에 해당하는 내용이지만,    z
파란색과 분홍색의 내용이 무엇인지 알아야 초록색에 대해서 이해할 수 있다.    
![img1 daumcdn](https://user-images.githubusercontent.com/85658845/173759615-0aede79c-a754-44e2-bea7-87a4bc19c418.png)
### apiElements 
라이브러리 컴파일(Compile)   
이 구성은 소비자가 이 라이브러리에 대해 컴파일하는 데 필요한 모든 요소를 검색하는 데 사용됩니다.  
default 설정과 다르게, implemenation이나 runtime 의존성에 대한 정보를 노출하지 않는다.

### runtimeElements   
라이브러리 실행 (Runtime)   
해당 라이브러리를 실행하는 데 필요한 모든 요소를 검색할 때 사용한다.

![img1 daumcdn](https://user-images.githubusercontent.com/85658845/173789767-81b7b040-1839-4b92-b89a-43be92d2a756.png)

### compileClasspath
