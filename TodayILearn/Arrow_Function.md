# 화살표 함수 (Arrow Function)

## 화살표 함수란?
화살표 함수에 대해 정식 사이트에서는 이렇게 설명하고 있다.  

화살표 함수 표현(arrow function expression)은 전통적인 함수표현(function)의 간편한 대안입니다. 

하지만, 화살표 함수는 몇 가지 제한점이 있고 모든 상황에 사용할 수는 없습니다.

- this나 super에 대한 바인딩이 없고, methods 로 사용될 수 없습니다.
- new.target키워드가 없습니다.
- 일반적으로 스코프를 지정할 때 사용하는 call, apply, bind methods를 이용할 수 없습니다.
- 생성자(Constructor)로 사용할 수 없습니다.
- yield를 화살표 함수 내부에서 사용할 수 없습니다.

이렇게 설명이 나와있다.

다시 풀어 보자면 화살표 함수는 ES6때 부터 사용가능해진 또 하나의 함수표현이라고 할 수 있다.

기존 function \[함수명](){} 이 구조에서 () => {} 식으로 표현을 할 수 있다.

예를 들어 
```
const sum = function(x, y) { 
  return x + y; 
} 

sum(3, 4);
```
현재 이런 함수가 정의되어 있다고 해보자

그럼 이 함수를 화살표 함수를 사용하면

eturn명령어 없이도 함수 실행을 종료시키고 값을 반환한다.

화살표함수를 이용해 위 함수를 아래와 같이 표현할 수 있다.

```
const sum = (x, y) => x + y;

sum(3, 4); //7
```

## 함살표 함수의 특징

맨위에서 설명을 했듯이 화살표 함수를 모든 경우에 사용할 수 있는건 아니다.

그렇다면 지금부터 화살표함수의 특징을 알아보자

### 1. 화살표 함수의 기본 문법
var/let/const 함수명 =  (매개변수)  => { 실행문 }

```
var foo = (a,b)=> {
return (a+b)*10;
};
```
만일 매개 변수가 하나라면, 다음과 같이 소괄호를 생략할 수 있다.

두 개 이상일 경우에는 반드시 소괄호() 사용해야한다

```
 var foo = a => {
      return a * 10;
    }; 
```

만일 함수가 하나의 실행문만을 가지고 있다면, 중괄호를 생략하고 한 줄에 표기할 수 있다.

이경우 실행문의 결과가 함수의 반환값이 된다.

```
var foo = (a, b) => a + b; 

foo(1, 2); //3 (foo 화살표함수의 반환값)
```

### 2. 기본적으로 화살표함수는 익명 함수로만 사용할 수 있기 때문에, 함수를 호출하기 위해서는 표현식으로 써야한다.

***익명함수(Anonymous function):*** 함수를 재사용하지 않을 목적으로 함수에 이름을 붙이지 않는 것.

```
//표현식을 이용한 화살표함수 
var addNumber (a, b) => {
  return a + b; 
}; 

//표현식을 이용하지 않은 화살표함수 
function (a, b) => { 
  return a + b; 
}; //Uncaught SyntaxError: Function statements require a function name
```
화살표함수는 일반함수보다 간결하게 콣백함수로 사용될 수 있다.

```
 var number = [1,2,3,4,5];
 var newArray = number.map(a=> a + a);
 console.log(newArray); //[2,4,6,8,10]
```

***.map()메서드:*** 배열 내 모든 요소에 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환하는 메서드

### 3. 화살표함수를 사용 할 수 없는 경우
1) 객체의 메소드를 정의하는 경우
2) prototype에 메서드를 할당하는 경우
3) 상성자 함수로 사용하는 경우

----------
## 화살표함수와 this

함수가 어떻게 호출되었는지에 따라 바인딩할 객체가 결정되는 일반함수와는 달리,

화살표함수의 this는 화살표함수가 호출되는 시점과는 무관하게 ***선언되는 시점에 결정***되며

***언제나 상위 스코프의 this를 가르킨다***

왜냐하면,

***화살표함수에는 this와 argument가 없기 때문이다.***

그래서 일반적으로 this가 개입되는 경우라면 일반 함수를 사용한다.

```
var obj = { 
    myName: 'Barbie', 
    logName: function() { 
        console.log(this.myName); 
    }
};

obj.logName();   //"Barbie"
//콜백함수로 일반함수표현방식을 사용하면 dot notation법칙에 따라 this는 obj객체가 된다. 
```
만일 위 예제를 화살표함수로 표현할 경우, this는 달라진다.

```
var obj = { 
    myName: 'Barbie', 
    logName: () => { 
        console.log(this.myName); 
    }
};

obj.logName();   //undefined 
/*콜백함수로 화살표함수를 사용하면 이 예제의 경우 this는 상위 스코프인 전역스코프 혹은 
window객체가 된다. 
현재 상위 스코프에는 변수 myName이 존재하지 않으므로 undefined를 반환한다.*/
```
따라서 window객체에 myName의 값을 할당해주면 아래와 같은 결과를 얻게 된다.

```
window.myName = "Hannah"; 
var obj = { 
    myName: 'Barbie', 
    logName: () => { 
        console.log(this.myName); 
    }
};

obj.logName();   //"Hannah"
//여기서 this는 obj객체의 상위스코프의 this인 window객체가 된다. 
```

화살표함수의 this 바인딩 객체 결정방식은 렉시컬 스코프(Lexical Scope)와 유사하다.

***렉시컬 스코프(Lexical Scope): 함수를 어디서 선언하였는지에 따라 상위 스코프가 정해지는 방식. 자바스크립트를 비롯한 대부분의 프로그래밍 언어는 렉시컬 스코프를 따름. ↔ 동적 스코프(Dynamic Scope)***

화살표 함수에서 this를 사용할 경우 일반 변수와 동일하게 스코프 체인을 따라 탐색하게 되는 것이다.

마지막으로 예제 하나 더

```
var status = "😎";

setTimeout(() => { 
  const status = "😍"; 
  
  const data = { 
    status: "🥑", 
    getStatus: function() { 
      return this.status;
    }
  }; 
  
console.log(data.getStatus.call(this));        //😎
```

위 예제의 맨 아랫줄 this를 가지고 있는 함수는 setTimeout() 화살표함수이다.   

하지만 앞서 언급한 바와 같이 화살표함수는 this를 갖고 있지 않으므로, 예제의 this값은 상위 스코프인 global scope의 this 가 된다.   

따라서 this.status는 😎를 반환하게 된다.   

------

## 참고

https://poiemaweb.com/es6-arrow-function
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Arrow_functions
https://saegeullee.github.io/category/javascript/javscript-es5-and-es6/#arrow-functions
