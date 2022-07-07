## 1. Async-Await란?
쉽게 요약하면 JS의 ES6 문법에서 사용하는 비동기 처리 패턴이다.

요즘 Front-end 개발을 하는데 있어서 Ajax/Axios를 사용하는 것은 너무나 많다

실제 사용도 복잡하고 Ajax/Axios를 대체할 수 있는 비동기 처리 방식이 다수 등장했다.


## 2.Promise
Front-end에서 어떤 Framework를 사용하느냐에 따라 다르지만, 일반적으로 Vue에서는 API 호출을 할 떄는  Axios 모듈을 많이 사용한다.

그런데 axios 모듈에서의 request/response는 비동기로 처리되기 때문에 어떤 처리 순서를 지정하지 않으면 request로 요청을 보내고 나서
response로 응답도 받기 전에 다음 구문을 수행해 버리기 때문에 원하는 결과를 받아오지 못한다.

```aidl
(() => {
    const response = axios.get('api/test')
    console.log(response)
})();
```
이런 익명 함수로 axios를 호출한다고 치자 맨아래에 axios에 대한 결과값이 response를 보여주려고 하는데, 결과는 원하는 결과값이 아닌 전혀 이상한 값이 나온다.

```aidl
Promise {<pending>}
	__proto__: Promise
	[[PromiseStatus]]: "resolved"
	[[PromiseValue]]: Object
```
왜냐 JS에서의 문장 처리 순서는 axios()를 사용해서 request를 보내는 연산을 수행하고
response를 언제 받는지는 잘 모르지만, 다음 문장을 수행하기 때문이다. 이러한 상황이기 때문에 순차적 처리를 위해서 
Promise를 사용하는 것이며, 다음과 같이 사용할 수 있다.

```aidl
(() => {
    axios.get('api/test')
        .then(response => {
            console.log(response)
        })
})();
```
간단히 .then을 붙이기만 했는데도 순서가 생겨 버렸다
하지만 여기서 주의해야 할 점은, 순차적으로 처리하는 부분은 .then() 구문내에서만 한정된다.
그말이 무슨 말이냐면

```aidl
(() => {
    axios.get('api/test')
        .then(response => {
            console.log(response)
        })
    console.log('TEST');
})();
```
```aidl
<결과>
TEST
APITEST
```
위 결과 처럼 TEST가 먼저 나오게 된다
왜냐하면, response는 axios로 요청했을 때 결과가 나오면 그걸 받고 위에서 언급했듯이 axios로 

request만 하면 response가 아직 수신이 안된 상황에서도 다음 문장을 시작하기 때문이다.

이러면 뭐가 문제일까? 바로 API를 여러번 호출 할 때 발생한다.

예제를 보자

```aidl
const testFunction = () => {
	axios.get('api/test')
	.then(function(response) {
		console.log(response)

		axios.get('api/test2')
		.then(function(response) {
			console.log(response)		
		})
	})
}
```
코드가 더러워 지고 가독성이 떨어진다

이문제를 Async-Await을 사용하여 해결할 수 있다.

## 3. Async-Await
먼저 Async는 현제 사용할 함수를 비동기로 처리한다는 선언자이다.

다음으로 Await은 비동기로 순차 처리하기 위해서 수행할 API에 붙이는 선언자 이다.

예제를 확인하자
```aidl
const testFunction = async () {
	const response = await axios.get('api/test')
	console.log(response)
}
```
위에 보시다시피 함수 앞에 async가 붙었다 그리고 axios함수 앞에는 await이 붙는다.

앞 예제는 이상한 값이 나왔지만 지금은 값이 잘 나온다.

await를 사용하여 API 함수에 대한 request를 보내고 다음 문장을 수행하는 것이 아니라. request에 대한 response까지 모두 받은 다음에 다음 문장을 
실행하기 때문이다.

그러면 API를 여러 번 호출한다면?

```aidl
const testFunction = async () {
	const response = await axios.get('api/test')
	console.log(response)
	const response2 = await axios.get('api/test')
	console.log(response2)	
}
```

첫 번째 axios 함수를 사용하고 response를 출력하고, 두 번째 axios 함수를 사용한 다음 response를 출력합니다. 맨 위의 Promise의 마지막 예제와 동일합니다.

