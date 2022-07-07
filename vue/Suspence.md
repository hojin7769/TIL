# Suspense(서스펜스)

## 서스펜스(Suspense)란?
- vue에서는 로딩중일때, 로딩완료 하였을때로 나눠 HTML을 작성한다.
- 페이지에 세 개의 로딩 스피너가 표시되고 콘텐츠가 모두 다르게 렌더링 될 수 있다.
- vue3에 나온 것으로 비동기 작업이 완료될때까지 기다릴 수 있게 해준다.(중첩된 자식 컴포넌트 API 호출이 끝날때 까지 기다린다.)

```aidl
<template>
  <Suspense>
    <template #default>
    <!--비동기 호출이 1개 이상있는 컴포넌트 -->
    </template>
    <template #fallback>
    <!-- 로딩중일때 보여주고 싶은 것 -->
    </template>
  </Suspense>
</template>
```
#default setup() 에 비동기 호출이 있으면 호출이 완료될 때 까지 #fallback을 보여준다. 그 다음 완료되면 #default를 보여준다.

-----
## 오류처리
지금까지 비동기 작업이 성공적으로 해결되었을 때 어떤 일이 발생하는지 살펴 보았지만 실패하고 거부되면 무슨 일이 일어날까?

고맙게도 새로운 ErrorCaptured 수명 주기 후크를 사용하여 이와 같은 오류를 포착하고 적절한 오류 메세지를 표시할 수 있다. 아래 예제를 보자

```aidl
<template>
  <div v-if="error">
   
  </div>
  <Suspense v-else>
    <template #default>
        <--- 화면에 표시할 컴포넌트 ---->
    </template>
    <template #fallback>
      <div>Loading...</div>
    </template>
  </Suspense>
</template>

<script>
import { onErrorCaptured } from 'vue'

setup() {
    const error = ref(null)
    onErrorCaptured(e => {
        error.value = e
        return true
    })
    return { error }
}
</script>
```

위의 예에서는 비동기 작업이 해결 될 때까지 대체 콘텐츠를 표시한다.

무언가 잘못되어 거부되면 onErrorCaptured Vue 후크를 사용하여 오류를 캡처하고 이를 error 속성에 전달하고 대체 콘텐츠 대신 템플릿에 표시합니다.


