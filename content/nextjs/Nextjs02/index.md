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

### Script: strategy 속성 더 살펴보기

- 스크립트의 로드 전략을 설정할 수 있는 옵션이다. 주로 스크립트가 언제 로드되고 실행할 지 지정한다.

- 다음 네가지 옵션이 있다.

  - afterInteractive(기본값): 스크립트가 페이지 상호 작용 가능한 후에 로드되고 실행됨
    <br/>

  - beforeInteractive: 스크립트가 페이지의 상호 작용 가능한 상태 이전에 로드되고 실행됨
    (hydration 이전) <br/>

  - lazyOnLoad: 스크립트가 페이지가 완전히 로드된 후에 로드되고 실행됨 (브라우저 idle 타임에)
    <br/>

  - worker(experimental): Service Worker와 같은 백그라운드 워커 스크립트를 로드하고 실행하는데 사용
    (오프라인 캐싱이나 알림등)

### Script: onReady 속성과 onLoad속성 더 살펴보기

- onLoad: 스크립트 파일이 브라우저에 성공적으로 로드될 때 호출된다.

  - 스크립트 파일에 추가적인 초기화 작업이 필요한 경우, onLoad를 사용해서 수행가능하다.
  - beforeInteractive과는 사용 불가함.(onReady 사용권장)<br/>

- onReady: 스크립트 파일이 브라우저에 로드되고,스크립트 내 모든 작업이 완료되었으며, 페이지가 상호 작용 가능한 상태가 될 때 호출된다.
  - 스크립트가 완전히 초기화 되고, 페이지의 모든 요소 초기화 + 상호 작용 작업 완료된 후 호출됨

예시

```js
<Script
  id="google-maps"
  src="https://maps.googleapis.com/maps/api/js"
  onReady={() => {
    new google.maps.Map(mapRef.current, { center: { lat: -34.397, lng: 150.644 } }, (zoom: 8));
  }}
/>
```

```toc

```
