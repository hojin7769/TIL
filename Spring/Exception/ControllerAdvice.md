# @ControllerAdvice, @ExceptionHandler를 이용한 예외처리 분리

## @ExceptionHandler

@ExceptionHandler는 @Controller,@RestController 가 적용된 Bean에서   
발생하는 예외를 잡아서 하나의 메서드에서 처리해주는 기능이다.   
@ExceptionHandler에 설정한 예외가 발생하면 handler가 실행된다.   
@Controller , @RestController 가 아닌 @Service나 @Repository가 적용된 Bean에서는 사용할수 없다.   
@ExceptionHandler 인터페이스로 들어가   
보면 아래와 같다.

![image](https://user-images.githubusercontent.com/85658845/175472457-b780bd99-cbc1-4021-86e9-4b08ba7f31d7.png)

value 설정을 통하여 어떤 예외를 잡을지 설정할 수 있다. 주의할 점은 value를   
지정하지 않으면 모든 예외를 잡기 때문에 필요한 예외를 설정 해주어야 한다.  
필요하다면 List 형태로 여러 예외들을 정할 수 있다.   
***@ExceptionHandler({Excpetion.class, Exception2.class})***   
이런 방법으로 2개 이상도 등록 가능하다.

실제 @Controller Bean에서 사용한 예를 보자.

![image](https://user-images.githubusercontent.com/85658845/175472781-2fd0084a-9889-4e60-9c4e-81ddb07d884c.png)

우선 ***@ExceptionHandler({SQLException.class, DataAccessException.class})*** 를 통하여 어떤 예외를   
처리 할 것 인지를 설정하였다. 컨트롤러 작업중 DB에 관련된 에러가 발생할 경우 @ExceptionHandler가 동작하게 된다.

## @ControllerAdvice
***@ControllerAdvice***는 ***@Controller*** 어노테이션이 있는 모든 곳에서의 예외를 잡을 수 있도록 해준다.   
***@ControllerAdvice*** 안에 있는 ***@ExceptionHandler***는 모든 컨트롤러에서 발생하는 예외상황을 잡을 수 있다.   
***@ControllerAdvice*** 의 속성 설정을 통하여 원하는 컨트롤러나 패키지만 선택할 수 있다.   
따로 지정을 하지 않으면 모든 패키지에 있는 컨트롤러를 담당하게 된다.

![image](https://user-images.githubusercontent.com/85658845/175473261-c0c566e8-2547-470a-b484-024f010a77b7.png)

***@ControllerAdvice***는 새로운 클래스 파일을 만들어 사용하면 된다.   
아래를 보면 ***PageControllerAdvice*** 라는 클래스에 ***@ControllerAdvice*** 어노테이션을 붙였다.   
그 후 ***@ExceptionHandler***로 처리하고 싶은 예외를 처리 할 수 있도록 하였다  

![image](https://user-images.githubusercontent.com/85658845/175473481-9200d580-cb1b-488a-8a2e-3802f7ac01e6.png)

## @RestControllerAdvice
> ControllerAdvice + @ResponseBody → @RestControllerAdvice

***@RestControllerAdvice*** 도 ***@ControllerAdvice***와 동일한 역할을 한다.   
단지 객체를 반환할 수 있다라는 의미를 가지고 있다.   
***@ControllerAdvice*** 와 달리 응답의 body에 객체를 넣어 반환이 가능하다.   
***@RestController***에서의 예외만 잡는다는 뜻이 아니다.   
***@RestController***에서 발생하든 ***@Controller*** 에서 발생하든 ***@RestControllerAdvice***는 다 잡을 수 있다.
