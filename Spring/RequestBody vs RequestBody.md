컨트롤러에서 데이터를 인자에 할당하는 대표적인 방법으로는 @RequestBody 와 @RequestParam 이 있다.   

<image src="https://user-images.githubusercontent.com/85658845/174200028-652d2a9d-0bd5-4353-b2fd-fcc1d924ef6a.png" width="400" height="400"/>


## FORM 태그로 데이터 전달

![image](https://user-images.githubusercontent.com/85658845/174200902-36f29f56-db2b-456d-b26a-240d26cc30d4.png)

![image](https://user-images.githubusercontent.com/85658845/174201310-7ac70933-4baf-405d-bc2d-63b6ae5e7a08.png)


위와 같이 데이터를 전송하여 컨트롤러에서 @RequestBody를 이용하여 데이터를 받아보았다

```
@PostMapping("/formTest")
	public String formTesr(@RequestBody String res) {
		
		System.out.println("통신성공");
		System.out.println(">>>>>" + res);
		
		return "result";
		
	}
  //출력 결과
  //통신성공
  // >>>>>name=123&age=22
```
우리가 입력한 '123' 이라는 이름과 '22' 라는 나이가 잘 전달이 되었지만 단지 'name=123&age=2' 이라는 String 으로 전달되어 전달된 데이터를 사용하기에는 불편함이 있다.

이제 @RequestParam으로 데이터를 받아보자   

```
@PostMapping("/formTest")
	public String formTesr(@RequestParam String name) {
		
		System.out.println("통신성공");
		System.out.println(">>>>>" + name);
		
		return "result";
		
	}
  //출력 결과
  //통신성공
  // >>>>> 123
```
@RequestBody 로 데이터를 받을 때는 메서드의 변수명이 상관이 없었지만, @RequestParam 으로 데이터를 받을때는 데이터를 저장하는 이름으로 메서드의 변수명을 설정해주어야 한다.    

결과적으로 123 이라는 이름이 잘 전달이 되었고, 이번엔 name 이라는 변수에 할당이 되어 사용하기에도 용이하다.    


## JSON 데이터로 전송하기

이번에는 ajax를 이용하여 데이터를 전달해보도록 하겠다.

ajax 는 Asynchronous JavaScript and XML 의 약자로서 비동기적으로 서버와 브라우저가 데이터를 주고 받는 방식이다.

대표적인 예로 javaScript 의 fetch API 가 있다.

많은 사람들이 사용하는 방법인데, 이번엔 fetch API 로 데이터를 전송하고 데이터를 받아보자.

```
  @PostMapping("/formTest")
	public String formTesr(@RequestParam String name) {
		
		System.out.println("통신성공");
		System.out.println(">>>>>" + name);
		
		return "result";
		
	}
}
```
위와 같이 컨트롤러를 구현한 후 데이터를 전송해보았지만 에러가 발생하였다.

<span style="color:red;">MissingServletRequestParameterException: Required String parameter 'name' is not present</span>

name 이라는 파라미터가 없다고 한다.

그 이유는 기본적으로 @RequestParam 은 url 상에서 데이터를 찾기 때문이다.

우리가 위에서 <form> 태그를 이용하여 데이터를 입력하고 제출 버튼을 누르면 입력한 데이터들이 url을 통해서 전달된다.
  
  
 

예를 들면 'http://<vo>localhost:8090/receive?name=jun&age=13' 이런 식이다.

반면에 Json형식으로 데이터를 전달할때는, url은 http://<no>localhost:8080/receive로 변함이 없고 body에 데이터를 포함하여 전송하기 때문에 @RequestParam 으로는 받을 수 없는 것이다.

그렇다면 한번 fetch API 로 데이터를 전달하되 전송하는 주소를 /receive?name=jun&age=13 으로 변경하고 전달해보면 어떻게 될까?
   
  ```
  통신성공
  >>>>>{"name":"jun","age":"13"}
  ```
  
  이제 다시 본론으로 돌아와 '/receive' 주소로 데이터를 전송하고 @RequestBody 로 데이터를 받아보자.
  
  ```
@Controller
public class UserController {

	@PostMapping("/receive")
	public String age(@RequestBody String req) {
		System.out.println("통신 성공");
		System.out.println(">>> " + req);
		return "result";
	}
}

//출력 결과
//통신 성공
//>>> {"name":"jun","age":"13"}
  ```
 
  <form> 태그로 데이터를 전달하고 @RequestBody 로 받았을 때와 차이가 없어 보인다.

하지만 여기에는 큰 차이가 있다.
    
## 자동객체 생성
    
만약 다음과 같이 name 과 age 를 필요로 하는 Person 클래스가 있고 getter 가 구현되어 있다면
    
```
public class Person {
//변수
private String name;
private int age;

public Person() {

}

public Person(final String name) {
  this.name = name;
}

public String getName() {
  return name;
}

public int getAge() {
  return age;
}

@Override
public String toString() {
  return "Person{" +
          "name='" + name + '\'' +
          ", age=" + age +
          '}';
  }
}
```
    
다음과 같은 기능이 가능하다.

```
 @Controller
public class UserController {

	@PostMapping("/receive")
	public String age(@RequestBody Person person) {
		System.out.println("통신 성공");
		System.out.println(">>> " + person);
		return "result";
	}
}

//출력 결과
//통신 성공
//>>> Person{name='jun', age=13}
```
신기하게도 Person 객체를 자동으로 생성해 주었다.

@RequestBody 가 아닌 @RequestParam 을 이용한다면 불가능하다. 한번 시도해보자.

비동기통신에서 @RequestParam 으로 데이터를 전달받기 위해 /receive?name=jun&age=13 의 주소로 데이터를 전송하고 @RequestParam 으로 데이터를 받아 같은 행동을 취했지만 에러가 발생하는 모습이다.

    
```
@Controller
public class UserController {

	@PostMapping("/receive")
	public String age(@RequestParam Person person) {
		System.out.println("통신 성공");
		System.out.println(">>> " + person);
		return "result";
	}
}

//출력 결과
.MissingServletRequestParameterException: Required Person parameter 'person' is not present]
```
    
@RequestBody, @RequestParam 모두 Map<String,String> 으로 결과를 받아올 수도 있다.
    
```
@Controller
public class UserController {

	@PostMapping("/receive")
	public String age(@RequestBody Map<String,String> map) {
		System.out.println("통신 성공");
		System.out.println(">>> " + map.get("name"));
		System.out.println(">>> " + map.get("age"));
		return "result";
	}
}

//출력 결과
//통신 성공
//>>> jun
//>>> 13
```
    
![image](https://user-images.githubusercontent.com/85658845/174204383-b60ae4e1-1692-4385-a69a-ea954fbaa2c9.png)
    
 ### 참조 
    https://ocblog.tistory.com/49
