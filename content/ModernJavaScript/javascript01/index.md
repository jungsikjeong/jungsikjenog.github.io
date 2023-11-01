---
emoji: ✍
title: 폴리필,바벨
date: '2023-11-01 11:36:00'
author: 정중식
tags: javascript
categories: javascript
---

## 폴리-필(Polyfill) 이란?

- 브라우저에서 지원하지 않는 코드를 사용 가능한 코드 조각이나 플러그인으로 변환한 코드를 의미한다.
- 즉,`최신 자바스크립트의 기능을 구식 자바스크립트 코드로 똑같이 구현한 코드`를 의미함.

## 바벨(babel)

- 트랜스파일러(transpiler)다. 모던 자바스크립트를 구 표준을 준수하는 코드로 변환.
- 웹팩(webpack)과 같은 모던 프로젝트 빌드 시스템은 코드가 수정될 때마다 자동으로 트랜스파일러를 동작시켜줌.
- 주요역할

1. 트랜스파일러: 코드를 재작성함
2. 폴리필(core js, polyfill.io)

## 바벨과 폴리필의 차이

- 바벨은 ESNext 에서 지원하는 문법을 ES5 문법으로 번역해주지만, ES5에 존재하지 않는 ES6의 Map, Promise, Set, Object.assigin() 이런애들은 존재하지 않으니 번역을 해줄수가 없다.

- 이것을 매꾸기 위해 polyfill 을 사용한다. (Map, Promise, Set 등을 사용가능한 객체로 만들어준다)

- babel 은 babel-polyfill 모듈을 사용하면 되지만, 현재 deprecated 되었기 때문에 core-js와 regenerator-runtime을 직접 사용하는 방식을 제안하고 있다.

## 참조

[모던 자바스크립트](https://ko.javascript.info/polyfills)
[폴리필 이란?](https://velog.io/@katanazero86/polyfill%ED%8F%B4%EB%A6%AC%ED%95%84-%EC%9D%B4%EB%9E%80)

```toc

```
