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
이 라이브러리를 컴파일하기 위해(Compile)   
이 구성은 이 라이브러리의 컴파일 클래스 경로를 포함하므로 컴파일하기 위해 자바 컴파일러를 호출할 때 사용된다.   


### runtimeClassPath   
라이브러리 실행 (Runtime)   
이 구성에는 이 라이브러리의 런타임 클래스 경로가 포함되어 있습니다.  

![img1 daumcdn](https://user-images.githubusercontent.com/85658845/173961683-0e09cd3f-a280-496e-9cd7-35536a05cafb.png)

### api
컴파일 타임과 런타임에 사용자에게 의존성을노출시킨다.   
의존 라이브러리가 수정되는 경우 본 모듈을 의존하는 모든 모듈들을 재빌드한다.   

### implementation   
내부적으로만 사용되고 사용자에게는 의존성을 노출시키지 않게 선언한다.   
다만, 런타임에는 노출된다.   
의존 라이브러리를 수정해도 본 모듈까지만 재빌드한다.  

결국, api와 implementation은 다음과 같은 차이를 가진다.   
A <= B <= C의 구조를 가지는 모듈이 있다고 가정하자.   

- A가 api면,C에서는 A접근이 가능하며 A가 수정되면 B,C가 재빌드 된다.
- A가 implementation이면, C에서 A를 접근할수 없고 A가 수정 시 B까지만 재빌드 된다.

### compileOnly
컴파일 타임에 필요한 라이브러리   
컴파일시에만 빌드하고 빌드 결과물에는 포함하지 않는다.

### compileOnlyApi
사용자가 만든 모듈에 의해 컴파일 타임에 필요한 라이브러리
compileOnly와 동일하게 컴파일 시에만 빌드하고 빌드 결과물에는 제외된다.

### runtimeOnly    
런타임 시점에만 필요한 라이브러리    
여기서 컴파일 시간이 아닌 런타임에만 필요한 종속성을 선언할 수 있습니다.   

### annotationProcessor
annotation Processor를 명시하기 위해 사용

## 언제 이 라이브러리 의존성 옵션을 써야 하는가?
라이브러리마다 필요한 시점이 다르기 때문에 거기에 맞게 사용해야 한다.   
가장 좋은 건 라이브러리마다 어떤 방식으로 제공하는지 이해한 후, 그에 맞게 사용해야 한다.   

### implemenation
실제로 MVNRepository에서 의존성 추가하려고 예시를 가져오면 대부분 이것을 사용한다.   
이 옵션은 대규모 빌드에서는 다시 컴파일을 진행할 때, 그 대상의 크기가 줄어 빌드 시간을 개선할 수 있다고 한다.   
프로젝트에 어떤 라이브러리를 사용한다고 하면 대부분 이것을 사용하게 된다   

### compileOnly
컴파일 시점에 꼭 필요한 라이브러리   
Lombok 같은 라이브러리가 이에 해당한다.   

### runtimeOnly
컴파일 시점에는 필요 없지만, 런타임에 필요한 라이브러리    
Logging 관련 라이브러리, DB 관련 라이브러리 등이 있겠다.   



### Reference
https://docs.gradle.org/current/userguide/java_library_plugin.html   
https://www.geeksforgeeks.org/how-is-compiletime-classpath-different-from-runtime-classpath-in-java/    
https://tomgregory.com/gradle-implementation-vs-compile-dependencies/       
https://stackoverflow.com/questions/4270950/compile-time-vs-run-time-dependency-java/4271013    
https://stackoverflow.com/questions/44493378/whats-the-difference-between-implementation-and-compile-in-gradle         
### 출처:   
(https://twinparadox.tistory.com/630) [Twinparadox Factory:티스토리]







