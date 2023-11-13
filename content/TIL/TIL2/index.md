---
emoji: ✍
title: 기록2
date: '2023-11-07 11:36:00'
author: 정중식
tags: TIL
categories: TIL
---

## 11월7일

- 팀 프로젝트 - 제품 상세페이지 css 작업 완료

  - 프론트엔드 개발자 회의
    - 각자 해야할 파트 상세하게 적기 (노션)

- 모던 자바스크립트 공부(객체: 기본 파트 공부완료)

  - 가비지 컬렉션 : 눈에 보이지 않는 메모리 관리 수행
  - this: 화살표함수의 this와 메서드의 this는 동작방식이 다름
  - 옵셔널 체이닝 '?': ?. 앞의 대상이 undefined나 null이면 평가를 멈추고 undefined을 반환한다.

- 모던 자바스크립트 공부(자료구조와 자료형 파트중에서 다음의 섹션들 공부)
  - 원시값의 메서드 : 원시값의 종류는 string,number,bigint,boolean,symbol,null,undefined 등 총 일곱가지다.
  - 숫자형
  - 문자열
  - 배열 : 배열의 끝부터 요소를 추가하고, 빼내는 push,pop 메서드와, 배열의 맨 앞에서부터 요소를 추가하고 빼내는 shift,unshift메서드가있다.
    일반적으로 맨 끝에서부터 요소를 추가하고 뺴내주는 `push,pop`메서드가 더 빠르다.

```toc

```

## 11월 8일

- 모던 자바스크립트 사이트에서 공부

  - Map, Set : 키가 있는 데이터를 저장한다는 점에서 객체와 유사하다.
    다양한 자료형을 허용한다.
  - WeakMap,WeakMap.Set : Map 사용법과 동일하지만,가비지 컬렉션이 일어난다. 반복작업(keys(),values(),entries() ..등등) 메서드를 지원하지 않는다.

  - 각종 배열관련 메서드

    - Object.keys(obj) : 객체의 키만 담은 배열을 반환한다.
    - Object.values(obj) : 객체의 값만 담은 배열을 반환한다.
    - Object.entries(obj) : [키, 값] 쌍을 담은 배열을 반환한다.

  - 구조 분해 할당 : 객체나 배열을 변수로 `분해`할 수 있게 해준다.
    ex)

    ```js
    // 이름과 성을 요소로 가진 배열
    let arr = ['Bora', 'Lee'];

    let [firstName, surname] = arr;

    alert(firstName); // Bora
    alert(surname); // Lee
    ```

  - Date 객체와 날짜

## 11월 9일~12일

휴식
