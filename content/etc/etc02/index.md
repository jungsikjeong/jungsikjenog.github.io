---
emoji: ✍
title: Tailwind 재사용하기
date: '2024-02-22 16:08:00'
author: 정중식
tags: etc
categories: etc
---

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
