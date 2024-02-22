---
emoji: ✍
title: Tailwind
date: '2024-02-22 16:08:00'
author: 정중식
tags: etc
categories: etc
---

## Tailwind 재사용하기

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer components {
  .btn-primary {
    @apply py-2 px-4 bg-purple-500 text-white;
  }
}
```

이렇게 `@layer` 키워드를 이용해서 설정후

```js
<button className="btn-primary">Save changes</button>
```

이렇게 사용해줄 수 있다.

## Adding Custom Styles

- `tailwind.config.js`파일을 통해서 사용자 정의 스타일 및 커스텀 클래스를 추가 할 수 있다.

```js
/** tailwind.config.js */
module.exports = {
  theme: {
    colors: {
      blue: '#1fb6ff',
      pink: '#ff49db',
    },
    fontFamily: {
      sans: ['Graphik', sans - serif],
    },
    extend: {
      spacing: {
        128: '32rem',
      },
    },
  },
};
```

- 이제 bg-blue를 사용해주면 기존 tailwind 색상이아닌,`#1fb6ff`색상으로 나오게된다.

## Functions & Directives

- Tailwind의 함수와 디렉티브 사용으로 Tailwind를 더욱 확장성있게 사용할 수 있고, 커스텀마이징 할 수있다.
  <br/>

### Functions

- theme(): 테마 값을 동적으로 읽음
- screen(): 미디어쿼리를 동적으로 생성할 수 있음

<br/>

### Directives

- `@규칙(at-rule)` 디렉티브를 사용해서 조건에 따라 요소의 스타일을 조절할 수 있다.

  - @tailwind: HTML 요소에 Tailwind CSS클래스를 동적으로 추가 가능하다.
  - @layer: CSS 규칙을 레이어별로 구성할 수 있게 해준다.
  - @apply: CSS클래스를 동적으로 적용할 수 있다.
  - @config: Tailwind CSS 구성 옵션 변경 가능
