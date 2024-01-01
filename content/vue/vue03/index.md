---
emoji: ✍
title: mitt - 컴포넌트간 데이터 전송
date: '2023-01-01 16:08:00'
author: 정중식
tags: vue
categories: vue
---

## npm i mitt

`npm i mitt`

라이브러리니깐
터미널로 설치해주자.

Vuex의 개념까지 알고 다시와봤는데, mitt는 리액트로따지면 contextAPI같은거라고 생각함

## 사용

- main.js

```js
import { createApp } from 'vue';
import App from './App.vue';
import mitt from 'mitt';
let emitter = mitt();
let app = createApp(App);
app.config.globalProperties.emitter = emitter;

app.mount('#app');
```

`app.config.globalProperties`는 글로벌한 변수 보관함이라고 생각하자.

모든 컴포넌트에서 자주 사용하는 라이브러리가있다면 등록해서 사용할 수있다.
예를들면

```js
import { createApp } from 'vue';
import App from './App.vue';
import mitt from 'mitt';
let emitter = mitt();
let app = createApp(App);
app.config.globalProperties.emitter = emitter;

app.mount('#app');
```

이렇게 해주면
import axios 해 올 필요 없이 this.axios로 사용이 가능해진다.

mitt라이브러리로 데이터를 전송할 때 다음과 같이 두가지만 기억하면된다.<br/>

1. this.emitter.emit()로 전송하고,
2. this.emitter.on()으로 수신한다.

이제 본격적으로 mitt라이브러리를 사용해서 컴포넌트간 데이터를 전송해보자.

```js
<template>
  <div
    @click="fire"
  >
  </div>
</template>

<script>
export default {
  name: 'FilterBox',
  props: {
 ...
  },
  methods: {
    fire() {
      this.emitter.emit('작명', '데이터');
    },
  },
};
</script>

<style>
...
</style>
```

`this.emitter.emit('작명','데이터')` 이런식으로 데이터를 쏴주고,

```js
<template>
 ...
</template>

<script>


export default {
  name: 'App',
  components: { ... },
  data() {
    return {
     ...
    };
  },
  mounted(){
    this.emitter.on('작명',()=>{

    })
  },
  methods: {
   ...
  },
};
</script>

<style>
...
</style>

```

`this.emitter.on()`으로 데이터를 수신해주면 된다.
중요한건 항상 mounted(){}안에서 사용해줘야한다.

그리고 개인적인 생각인데

```js
this.emitter.on('작명', function () {});
```

이거 말고

```js
this.emitter.on('작명', () => {});
```

이렇게 사용해주는 이유는..  
크게 상관은없지만 자바스크립트의 this때문이 아닌가 싶다.
()=>{}의 this는 함수 바깥의 데이터를 가르키고,
function(){}의 this는 함수 안쪽의 데이터를 가르키기 때문이지않을까..

## 단점

데이터를 전송할때의 name도 겹치게되면 안되고 하기때문에
많이 사용하게되면 관리하는게 힘들어진다.

대체품으로는: Vuex가 있다고한다.

```toc

```
