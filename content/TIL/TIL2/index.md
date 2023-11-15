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

## 11월 13일

팀 플젝중 깃 충돌이 일어났다.
각자 브랜치를 따고 푸쉬후 pr을 날려서 자신이 수락하는 형태였는데 이 방식이 문제였다.
앞으로 이런 상황을 방지하고자 프론트엔드 리더분이 다음과 같은 방안을 제시했다.

- 다같이 온라인으로 만나서 1주일 단위로 pr 할 것 (일요일 회의 끝나고 하는걸로)
- pr하기전 정해진 리뷰어가 코드를 확인후 수락해줄것

깃 충돌을 말로만 들었는데 이렇게 광범위한 충돌을 경험한게 갚진 경험인 것 같고 프론트엔드 리더분이 헤쳐나가고, 소통하는거를 지켜보는 것 만으로도 커뮤니케이션 방식과 깃 충돌에 대처하는 것 등등에대해서 한단계 도약한거 같은 기분이다.

## 11월 14일

팀 플젝 작업

- 제품 리스트 페이지 디자인 변경사항 css적용
  - 폰트사이즈, 마진값, 패딩값 기타 등등 적용 <br/>
- 제품 리스트 페이지 카테고리 api통신 적용

- postman에서는 문제없었으나, 로컬(브라우저 환경)에서 api통신할때 401에러 발생
  - 프록시 문제였다. 프론트엔드 리더분이 해결해주셨다.
    현재 플젝 환경이 vite+리액트 환경인데 vite 환경설정 및 axios 설정으로 해결했다.

axios 환경설정한 코드 첨부.

```js
import axios from 'axios';
axios.defaults.withCredentials = true;
const instance = axios.create({
  baseURL: '/api',
  timeout: 1000,
  headers: {
    'Content-Type': `application/json;charset=UTF-8`,
    Accept: 'application/json',
    'Access-Control-Allow-Origin': `http://localhost:주소`,
    'Access-Control-Allow-Credentials': 'true',
    withCredential: true,
  },
});

export default instance;
```

# 11월 15일

팀 플젝 작업

- axios를 사용해서 카테고리 목록을 불러오는 것을 react-query로 바꿧다.

- 향수 데이터 불러오는것을 react-query로 바꿧다.

- react-query 개념을 다시 짚고 넘어갔다.
  - useQuery:일반적으로 데이터 get할때 사용
  - useMutation:put,post,delete할때 사용

<br/>

- 카테고리를 선택하면 url에 query로 찍히는게 어떻겠냐는 제안을 받아서 임시로 구현을 했다.
  Ex) `http://localhost:5001/perfumes?category='프루티'`
  지금 현재는 useState에 카테고리 값이 저장되어있는 상태라, 새로고침을 하면 초기의 카테고리로 돌아가게된다.
  이것은 사용자가 불편을 초래할 수 도 있다는 의견인데.. 나도 이에 동의해서 구현을 해봤다.
  프론트엔드 리더가 참고하면 좋을만한 링크들을 보내줘서 그것을 보고 구현을 해봤다.
  useSearchParams을 활용했다.
