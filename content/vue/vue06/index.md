---
emoji: ✍
title: computed , mapState
date: '2023-01-01 16:08:00'
author: 정중식
tags: vue
categories: vue
---

## vue에는 computed()와, methods()가 존재한다. 어떤 차이점이있을까?

- computed 함수는 사용해도 실행되지않는다. 처음 실행하고 값을 간직한다.(캐싱같은거같음,줄로 계산결과 저장용 함수로 사용함)<br/>

  computed함수는 이름만 사용해서 불러와야한다. 소괄호() 사용을하면 안된다.<br/>
  예를들면 이렇게

  ```js
  <p>{{ computed }}</p>
  ```

  <br/>

- methods함수는 사용할 때마다 실행된다.
  <br/>

## mapState

state 꺼내쓰는 코드가 짧아진다! <br/>

computed:{}안에 작성하는게 일반적이다!

예를들면 이렇게..

```js
<template>
  <p>{{name}}</p>
</template>
<script>

export default {
  name: 'App',
  components: { Container },

  computed: {
    name() {
      return this.$store.state.name;
    },
  },

  data() {
    return {
  ...
    };
  },
  mounted() {
   ...
  },
  methods: {
...
  },
};
</script>
```

중요한점은,<br/>
computed함수는 꼭 `return`을 적어줘야한다.

축약 또한 가능하다.

```js
<template>
  <p>{{name}} {{age}}</p>
</template>
<script>
import {mapState} from 'vuex';

export default {
  name: 'App',
  components: { Container },

  computed: {
    {/* name() {
      return this.$store.state.name;
    }, */}

    {/* 내가 가져오고싶은 vuex Store안의 state들을 적어주면 사용가능 */}
    ...mapState(['name','age']),
    ...mapState({작명:'name'}), // 이런식으로도 가능함
  },

  data() {
    return {
  ...
    };
  },
  mounted() {
   ...
  },
  methods: {
...
  },
};
</script>
```

> 출처: 코딩애플

```toc

```
