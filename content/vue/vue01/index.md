---
emoji: ✍
title: Navigation guards
date: '2023-12-30 16:08:00'
author: 정중식
tags: vue
categories: vue
---

> 출처 코딩애플

## 개념

특정 URL로 접속할 때 코드를 실행하고 싶은 경우 사용한다.
예를들면 로그인 유무에따른 페이지를 보여줘야할 때 `Navigation guards`를 사용하면 된다.

리액트로 따지면 hook같은거라고 생각하자.

## 사용법

```js
const routes = [
  {
    path: '/hello',
    component: HelloWorld,
    beforeEnter: (to, from) => {
      return to.fullPath;
    },
  },
];
```

1. 파라미터는 두세개 작명 가능하다.
2. 첫 파라미터는 목적지 페이지,
3. 둘째 파라미터는 출발 페이지다.

`$route`라는 변수랑 똑같이 이용이 가능하다.
예를들면 `to.fullPath`하면 전체 경로를 알려주고,`to.params.id`하면 id파라미터를 알려준다.

> return false는 라우팅을 중단시킨다. return이 없으면 원래의 route인 /hello로 이동시켜준다.

### 여러개의 route에 navigation guard를 추가하고 싶으면?

`.beforeEach()`혹은 `beforeResolve()`를 사용하자.

```js
const router = createRouter({ 어쩌구 });
router.beforeEach((to, from) => {
  //페이지 변경 전에 실행할 코드
});
```

라우팅 하고나서 뭔가 실행하고 싶으면 `afterEach()`를 사용하면 된다.

### Vue 컴포넌트 안에서도 navigation guard사용가능

리액트로 치면 useEffect()같다.

created(), mounted() 이런거랑 비슷하게 활용이 가능하다.

```js
beforeRouteEnter(){}
beforeRouteUpdate(){}
```

위의 두 코드를 `lifecycle hook`쓰는 위치에다가 쓰면 된다.

- 파라미터 두개 입력 가능 - 목적지 to, 출발지 form
- `특정 페이지에 접속했을때 ajax요청할 일이 있으면 사용하자.`

```toc

```
