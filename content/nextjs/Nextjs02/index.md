---
emoji: ✍
title: Nextjs Script컴포넌트
date: '2024-02-22 16:08:00'
author: 정중식
tags: next.js
categories: next.js
---

## Nextjs Script컴포넌트란?

- 서버 및 클라이언트 모두에서 JavaScript 코드를 실행하고 데이터를 초기화하는데 사용되는 컴포넌트다.<br/>
  (SSR, CSR 모두 적용 가능함)

- 서버에서 데이터를 미리 가져와 클라이언트로 전달하거나, 클라이언트 측에서 라우팅 또는 페이지 진입시 특정 작업을 수행 할 수 있음

- `서버 사이드 데이터 로딩`: 페이지가 서버에서 처음 렌더링 될 때 데이터 초기화하는데 사용한다.

- `클라이언트 사이드 데이터 로딩`: 페이지가 클라이언트에서 로딩될 때 특정 작업 수행하도록 설정 할 수 있다.

<br/>

사용예시

```js
import Script from 'next/script';

export default function Dashboard() {
  return (
    <>
      <Script src="https://example.com/script.js" />
    </>
  );
}
```

이러면 저 script는 Dashboard라는 페이지 진입시 로드됨

## 주요 속성 정리

- src : 로드할 스크립트 파일 경로 지정
  `EX) src="http://example.com/script"`

- strategy : 스크립트의 로드 전략 설정 (언제 로드/실행 하는지)
  `Ex) strategy="lazyOnload"`

- onLoad : 스크립트가 로드되면 실행할 함수 지정
  `Ex) onLoad ={onLoadFunc}`

- onReady : 스크립트가 준비되면 실행할 함수 지정
  `Ex) onReady ={onReadyFunc}`

- onError : 스크립트 로드 중에 오류가 발생할 때 실행할 함수 지정
  `Ex) onError={onErrorFunc}`

```toc

```
