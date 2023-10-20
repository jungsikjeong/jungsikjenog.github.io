---
emoji: ✍
title: 자바스크립트 기본
date: '2023-10-20 16:45:00'
author: 정중식
tags: ModernJavaScript
categories: ModernJavaScript
---

## 변수

> `데이터를 담는 이름이 붙은 저장소`라고 생각하자.

<br/>

```js
var message;
let message;
const message;
```

이렇게 `var` 와 `let`, `const` 등으로 변수를 만들 수 있다.<br/>
(`var`는 옛날 방식임) <br/><br/>

가급적이면, 한 줄에 한개의 변수를 작성하자. 읽기가 편하다.

```js
let user = 'John';
let age = 25;
let message = 'Hello';
```

<br/> <br/>

### ❗❗ 변수 주의점 <br/>

변수를 두 번 선언하면 에러가 발생한다는 점만 기억하자.

```js
let message = 'This';

// 'let'을 반복하면 에러가 발생합니다.
let message = 'That'; // SyntaxError: 'message' has already been declared
```

선언한 변수를 참조할 때는 let 없이 변수명만 사용해 참조해야 한다. 이런식으로.

```js
let message = '흠';
message = '변경';

console.log(message); // '변경'
```

<br/>

## 변수 명명 규칙

1. 변수명에는 오직 문자와 숫자, 기호 $와 \_만 들어갈 수 있다.
2. 첫 글자는 숫자가 될 수 없다.
3. 예약어를 변수명으로 사용할 수 없다. EX)let, class, return, function 기타등등..

<br/>

## 상수

> 변화하지 않는 변수, `const`

<br/>

아래처럼 const로 선언한 변수를 '상수(constant)'라고 부른다.  
상수는 재할당할 수 없으므로 상수를 변경하려고 하면 에러가 발생한다.

```js
const myBirthday = '18.04.1982';

myBirthday = '01.01.2001'; // error, can't reassign the constant!
```

<br/><br/>
기억하기 힘든 값을 변수에 할당해 별칭으로 사용하는 것은 널리 사용되는 관습이라고 한다. <br/>
예시)

```js
const COLOR_RED = '#F00';
const COLOR_GREEN = '#0F0';
const COLOR_BLUE = '#00F';
const COLOR_ORANGE = '#FF7F00';

// 색상을 고르고 싶을 때 별칭을 사용할 수 있게 되었습니다.
let color = COLOR_ORANGE;
alert(color); // #FF7F00
```

<br/><br/>

## 바람직한 변수명

변수명은 간결하고, 명확해야 한다. 변수가 담고있는 것이 무엇인지 잘 설명할 수 있어야 한다.<br/>

- userName 이나 shoppingCart처럼 사람이 읽을 수 있는 이름 사용
- 무엇을 하고 있는지 명확히 알고 있지 않을 경우 외에는 줄임말이나 a, b, c와 같은 짧은 이름은 피하자.
- 최대한 서술적이고 간결하게 명명하자.

  - `data와 value는 나쁜 이름의 예시`임. 이런 이름은 아무것도 설명해주지 않는데, 코드 문맥상 변수가 가리키는 데이터나 값이 아주 명확할 때에만 이런 이름을 사용하자.

- 자신만의 규칙이나 소속된 팀의 규칙을 따르도록 하자.
  - 만약 사이트 방문객을 'user’라고 부르기로 했다면, 이와 관련된 변수를 currentVisitor나 newManInTown이 아닌 currentUser나 newUser라는 이름으로 지어야 한다.

## 자료형

자바스크립트에서 값은 `동적 타입`(dynamically typed)을 갖고 있다.

> 동적타입이란? 자료의 타입은 있지만, 변수에 저장되는 값의 타입은 언제든지 바뀔수 있는 타입을 의미한다.

자바스크립트의 변수는 자료형에 관계없이 모든 데이터일 수 있다.
즉 변수는 어떤 순간에 문자열이 될 수도, 숫자가 될 수도 있다.

```js
// no error
let message = 'hello'; // 문자열이 된다.
message = 123456; // 숫자가 된다.
```

## 숫자형

```js
let n = 123;
n = 12.345;
```

- 곱셈 \*, 나눗셈 /, 덧셈 +, 뺄셈 - 등등이 있다.
- NaN은 계산 중에 에러가 발생했다는 것을 알려주는 값이다. 주로 문자열을 숫자와 같이 계산식을하면 NaN이 반환됨
-

## 불린형

논리 타입으로 true와 false 두 가지 값 밖에 없다.

## null 값

null 값은 오로지 null만 포함한다. 어느 자료형에도 속하지 않는다.

## undefined

undefined 값도 null 값처럼 자신만의 자료형을 형성한다.
주로 값이 할당되지 않은 상태를 나타낸다.

그렇다고해서, 다음과 같이 직접 할당하지는 말자

```js
let age = 100;

// 값을 undefined로 바꿉니다.
age = undefined;

alert(age); // "undefined"
```

undefined는 값이 할당되지 않은 변수의 초기값이라는 예약어로 남겨두기 위해서, null을 사용하자

```js
let age = null;
```

## 객체, 심볼

객체(object)는 데이터 컬렉션이나 복잡한 개체를 표현 할 수있다.
심볼(symbol)형은 객체의 고유한 식별자(unique identifier)를 만들 때 사용된다.

## typeof 연산자

typeof 연산자는 인수의 자료형을 반환한다. 자료형에 따라 처리 방식을 다르게 하고 싶거나 변수의 자료형을 빠르게 알아내고자 할 때 유용하다.

## 참조

[모던 자바스크립트](https://ko.javascript.info/)

```toc

```
