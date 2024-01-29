---
emoji: ✍
title: 화살표 함수의 특징
date: '2024-01-30 11:36:00'
author: 정중식
tags: javascript
categories: javascript
---

# 화살표 함수의 특징

## 화살표 함수에는 'this'가 없다.

`()=>` 화살표 함수는 this를 내부가 아닌, 외부에서 가져온다.<br/>
그렇기 때문에 다음과 같은 코드를 작성할 수 있다.

```js
let group = {
  title: '1모둠',
  students: ['보라', '호진', '지민'],

  showList() {
    this.students.forEach((student) => alert(this.title + ': ' + student));
  },
};

group.showList();
```

## 화살표 함수는 new와 함께 실행할 수 없다.

`this`가 없기때문에, 화살표함수는 생성자 함수로 사용할 수 없다는 제약이 있다.

## arguments가 없다.

> arguments란? 일반 함수와는 다르게 모든 인수에 접근할 수 있게 해주는 유사 배열 객체를 arguments라고 한다.

## 참조

[모던 자바스크립트](https://ko.javascript.info/closure)

```toc

```
