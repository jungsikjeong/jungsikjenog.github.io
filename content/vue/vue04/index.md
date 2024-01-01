---
emoji: ✍
title: Vuex
date: '2023-01-01 16:08:00'
author: 정중식
tags: vue
categories: vue
---

## Vuex

```
npm install vuex@next --save
```

데이터들을 한곳에 몰아넣고 사용함.
리액트로따지면 리덕스,리코일 등등 같음

단점으로는 코드가 길어질 수 있고, 간단한 수정기능을 만드는데도 코드가 되게 길어짐

그래서 데이터 관리를 많이 안하는 웹이면 `Vuex를`를 사용하고,
간단한 웹은 `mitt`를 사용하자!

## 사용

src/store.js (store라고 작명하는게 보통 관습임)

```js
import { createStore } from 'vuex';

const store = createStore({
  state() {
    return {
      // state를 저장하고싶으면 여기에,
      //ex)
      name: 'kim',
    };
  },
});

export default store;
```

src/main.js

```js
import { createApp } from 'vue';
import App from './App.vue';
import mitt from 'mitt';
let emitter = mitt();
let app = createApp(App);
app.config.globalProperties.emitter = emitter;

import store from './store.js';

app.use(store).mount('#app');
```

참고로 전 게시글 mitt사용법의 main.js와 연동되어있다.
달라진점은 import store와, `app.use(store).`밖에없다.

여기까지 세팅해주면 모든 컴포넌트에서 데이터(state)를 사용할 수 있다.
완전 리액트 리덕스같다.

```js
// 안녕 kim이 출력된다.
<h4>안녕 {{ $store.state.name }}</h4>
```

state를 이런식으로 바로 변경도 가능하다

```js
  <h4>안녕 {{ $store.state.name }}</h4>
  <button @click="$store.state.name = '박'">버튼</button>
  // 버튼 누르면 안녕 박 출력됨
```

근데 Vuex법칙중 하나가, 데이터를 직접 수정하면 안된다고한다.
데이터 추적이 어렵기때문에(리덕스도 그랬음)

## State 수정하는 법

Vuex의 데이터를 수정하려면 다음과 같은 방법을 따르면된다.

1. store.js에 state수정 방법을 정의하고(mutations사용),
2. store.js에 부탁하자. ($store.commit('') 사용)
   <br/>

```js
import { createStore } from 'vuex';

const store = createStore({
  state() {
    return {
      name: 'kim',
      age: 20,
    };
  },

  // 수정방법 정의하는 곳
  mutations: {
    nameChange(state, newName) {
      state.name = newName;
    },
  },
});

export default store;

// 사용
<h4>안녕 {{ $store.state.name }}</h4>
<button @click="$store.commit('nameChange', 'park')">버튼</button>
```

```toc

```
