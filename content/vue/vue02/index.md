---
emoji: ✍
title: 커스텀 이벤트
date: '2023-12-31 16:08:00'
author: 정중식
tags: vue
categories: vue
---

> 계속 사용법 까먹어서 쓰는 글
> <br/>
> Vue에서 하위컴포넌트에서 상위컴포넌트로 이벤트를 전파 할 수 있는데, 이것을 대충 커스텀 이벤트라고한다.

## 하위 컴포넌트에서 상위 컴포넌트로 이벤트 전파

- 대충 하위컴포넌트라고 생각

```js
 <textarea
    ="write-box"
    @input="$emit('write', $event.target.value)"
 >
    글을 작성해보세요!
 </textarea>
```

- 대충 상위컴포넌트

```js
<template>
  <Container
    @write="writeText = $event"
  />
</template>

<script>
  export default {
  name: 'App',
  components: { Container },
  data() {
    return {
      writeText: '',
    };
  },
}
</script>
```

이렇게 해주면 상위컴포넌트의 데이터의 `writeText`에 값이 저장된다.

`$emit('작명',함수 혹은 이벤트)`로 상위컴포넌트에 전달할 이벤트명을 보내주면된다.

사용은 상위컴포넌트에서
`@write="writeText = $event"` 이런식으로 @작명한이벤트명으로 연결해주면 된다.

> 출처 코딩애플

```toc

```
