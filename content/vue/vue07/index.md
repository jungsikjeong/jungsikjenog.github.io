---
emoji: ✍
title: Composition API
date: '2023-01-02 16:08:00'
author: 정중식
tags: vue
categories: vue
---

Composition API를 쓰면 관련있는 코드를 한 곳에 모을 수 있다.

# 기존에는 이렇게 사용했다면..

```js
<template>
  ...
</template>

<script>
export default {
  name:'App',

  methods:{
    ...
  }
}
</script>

<style>

</style>
```

기존에는 methods함수 안에 뭔가를 적고 사용하고 이런식의 방식이였다.<br/>
이런 방식, 기존방식을 Options API라고칭한다.

# Composition API

> created hook 임

## setup

```js
<template>
...
</template>

<script>
export default {
  name: 'MyPage',
  setup() {

  },

  data() {
    return {};
  },
};
</script>

<style></style>

```

setup(){}을 사용해주면 된다.<br/>
컴포넌트를 생성하기전에, 이 코드가 먼저 실행된다. <br/>

이곳에 데이터 생성 및 조작과 methods를 만들 수 있고, hook도 걸 수 있다.

거의 모든 기능개발을 setup 한 곳에서 가능하다.

### setup()안에서 데이터 생성 ref(데이터)

setup()안에서 데이터 생성은 ref()를 사용하면 되고,<br/>
return{}으로 그걸 리턴해주면된다.

```js
<template>
  <div>{{follower}}</div>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'MyPage',
  setup() {
    let follower = ref([]);

    return { follower };
  },

  data() {
    return {};
  },
};
</script>
```

ref()에 데이터를 넣는 이유는,<br/>
vue에서 데이터가 바뀌면 실시간으로 랜더링이 일어날 수 있는 이유는 바로 데이터 타입이 reference data type이기 때문인데, 이 타입을 감지해서 랜더링해주는것이다. 그래서 감싸주는 것임

```js
  setup() {

  },
```

### ajax 요청하기

```js
<script>
import { onMounted, ref } from 'vue';
import axios from 'axios';

export default {
  name: 'MyPage',
  setup() {
    let follower = ref([]);

    onMounted(() => {
      axios.get('/follower.json').then((res) => {
        follower.value = res.data;
      });
    });

    return { follower };
  },

  data() {
    return {};
  },
};
</script>
```

### ref말고 reactive 사용

```js
<script>
import { onMounted,reactive, ref } from 'vue';
import axios from 'axios';

export default {
  name: 'MyPage',
  setup() {
    let follower = ref([]);
    let test = reactive({ name: 'kim' });

    onMounted(() => {
      axios.get('/follower.json').then((res) => {
        follower.value = res.data;
      });
    });

    return { follower };
  },

  data() {
    return {};
  },
};
</script>
```

이렇게 사용해주면 된다.<br/>
reactive는 주로 array,object 데이터를 사용할 때 사용한다.<br/>

근데 굳이 엄격하게 사용하지않고 그냥 사용하겠다면 ref([])에 담아서 사용해도된다.

### 또 있음 props를 받아오는 법

```js
import {toRefs,watch,computed} from 'vue'
setup(props,context){
  // 여기서 one은 다른데서 전달해준 값임
  let {one} = toRefs(props);
  // 1이 나옴
  console.log(one.value)

  // 데이터 변환 감지
  watch(one,()=>{
    // one이 변경될때마다 실행될 코드 작성
  });

  // 데이터 연산결과 저장도 가능 (캐싱)
  let re = computed(()=>{return one.value})
  console.log(re.value)
}
```

1. 첫번째 파라미터는 항상 props고,
2. 두번째 파라미터는 변수같은게 담겨있다.
3. toRefs()로 감싸준다.
4. .value를 사용하면 출력이됨

이 외에도 watch()로 데이터를 감지할 수 있고,
computed()로 데이터 연산결과 저장도 가능하다.

## vuex store 사용법

```js
import {toRefs,watch,computed} from 'vue'
import {useStore} from 'vuex'

setup(props,context){

let store= useStore();
console.log(store.state.name)
}
```

이 밖에도 `store.commit()`과, store.dispatch()를 사용할 수 있다.

근데, Composition API를 사용하면 mapState를 사용 할 수 없다.(Vue3버전 기준)

> 출처: 코딩애플

```toc

```
