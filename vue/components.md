# Component

## Components란?
컴포넌트는 Vue의 가장 강력한 기능 중 하나입니다. 기본 HTML 엘리먼트를 확장하여 재사용 가능한 코드를 캡슐화하는 데 도움이 됩니다.

상위 수준에서 컴포넌트는 Vue의 컴파일러에 의해 동작이 추가된 사용자 지정 엘리먼트입니다.

경우에 따라 특별한 is 속성으로 확장 된 원시 HTML 엘리먼트로 나타날 수도 있습니다.

Vue 컴포넌트는 Vue 인스턴스이기도 합니다. 그러므로 모든 옵션 객체를 사용할 수 있습니다.

(루트에만 사용하는 옵션은 제외) 그리고 같은 라이프사이클 훅을 사용할 수 있습니다.

## 컴포넌트 사용하기

### 전역 등록

이전 섹션에서 다음을 사용하여 새 Vue 인스턴스를 만들 수 있음을 알게 되었습니다.

```
new Vue({
  el: '#some-element',
  // 옵션
})
```

전역 컴포넌트를 등록하려면, Vue.component(tagName, options)를 사용합니다.

```
Vue.component('my-component', {
  // 옵션
})
```

> Vue는 사용자 지정 태그 이름에 대해 [W3C 규칙](http://www.w3.org/TR/custom-elements/#concepts)을 적용하지 않습니다    
> (모두 소문자이어야 하고 하이픈을 포함해야합니다).    
> 그러나 이 규칙을 따르는 것이 좋습니다.   

일단 등록되면, 컴포넌트는 인스턴스의 템플릿에서 커스텀 엘리먼트,   

<my-component></my-component>로 사용할 수 있습니다. 

루트 Vue 인스턴스를 인스턴스화하기 전에 컴포넌트가 등록되어 있는지 확인하십시오.

전체 예제는 다음과 같습니다.

```
<div id="example">
  <my-component></my-component>
</div>
```
 
```
// 등록
Vue.component('my-component', {
  template: '<div>사용자 정의 컴포넌트 입니다!</div>'
})

// 루트 인스턴스 생성
new Vue({
  el: '#example'
})
```

아래와 같이 렌더링 됩니다.

```
<div id="example">
  <div>사용자 정의 컴포넌트 입니다!</div>
</div>
```

