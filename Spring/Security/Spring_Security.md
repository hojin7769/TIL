# Spring Security란?
Spring을 사용한다면 사실상 최선의 Security Framework

Web 기반 Application에 보안적인 제한을 추가하기 위해 사용하는 Security Framework 중에 하나입니다.
Spring Security의 주된 목표는 rest api endpoint, mvc url, 정적 리소스와 같은 리소스들에 접근하려는 요청의 인증을 책임지는 것 입니다.
Spring Security는 Spring 생태계와 호환성이 높고 커스텀이 매우 쉽습니다.

# 인증과 인가

spring security를 한문장으로 소개해야 한다면
스프링 생태계에서 인증과 인가라는 개념을 최대한 쉽고 유연하게 구현할 수 있도록 만들어진 framework이다.

그만큼 인증과 인가는 Spring Security의 개념들 중에 하나에 그치는게 아니라 Spring Security가 궁극적으로 이루고자 하는 목표이다.

# 인증(Authentication)
인증은 사용자가 누구인가 확인하는 절차입니다.
단적인 예로 로그인을 말함
![스크린샷 2022-06-27 오후 10 06 38](https://user-images.githubusercontent.com/85658845/175948808-233b4457-7142-4e31-b805-bbd2466b1aec.png)

# 다양한 인증 방법
 어떨게 나를 인증할 수 있을까?
 단순히 로그인 하면 되지! 라는 생각으로는 해결되지 않습니다.   
 로그인을 한번하고 난 뒤, 서비스를 이용하는 중에도 계속해서 인증이 이루어져야 하기 때문이다.   
 로그인은 유저A로 하고 실제 서비스는 유저B가 이용할 지 아무도 모르는 것이기 때문이다.
 
![스크린샷 2022-06-27 오후 10 06 38](https://user-images.githubusercontent.com/85658845/175949161-561b2c86-317b-468e-81a2-c6135911835e.png)
