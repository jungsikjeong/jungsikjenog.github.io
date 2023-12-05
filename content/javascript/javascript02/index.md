---
emoji: ✍
title: 클로저와 [[Environment]]
date: '2023-12-5 11:36:00'
author: 정중식
tags: javascript
categories: javascript
---

> `요점만 말해` 부분만이라도 읽어보세요!

## 클로저

> 핵심 요약

- 외부 변수를 기억하고 이 외부 변수에 접근할 수 있는 함수를 의미한다.
- 자바스크립트에선 모든 함수가 자연스럽게 클로저가 된다. (예외가 있긴함)

<br/>

### 클로저의 개념

클로저는 내부 함수에서 외부 함수의 범위에 대한 접근을 제공하는 개념이다.
자바스크립트에서 클로저는 `함수 생성 시 함수가 생성될 때 마다 생성된다.` - 그렇기 때문에 `자바스크립트에선 모든 함수가 자연스럽게 클로저가 된다.`

다음은 mdn에서 긁어온 코드이다.
렉시컬 스코프 (어휘적 범위 지정)환경을 고려해서 살펴보면..

```js
function init() {
  var name = 'Mozilla'; // name은 init에 의해 생성된 지역 변수이다.
  function displayName() {
    // displayName() 은 내부 함수이며, 클로저다.
    console.log(name); // 부모 함수에서 선언된 변수를 사용한다.
  }
  displayName();
}
init();
```

위의코드를 간단하게 풀어보자면,

중첩함수인 `displayName()` 내부엔 자신만의 지역변수가 없지만
내부 함수에서 외부 함수에 접근할 수 있기 때문에
`init()`함수에 선언된 지역 변수인 name에 접근할 수 있는 것 이다.
이렇게 내부에서 외부에 접근할 수 있는것. 이것을 `클로저`의 개념이다.

### 조금 더 깊숙히

속담에 호랑이를 잡기 위해선 호랑이 굴로 들어가야한다고 한다.
클로저라는 호랑이를 잡기위해 호랑이 굴로 들어가보자.

아래의 코드는,위에있는 코드와 유사하다. 결과 또한 똑같다.
다른점은 displayName() 내부 함수가 실행되기 전에 외부 함수에서 반환된다는 점이다.

```js
function makeFunc() {
  const name = 'Mozilla';
  function displayName() {
    console.log(name);
  }
  return displayName;
}

const myFunc = makeFunc();
myFunc();
```

왜 그런걸까?

이러한 결과값에 대해서 mdn에서는 자바스크립트 함수가 클로저를 형성하기 때문이라고한다. (조금 더 자세한 사항이 궁금하다면 [여기를 참조](https://developer.mozilla.org/ko/docs/Web/JavaScript/Closures))

똑같은 말이지만, dispalyName()함수를 먼저 리턴을 해주고있는데, dispalyName()함수내부엔 name이없다. 그러면 외부로 거슬러올라가서 `name`이란 지역변수에서 가져오게되는것이다.

<br/>

## [[Environment]]

> 요약

- 자바스크립트의 함수는 숨긴 프로퍼티인 `[[Environment]]`를 이용해 자신이 어디서 만들어졌는지를 기억한다.

- 함수 본문에선 `[[Environment]]`를 이용해 외부 변수에 접근한다.

<br />

## [[Environment]] 개념

모든 함수는 함수가 생성된 곳의 렉시컬 환경을 기억한다고 한다.

> 렉시컬 환경이란? 코드가 어디서 실행되며 주변에 어떤 코드가 있는지를 뜻하며 이를 구현한 것이 실행컨텍스트이다.

함수는 `[[Environment]]`라 불리는 숨김 프로퍼티를 갖는데, 여기에 함수가 만들어진 곳의 렉시컬 환경에 대한 참조가 저장된다.

<br/>

### 클로저와 유사하다.

```js
function makeCounter() {
  let count = 0;

  return function () {
    return count++;
  };
}

let counter = makeCounter();
```

클로저도 내부함수가 외부함수를 참조할수 있다고했다.
`[[Environment]]`프로퍼티 개념도 이와 똑같다고 생각한다.

`makeCounter()`를 호출할 때마다 새로운 렉시컬 환경 객체가 만들어지고, 여기에 `makeCounter`를 실행하는데 필요한 변수들이 저장된다.

위의 예시코드는 makeCounter함수 안의 중첩함수가 외부변수인 count의 외부렉시컬환경을 참조하여 중첩함수의 내부렉시컬환경에 참조시킨것이다.

## 요점만 말해

- 클로저(Closure)는 프로그래밍 언어에서 함수와 그 함수가 선언된 렉시컬 환경(lexical environment) 사이의 조합을 나타냄

- 클로저는 함수가 자신이 선언된 범위 외부의 변수에 접근할 수 있는 특성을 갖고있음

- 자바스크립트에서는 모든 함수가 클로저의 특성을 지니고 있음

- 이는 함수가 선언될 때의 렉시컬 환경에 대한 참조를 유지하며, 이러한 렉시컬 환경은 함수가 호출되어도 사라지지 않음

- 함수가 클로저인 이유는 함수가 선언될 때의 렉시컬 환경에 대한 참조가 함수 객체의 내부 [[Environment]] 프로퍼티에 저장되기 때문임

- 이 [[Environment]] 프로퍼티는 해당 함수가 정의된 스코프의 렉시컬 환경을 가리키며, 함수가 외부 변수에 접근할 때 이 렉시컬 환경을 참조하여 변수에 접근함

- 렉시컬 환경은 변수와 그 변수에 대한 값 또는 참조를 매핑하는데 사용되며, 이를 통해 클로저가 외부 변수에 접근하고 변경할 수 있게 되는 것임

## 참조

[모던 자바스크립트](https://ko.javascript.info/closure)
[mdn](https://developer.mozilla.org/ko/docs/Web/JavaScript/Closures)

```toc

```
