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

![image](https://user-images.githubusercontent.com/85658845/177436161-92b7baa4-e8ea-4b01-9032-87095603fa0c.png)

### 지역등록
모든 컴포넌트를 전역으로 등록 할 필요는 없습니다.

컴포넌트를 components 인스턴스 옵션으로 등록함으로써 다른 인스턴스/컴포넌트의 범위에서만 사용할 수있는 컴포넌트를 만들 수 있습니다:

```
var Child = {
  template: '<div>사용자 정의 컴포넌트 입니다!</div>'
}

new Vue({
  // ...
  components: {
    // <my-component> 는 상위 템플릿에서만 사용할 수 있습니다.
    'my-component': Child
  }
})
```

동일한 캡슐화는 디렉티브와 같은 다른 등록 가능한 Vue 기능에도 적용됩니다.

본인이 한 component 방식

```
<script>
import ClickButton from '../components/button/ClickButton.vue';
import EditModal from '../components/modal/EditModal.vue';

export default {
components:{
    "click-button":ClickButton,
		"edit-modal":EditModal,
  },
}
</script>
<template>
	<div class="q-pa-md q-gutter-y-md column items-end">
			<click-button :data = "data" v-on:tt="val => dialog = val"></click-button>
		</div>
		<edit-modal :dialog = 'dialog'  :data = 'data' v-on:backModal="val => dialog = val"></edit-modal>
</template>
```
이런 방식으로 vue 페이지 내에서 등록하여 사용중이다 이 방식을 사용하면 나중에 수정이 필요하면 바로 바로 고칠수 없다는 단점이 존제한다.

## Vue.js Component 설계의 중요성
컴포넌트를 어느 곳에 사용하고 어느 부분이 컴포넌트 화 해야할지에 대해 정확한 설계가 없다면 이 후 전반적으로 문제를 야기한다.

물론 Application을 개발 할 때 모든 항목들을 컴포넌트 단위로 잘게 쪼개도 Application 성능에 크게 영향을 주지는 않지만

규모가 크거나 또는 점점 규모가 커지는(고도화) 프로젝트에서는 해당 프로젝트의 유지관리와 개발 진행 단계에 영향을 준다.

명확한 설계를 무시하고 Vue.js 컴포넌트를 생성했을 때 아래와 같은 문제점들이 있다.

> 1. 전반적인 코드의 가독성과 유지관리 효율성 저하
> 2. 컴포넌트 구조의 복잡성 증가
> 3. 독립적인 컴포넌트로의 변이

### 1. 전반적인 코드의 가독성과 유지관리 효율성 저하
무분별한 컴포넌트의 생성은 코드의 가독성과 앞으로 있을 유지관리에 대한 효율성을 현저히 저하시킨다. 

굳이 컴포넌트를 안 해도 되는 부분까지 나눠서 컴포넌트화 하는 경우가 많다.

그렇다면 어떻게 해야 가독성이 높은 컴포넌트와 효율성을 올릴 수 있을까?

먼저 컴포넌트화 해야 하는 부분을 명확하게 나눠야 한다. 

A라는 부분이 N개의 페이지에서 사용하는 공통적인 항목이라면 컴포넌트로 분리해야하는 것이 바람직하다.

그리고 컴포넌트화 해야 하는 덩어리(chunk)를 굳이 세분화해서 나눌 필요는 없다. 

우리는 컴포넌트를 작성할 때 과감하게 큰 덩어리(chunk) 단위로 나눌 필요도 있다.

## 2. 컴포넌트 구조의 복잡성 증가

뒤에서도 배우겠지만 대부분 컴포넌트의 작성은 Template와 Script 그리고 Style Sheet를 하나의 파일에 작성하는

단일 파일 컴포넌트(Single File Component)로 작성하게 된다.\

이런 컴포넌트에서 props, watch, methods 등의 속성이 무수히 많고 정확한 설계 없이 동작만을 목적으로 하고 작성한다면

이미 이 컴포넌트 복잡한 구조를 가진 컴포넌트이다. 

뿐만 아니라 부모-자식의 참조 역시 어려워지게 된다.

### props
props가 많다는 것은 이미 부모 컴포넌트(Parent Component)에서 많은 속성을 전달하고 있다는 것이다.

이렇게 된다면 이미 이 컴포넌트는 특정한 부모 컴포넌트에 종속된 것이나 다름없는 것이다

그뿐만 아니라 props는 해당 컴포넌트에서 직접적으로 변경이 불가능하기 때문에

이미 넘어온 props를 변경하기 위해서는 바인딩 되어 있는 props를 data에 재 바인딩해야 하는 경우가 많다.

이렇게 되면 자연적으로 watch와 같은 감시자와 상위 컴포넌트로 이벤트를 전달하는 $emit이 많아지게 된다.

### watch
watch가 많다는 것은 이미 해당 컴포넌트에서 반강제적으로 반응 적인 모델이 필요하다는 경우이다. 

이런 watch가 많아지게 되면 해당 컴포넌트를 다른 곳에 반인딩하였을 때 의도치 않은 동작을 야기할 수 있다.

특히 이런 경우엔 유지보수가 매우 어렵다. 이미 이 watch에 종속된 기능이 거미줄처럼 엉켜있기 때문이다.

특히나 Vue.js의 반응 적 모델은 Application의 성능에 직접적인 연관을 주기도 하기 때문에 watch를 최소화하는 것이 좋다.

위와 같은 컴포넌트의 복잡성 증가를 해결하기 위해서는
> - props는 해당 컴포넌트에서 절대적으로 필요한 요소로 생성하고
> - watch의 사용을 최소화하고
> - 공통적인 methods와 같은 Script들은 javaScript 파일로 별로 분리하는 것이 좋으며
> - 컴포넌트 간의 깊은 바인딩(deep)은 자제해야 한다.

## 부모 컴포넌트에서 자식 컴포넌트로 정보를 주는 방법

### Props란?
모든 컴포넌트 인스턴스는 각자의 자체 격리된 범위(scope)기 있다. 이때문에 하위 컴포넌트의 템플릿에서는

상위 데이터를 직접 참조할 수 없는데, <span style="background:gray;color:black;">props</span>를 사용하면 하위 컴포넌트로 데이터를 전달 할 수 있습니다.

![img.png](./imgs/componentImg.png)

<code>props</code>는 상위 컴포넌트의 데이터를 전달하기 위한 사용자 지정 특성
하위 컴포넌트에서는 <code>props</code> 옵션을 사용해 수신할 것으로 기대되는 <code>props</code>를 명시적으로 선언

#하위컴포넌트 js
```js
Vue.component('child', {
  // props 정의
  props: ['message'],
  // 데이터와 마찬가지로 prop은 템플릿 내부에서 사용할 수 있으며
  // vm의 this.message로 사용할 수 있습니다.
  template: '<span>{{ message }}</span>'
})
```
그런 다음 일반 문자열을 다음과 같이 전달할 수 있습니다.(리터럴 방식)

＃ 상위 컴포넌트 html template
```vue
<child message="안녕하세요!"></child>
```
이렇게 하면 상위 컴포넌트에서 message에 담은 <code>안녕하세요!</code>라는 문자열을 하위 컴포넌트의 message로 보내줄 수 있다.

하지만 이 방식은 동적 바인딩은 아니라서, 상위 컴포넌트의 데이터가 변해도 하위 컴포넌트에는 반영이 되지 않는다.

# 동적Props
v-bind를 사용하면 부모 (상위 컴포넌트)의 데이터를 동적으로 바인딩해 자식(하위 컴포넌트)
에게 전달할 수 있다. 데이터가 상위에서 업데이트 될 때마다 하위 컴포넌트로도 전달된다.

＃ 상위 컴포넌트 html template
```vue
<div>
  <input v-model="parentMsg">
  <br>
  <child v-bind:my-message="parentMsg"></child> # 동적 바인딩
</div>
```
v-bind는 아래와 같이 : 을 활용해 단축 구문으로 사용하는 경우가 더 많습니다.

```vue
<child :my-message="parentMsg"></child>
```
전달하고 싶은 데이터가 객체라면, 인자 없이 v-bind를 써도 전달 가능합니다. (v-bind:prop-name 대신 v-bind:객체명)

예를 들어 todo라는 객체가 있다면,

```vue
# 상위 컴포넌트 js
todo: {
  text: 'Learn Vue',
  isComplete: false
}
```
아래의 두 가지 작성 방식은 같은 동작을 한다. 각자의 props를 바인딩 하는 것과 객체로 바인딩 하는 방식이

가져오는 효과는 같다.
```vue
# 상위 컴포넌트 html template
1)
<todo-item v-bind="todo"></todo-item>

2)
<todo-item
  v-bind:text="todo.text"
  v-bind:is-complete="todo.isComplete"
></todo-item>
```
또는 다른 방법으로는

```vue
#부모페이지
<uploadCom :alert="alert"  :confirm="confirm" ></uploadCom>
```
```js
import UploadCompVue from '../components/alert/UploadComp.vue';

export default {
    components: {
         uploadCom : UploadCompVue,
    },
}
}
```

```vue
#자식페이지
<template>
  <div>
    <q-dialog v-model="props.alert">
      <q-dialog v-model="props.confirm" persistent>
        <q-card>
          <q-card-section class="row items-center">
            <q-avatar
              icon="signal_wifi_off"
              color="primary"
              text-color="white"
            />
            <span class="q-ml-sm"
              >You are currently not connected to any network.</span
            >
          </q-card-section>

          <q-card-actions align="right">
            <q-btn flat label="취소" color="primary" v-close-popup />
            <q-btn flat label="확인" color="primary" v-close-popup />
          </q-card-actions>
        </q-card>
      </q-dialog>
    </q-dialog>
  </div>
</template>
<script>
export default {
  name: "SampleData",
  components: {},
  data() {
    return {};
  },
  props: {
    alert: {
      type: String,
      default: "false",
    },
    confirm: {
      type: String,
      default: "false",
    },
  },
  setup(props, { emit }) {
    return {
      props,
    };
  },
  created() {},
  mounted() {},
  unmounted() {},
  methods: {},
};
</script>
<style scoped></style>

```

이런식으로 props를 이용해 데이터를 줄수 있다.

## 자식에서 부모로 정보 넘겨주기
Emit은 자식에서 부모로 이벤트를 전달하는 역활을 한다.
자식에서는 그 메서드를 $emit()에 작성하고 그 상위 부모에서는 v-on 속성으로 구현한다.

```vue
//이벤트 발생
this.$emit('이벤트명');
```

```vue
// 이벤트 수신
<child-component v-on:이벤트명="상위 컴포넌트의 메서드명"></child-component>
```

$emit()을 호출하면 괄호 안에 정의된 이벤트가 발생한다.
그리고 일반적으로 $emit()을 호출 하는 위치는 하위 컴포넌트의 특정 메서드 내부이다.
따라서 $emit()을 호출할 때 사용하는 this는 하위 컴포넌트를 가르킨다.

호출한 이벤트는 하위 컴포넌트를 등록하는 태그(상위 컴포넌트의 template 속성에 위치)에서 v-on:으로 받습니다.
하위 컴포넌트에서 발생한 이벤트명을 v-on: 속성에 지정하고,
속성의 값에 이벤트가 발생했을 때 호출될 상위 컴포넌트의 메서드를 지정합니다.

예제 

```vue
<template>
  <q-btn-group push>
    <q-btn push label="목록" @click="listback" />
    <q-btn push label="수정" @click="$emit('tt', true)" />
    <q-btn push label="삭제" @click="deleteSeq" />
  </q-btn-group>
</template>
<script>
import { reactive } from 'vue';
import { callUrl } from '../../assets/js/ui';
import router from '../../router';
export default {
  name: 'ClickButton',
  props: {
    data: {
      seq: {
        type: String,
        default: '0',
      },
      title: {
        type: String,
        default: '0',
      },
      content: {
        type: String,
        default: '0',
      },
      writer: {
        type: String,
        default: '0',
      },
      writeDay: {
        type: String,
        default: '0',
      },
    },
  },
  emits: ['tt'],
  setup(props, { emit }) {
    const listback = () => {
      router.addRoute({
        component: () => import('../..//views/ListView.vue'),
        name: 'list',
        path: '/list',
        props: true,
      });
      router.push({ name: 'list' });
    };
    const deleteSeq = () => {
      const param = {
        NO_SEQ: props.data.seq,
        DS_TITLE: props.data.title,
        DS_CONTENT: props.data.content,
        ID_USER: props.data.writer,
        MapperId: 'BoardMapper.delete',
      };
      if (!confirm('삭제하시겠습니까?')) return false;
      callUrl('save', param)
          .then(function (response) {
            if (response.status == '200') {
              alert('삭제되었습니다.');
              location.href = '/list';
            }
          })
          .catch(function (error) {
            console.log(error);
          });
    };
    const onEmit = function () {
      emit('print', true);
    };

    return {
      listback,
      deleteSeq,
      onEmit,
    };
  },
};
</script>

```

위에 코드를 보는것과 같이 vue3에서는 this라는 개념이 약하기 때문에 emit을 setup에 적역으로 등록을 해 놓고 사용한다.

그럼 넘겨주는 저 string 이름으로 v-on: 속성에 사용한다



