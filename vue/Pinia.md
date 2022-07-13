# Pinia
![](../../../Users/admin/AppData/Local/Temp/168429298-d9a2e055-82f0-415d-b5d9-215e4f7f3998.png)
-------
## Pinia 란?
<div style="font-size: 17px">
pinia는 Composition API 기반에서 동작하는 상태관리자 입니다.

여태까지 Vue에서 사용되던 가장 보편적이고 유명한 상태 관리자는 Vuex였습니다.

그런데 Vue의 개발자, ***Even You*** 는 본인 트위터에서 Vuex 5와 Pinia는 사실상 완전 동일한 프로젝트로 생각해야 한다고 말한 바 있습니다.

Vuex 5에서 원하던 기능들의 대부분을 이미 Pinia에서 지원하고 있었기에 Vuex 프로젝트를 유지하는 대신 Pinia 를 공식적으로 지원한다고 Pinia의 공식 문서에 적혀 있습니다

### 차이점
 Vuex를 버리고 Pinia를 써야하는 이유에는 어떤 것들이 있을까요?

### Typescript 지원

#### Vuex에서 
Vuex를 이용하여 프로젝트를 구성해보신 적이 있으시다면, Vuex의 상태와 매칭되는 타입 정의가 매우 까다롭다고 생각하셨을 겁니다.

1. Vuex는 module을 지원한다.
2. module은 대부분 각각의 파일에서 구현부가 작성된다.
3. 컴포넌트에서 store를 접근할 때는 this.$store를 통해 Vue의 Prototype에 정의 되어있는 $store 객체를 통해 접근한다.

위와 같은 형태로 Vuex를 이용하기 때문에 사실상 뿔뿔이 흩어져있는 module 파일들에 대한 state 타입을 추록하는게 어렵습니다.

그래서 vuex를 이용하면서 타입 추록도 하려면 아래와 같은 몇가지 과정을 거쳐야 합니다.



```ts
// vuex.d.ts
import { Store } from 'vuex'

declare module '@vue/runtime-core' {
  // declare your own store states
  interface State {
    count: number
  }

  // provide typings for `this.$store`
  interface ComponentCustomProperties {
    $store: Store<State>
  }
}

```
일단, 상태가 하나 추가 및 수정 될 때마다 타입 추록을 위해 state의 구조를 나타내는 d.ts파일을 별도로 작성합니다.

```ts
import type { StateType as AType } from './A';
import type { StateType as BTYpe } from './B';

export type RootState = {
  A: AType,
  B: BType,
};
```
또한 RootState를 얻기 위해 필요하지도 않은 index.ts 파일을 만들어서 모든 module을 하나로 연결 시켜줄 구심점을 구성해야 하며

```ts
import type { RootState } from './index';

export const actions: ActionTree<StateType, RootState> = {
  // ...actions
};
```
모듈을 만들고 Action을 하나 정의할 때마다 ActionTree의 Generic에 전달할 RootState를 index.ts로 부터 끌고 와야 한다는 점이 있습니다.

물론 이 모든 과정은 최초 한 번만 하면 되는게 아니라 어떤 Module의 State가 변하거만 추가되면 다시 해야 합니다!

그래서 Vue2 + Vuex + TypeScript 환경에서 개발할 일이 있을때는 Vuex에 대한 타입 추론은 아예 초기 하고 this.$store를 any로 정의하여 구현해야 할 수도 있다.

#### pinia에서
pinia는 difineStore라는 함수를 이용하여 각각의 파일 마다 별도의 stroe를 정의하여 module 기능을 대신한다.
Vuex의 this.$store와는 달리 Pinia는 defineStore가 반환하는 hook을 이용하여 store에 아주 쉽게 접근 할 수 있습니다.

그렇기에,반환된 hook은 내부 구성 요소에 대한 타입을 포함하고 있으며, 타입 추론에 대한 그 어떤 작업도 추가로 필요하지 않습니다.

```ts
import { defineStore } from 'pinia';

export const useCart = defineStore('cart', {
  state: () => ({
    items: [],
  }),
  actions: {
    addItem(item: ItemType) {
      this.items.push(item);
    },
  },
});
```
cart.ts 파일을 정의하면 ,실제 프로젝트에서는 아래와 같이 사용할 수있습니다.

```ts
<script type="ts">
import { defineComponent } from 'vue';
import { ItemType, useCart } from '@/store/cart';

export default defineComponent({
  name: 'HomePage',
  setup () {
    const cart = useCart(); // cart.items, cart.addItem
    return {
      cart,
    };
  }
});
</script>
```
defineStore 함수가 반환한 커스텀 hook인 useCart를 이용하여 선언만 한다면 state, actions가 모두 변수 cart에 객체로 할당되는 것을 보실 수 있습니다.

## 구성요소

### Vuex에서
Vuex는 아래와 같은 구성요소를 갖습니다.

- namespace
  - module을 별도의 name으로 분리하여 관리할 것인지를 정의하는 프로퍼티
- state
  - 모듈 하나에 하나만 보유 가능
  - 해당 모듈에서 보관할 상태값의 집합
- mutation
  - state를 변환할 수 있는 사실상 유일한 방법
  - 비동기 로직을 처리할 수 없으며, mutation 함수의 첫번째 인자로 현재 state 값을 가져올 수 있다.
- getter
  - state값을 단순히 반환하기만 하는 함수의 집합
  - state값의 수정이 불가능하며, 특정 규칙에 따라 필터링 된 state를 얻을 때 요긴하게 사용된다.
- actions
  - 비동기 처리가 가능하며, state를 변환할 때 쓰는 함수의 집합
  - 직접적으로 state를 변환할 수는 없으며, commit 함수를 통해 mutation을 호출하여 수정이 가능하다.
### Pinia에서
    Pinia는 아래와 같은 구성요소를 갖습니다.

- state
  - store하나에 하나만 보유 가능
  - 해당 store에서 관리 될 상태값의 집합
- actions
  - state를 변환할 때 사용하는 함수의 집합
  - 비동기 처리가 가능하며, vuex와는 다르게 직접 state의 값을 제어할 수 있다.
- getter
  - state값을 단순히 반환하기만 하는 함수의 집합
  - state값의 수정이 불가능하며, 특정 규칙에 따라 필터링 된 state를 얻을 때 요긴하게 사용된다.

Vuex와는 다르게 mutation이 제거되고 actions에서 상태를 모두 제어합니다.
이로 인해 actions에서 state를 제어하기 위해 mutation을 일일히 만들지 않아도 됩니다.

또한, module이라는 개념이 사라지고, 개별적인 store로 관리 되기에 namespace도 없어집니다.

</div>
