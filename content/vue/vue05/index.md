---
emoji: ✍
title: actions
date: '2023-01-01 16:08:00'
author: 정중식
tags: vue
categories: vue
---

## actions

> Vuex..

- ajax하는 곳
- 혹은 오래걸리는 작업들에 사용

사용예시

```js
import { createStore } from 'vuex';

const store = createStore({
  state() {
    return {
     ...
     posts: data,
     moreNumber: 0,
    };
  },

  // 수정방법 정의하는 곳
  mutations: {
     setPost(state, payload) {
      state.moreNumber++;
      state.posts.push(payload);
    },
  },

   actions: {
    // context는 $store를 뜻함
    getData(context) {
      axios
        .get(
          `https://codingapple1.github.io/vue/more${context.state.moreNumber}.json`
        )
        .then((res) => {
          console.log(res.data);
          context.commit('setPost', res.data);
        });
    },
  },

});

export default store;
```

<br />

### 핵심 키워드

1. `actions()`안에서 store의 state를 가져다 쓰려면 `context`를 사용해서 불러오자.
2. mutations안의 함수를 사용할땐 `context.commit('함수', 데이터);` 이렇게!
3. state를 수정할땐 `mutations`를 사용하자!

## 그런데요 mutations에 사용해도되지않을까요?

예를들어

```js
import { createStore } from 'vuex';

const store = createStore({
  state() {
    return {
     ...
    };
  },


  mutations: {
  // 이런식으로..
  함수(){
    axios.get.then()
  }

  },

  actions:{

  }
});

export default store;

```

위와 같이 사용하면 안된다. 왜냐하면,<br/>
`ajax처럼 오래걸리는 코드를 적으면 나중에 길게 코드짤 때 힘들어져서 그렇다고한다.`

> 코딩애플은 예시를들어서 name과 age를 수정하는 ajax요청이 각각 필요한데 만약 3초이상 걸리는 코드들이라면 age가 먼저 바뀔수도있는등 나중에 의도치않은 버그가 생길 수 있다고하는데.. 이거야 어떻게든 해결할 수 있겠지만, 그 해결하기위해선 코드가 길어질수밖에 없는데 이 길어지는 코드때문인것 같다.
> <br/>

그래서 state를 수정하는 mutations 함수는 ajax코드를 넣지말고,
순수하게 state 변경만 하는 함수로 만들어두자.

ajax코드는 `actions` 안에 넣어주자.

> 출처: 코딩애플

```toc

```
