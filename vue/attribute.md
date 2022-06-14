# Vue.js에서 사용되는 속성및 방법
-----
  ## 1. 데이터 바인딩 data()
-----  
  ```
    <template>
    <div>
        {{sampleData}}
    </div> 
    </template>
    <script>
    export default {
        name:'SampleData',
        components:{},
        data() {
            return {
                samepleData: '테스트',
            };
        },
        setup() {},
        created() {},
        mounted() {},
        unmounted() {},
        methods: {
        }
    }
    </script>
    <style scoped>

    </style>
  ```
  > <결과>
  >> ![image](https://user-images.githubusercontent.com/85658845/173479190-610fe7ec-ab02-469f-86a4-382a4d43ec74.png)
  -----
  ## 2. 원시 HTML 데이터 바인딩 (V-htlm)
  원시 HTML 데이터 바인딩은 데이터 셋에 HTML코드를 입력하여 사용할 수 있게 해주는 방법인다.
  ### <예시>
  -> 잘못된 방법
  ```
    <template> 
    <div>{{htmlString}}</div>
</template>
<script>
export default {
    name:'DataBinding',
    components:{},
    data() {
        return {
            htmlString: '<p style="color:red;"> This is a red String.</p>'
        }
    },
    setup() {},
    created() {},
    mounted() {},
    unmounted() {},
    methods: {
    }
}
</script>
<style scoped> 

</style>
  ```
  <결과>
 
 ![image](https://user-images.githubusercontent.com/85658845/173479976-b96bf1cf-9cc3-4932-9b2b-39310c81add0.png)
 
 <원하는 결과>
 
 ![image](https://user-images.githubusercontent.com/85658845/173480087-156261bf-f429-4165-9851-cb32a1281d67.png)
 
 ```
  <template> 
    <div v-html="htmlString"></div>
</template>
<script>
export default {
    name:'DataBinding',
    components:{},
    data() {
        return {
            htmlString: '<p style="color:red;"> This is a red String.</p>'
        }
    },
    setup() {},
    created() {},
    mounted() {},
    unmounted() {},
    methods: {
    }
}
</script>
<style scoped> 

</style>
 ```
-----

## 3. 입력 데이터 바인딩 (v-model)

-----
vue는 양방향 데이터 바인딩을 지원하여 따로 document.getelementbyid로 그 돔을 가져와 데이터를 확인 안해도 확인이 가능하다.
하는 방법은
> <예시>

![image](https://user-images.githubusercontent.com/85658845/173485643-6e3a8e71-f5ba-47a1-8255-7be20613d77c.png)

![image](https://user-images.githubusercontent.com/85658845/173485665-58339333-6803-4889-b292-ed5516565c6f.png)


```
<template>
    <div>
        <input type="text" v-model="value" />
        <p>{{value}}</p>
    </div> 
</template>
<script>
export default {
    name:'SampleData',
    components:{},
    data() {
        return {
            value:'text'
        };
    },
    setup() {},
    created() {},
    mounted() {},
    unmounted() {},
    methods: {
    }
}
</script>
<style scoped>

</style>
  
```

위 사진과 같이 값을 안가지고 와도 위에 input 값이 바뀌면 아래에 P태그의 value도 함께 바뀌는것을 볼 수 있다.
이를 통해 우리는 data값을 조종 할 수 있다.

-----


  
  
  
