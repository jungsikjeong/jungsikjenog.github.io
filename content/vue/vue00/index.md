---
emoji: ✍
title: vue에서 UI 애니메이션 주는법 두가지
date: '2023-12-28 16:08:00'
author: 정중식
tags: vue
categories: vue
---

> 출처 코딩애플

vue에서 애니메이션 주는 방법이 두가지가 있다고 한다.

## css로 애니메이션 만들기

첫번째 방법으로는, <br/>

1. 애니메이션 시작 전 class를 디자인하고,
2. 애니메이션 동작 후 class를 디자인한다.
3. 원할 때 애니메이션 동작 후 class를 부착하면된다.

코드로 예시를 들면 이렇다.

```js
<div class="start">
    <Modal
      :원룸들="원룸들"
      :누른거="누른거"
      :모달창열렸니="모달창열렸니"
      @closeModal="모달창열렸니 = false"
    />
 </div>

 <style>
    .start {
        opacity: 0;
        transition: all 1s;
    }
    .end {
        opacity: 1;
    }
 </style>
```

div태그에 class명을 start로 붙여놓고, 클릭했을때 end class를 붙이고, 떼는건데
vue에서는 조건문으로 이런식으로 코드를 작성한다.

```js
  <div class="start" :class="{ end: 모달창열렸니 }">
    <Modal
      :원룸들="원룸들"
      :누른거="누른거"
      :모달창열렸니="모달창열렸니"
      @closeModal="모달창열렸니 = false"
    />
  </div>
```

데이터 바인딩과 비슷하게, 클래스 바인딩을 할 수있다.
`:class="{ end: 모달창열렸니 }` 모달창열렸니 이 부분이 true라면 class명에 end가 부착이된다.

## 더 간단하게 <Transition>이용하기

두번째 방법으로 vue에서 제공하는 `Transition`태그를 이용하면 된다.

```js
<template>
  <Transition name="fade">
    <Modal
      :원룸들="원룸들"
      :누른거="누른거"
      :모달창열렸니="모달창열렸니"
      @closeModal="모달창열렸니 = false"
    />
  </Transition>
</template>

<script>
...

</script>

<style>
/* 애니메이션 동작전 스타일 */
.fade-enter-from {
  transform: translateY(-1000px);
}
.fade-enter-active {
  transition: all 1s;
}
/* 애니메이션 동작 후 스타일 */
.fade-enter-to {
  transform: translateY(0px);
}

/* 퇴장 애니메이션 동작전 스타일 */
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
/* 퇴장 애니메이션 동작 후 스타일 */
.fade-leave-to {
  opacity: 0;
}
</style>

```

`Transition`태그의 name이름은 아무렇게나 작명가능한데, 위의예시 코드에서는 fade로 이름을 주었다.
그러면 css코드로 fade-어쩌구-to 이런식으로 지어주면된다.

```toc

```
