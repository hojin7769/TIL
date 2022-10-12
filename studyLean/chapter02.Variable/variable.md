# 변수란?
- 수학적 의미: '변수變數'를 '변하는 수'
- 프로그래밍적 의미: 변수(variable)란, 값을 저장 할 수 있는 메모리상의 공간을 의미
    - 이 공간에 저장된 값은 변경 될 수 있어 변수라는 수학적 정의와 상통한다.

- #### 하나의 변수에는 단 하나의 값만 저장할 수 있다.
  - 새로운 값을 저장하면 이전의 값은 사라진다.

## 변수의 선언과 초기화
변수를 사용하려면 먼저 변수를 초기화 해야 한다.
```java
 int age; //age라는 이름의 변수를 선언
```
1. 변수 타입 설정
2. 변수 이름 설정

변수의 사용은 변수 이름으로 사용하게 된다.

### 변수 초기화
변수를 사용하려면 반드시 '초기화(initialization)'해야한다. 메모리는 여러 프로그램이 공유하는 자원이므로
전에 다른 프로그램에 의해 저장된 '알 수 없는 값(쓰레기값 garbage value)'이 남아있을 수 있기 때문

변수를 초기화 할때는 '='대입 연산자를 사용한다.   

'='의 의미
- 수학적 의미: 양변이 같다
- 프로그래밍적 의미 : 오른쪽 값은 왼쪽 변수에 저장하라 

ex)
```java
int age = 25;
```

![img.png](img.png)

```java
int a;
int b;
int x =0;
int y = 0;
```

```java
int a , b;
int x = 0 , y = 0;
```

위 아래 코드는 모두 같은 코드이다.


### 두 변수의 값 교환하기
다음과 같은 x,y 두 변수 가 있을때 두 변수의 값을 바꿀려면 어떻게 할까?

```java
int x = 10;
int y = 20;
```
![img_1.png](img_1.png)

위 그림처럼 하면 변수는 모두 같은 값으로 변하게 될것이다. 이미 x 값은 y로 바뀌었기 때문에 이전의 x 값은 존재하지 않기 때문이다.

위 방법 말고 우리는 임시 변수를 만들어 값을 할당하고 사용한다
```java
int x = 10;
int y = 20;
int tmp;
```


![img_2.png](img_2.png)

두변수는 값을 교환하는 것은 마치 두 컵에 담긴 내용뮬을 바꾸려면 컵이 하나 더 필요한 것과 같다.

## 변수의 명명규칙

> 프로그래밍에서 사용하는 모든 이름을 '식별자(identifier)'라 칭한다
> 식별자는 같은 영역 내에서 서로 구분 될 수 있어야 한다.

식별자를 만들때는 반드시 아래의 규칙을 지켜야한다.

> 1. 대소문자가 구분되며 길이에 제한이 없어야 한다
>   - True와 true는 서로 다른 것으로 간주한다
> 2. 예약어를 사용해서는 안된다
>    - true는 예약어라서 사용할 수 없지만, True는 가능하다
> 3. 숫자로 시작해서는 안된다.
>    - top10은 가능자만 7up은 허용되지 않는다.
> 4. 특수문자는 '_'와 '$'만 허용한다
>    - $harp은 허용되지만, S#arp은 허용하지 않는다 

예약어는 키워드 또는 리져브드 워드(reserved word) 라고한다.

-------
### 예약어 종류
<table style="text-align: center">
<tr>
<td>absteact</td>
<td>default</td>
<td>if</td>
<td>package</td>
<td>this</td>
</tr>
<tr>
<td>assert</td>
<td>do</td>
<td>goto</td>
<td>private</td>
<td>throw</td>
</tr>
<tr>
<td>boolean</td>
<td>double</td>
<td>implements</td>
<td>protected</td>
<td>throws</td>
</tr>
<tr>
<td>break</td>
<td>else</td>
<td>import</td>
<td>public</td>
<td>transient</td>
</tr>
<tr>
<td>byte</td>
<td>enum</td>
<td>instanceof</td>
<td>return</td>
<td>true</td>
</tr>
<tr>
<td>case</td>
<td>extends</td>
<td>int</td>
<td>short</td>
<td>try</td>
</tr>
<tr>
<td>catch</td>
<td>false</td>
<td>interface</td>
<td>static</td>
<td>void</td>
</tr>
<tr>
<td>char</td>
<td>final</td>
<td>long</td>
<td>strictfp</td>
<td>volatile</td>
</tr>
<tr>
<td>class</td>
<td>finally</td>
<td>native</td>
<td>super</td>
<td>while</td>
</tr>
<tr>
<td>const</td>
<td>float</td>
<td>new</td>
<td>switch</td>
</tr>
<tr>
<td>continue</td>
<td>for</td>
<td>null</td>
<td>synchronized</td>
</tr>
</table>

-------

> 1. 클래스 이름의 첫 글자는 항상 대문자로 한다.
>   - 변수와 메서드의 이름의 첫 글자는 항상 소문자로 한다.
> 2. 여러 단어로 이루어진 이름은 단어의 첫 글자를 대문자로 한다.
>    - lastIndexOf, StringBuffer
> 3. 상수의 이름은 모두 대문자로 한다. 여러 단어로 이루어진 경우 '_'로 구분한다.
>   - PI,MAX_NUMBER

위의 규칙들은 반드시 지켜져야 하는건 아니지만 개발자의 암묵적인 룰로 정해져 내려온다.

나만의 규칙을 만들시 모든 파일의 명명 규칙을 일관되게 해야 한다.

--------

## 2. 변수의 타입
변수 타입은 크게 문자 , 숫자로 나눌 수 있다.

이 변수의 타입을 자세히 공부해 본다.

----------
### 기본형과 참조형










