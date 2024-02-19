---
emoji: ✍
title: useMemo와 useCallback 차이
date: '2024-02-19 16:08:00'
author: 정중식
tags: React
categories: React
---

# Memoization

> useMemo와 useCallback은 메모제이션된 값 혹은 함수를 반환하기 때문에 메모제이션 개념을 먼저 알고가자.

메모제이션이란 `기존에 수행한 연산의 결과 값을 어딘가에 저장해두고 동일한 입력이 들어오면 재활용`하는 프로그래밍 기법이다.

다음과 같은 장점이있다.

- 중복 연산을 피할 수 있다.
- 메모리를 조금 더 쓰더라도 애플리케이션의 성능을 최적화 할 수 있다.

# useMemo

- 메모제이션된 `값`을 반환하는 함수다.
- 불필요한 연산을 방지해준다.

```js
useMemo(() => fn, [deps]);
```

`deps` 값이 변하면 ()=>fn 함수를 실행하고,
그 함수의 반환값을 반환 해준다.

> deps dependency의 약자로, 의존성을 뜻한다.
> useMemo가 이 deps 의존하고 있다는것을 뜻한다.

# useCallback

- 메모제이션된 `함수`를 반환해준다.
- 자식 컴포넌트에 props로 함수를 전달할 때 사용된다.
- 외부에서 값을 가져오는 api를 호출할 때 사용된다.

```js
useCallback(fn, [deps]);
```

## 자식 컴포넌트에 props로 함수를 전달할 때 사용하는 경우

```js
function App() {
  const [name, setName] = useState('');
  const onSave = () => {};

  return (
    <div className="App">
      <input type="text" value={name} onChange={(e) => setName(e.target.value)} />
      <Profile onSave={onSave} />
    </div>
  );
}
```

위의 코드를 useCallback를 사용해서

```js
function App() {
  const [name, setName] = useState('');
  const onSave = useCallback(() => {
    console.log(name);
  }, [name]);

  return (
    <div className="App">
      <input type="text" value={name} onChange={(e) => setName(e.target.value)} />
      <Profile onSave={onSave} />
    </div>
  );
}
```

onSave라는 함수를 재사용하는 것으로 자식 컴포넌트의 리렌더링을 방지할 수 있다.

## 외부에서 값을 가져오는 api를 호출하는 경우

```js
import React, { useState, useEffect } from 'react';

function Profile({ userId }) {
  const [user, setUser] = useState(null);

  const fetchUser = useCallback(
    () =>
      fetch(`https://your-api.com/users/${userId}`)
        .then((response) => response.json())
        .then(({ user }) => user),
    [userId],
  );

  useEffect(() => {
    fetchUser().then((user) => setUser(user));
  }, [fetchUser]);

  // ...
}
```

# 참조

[시간이 멈추는 장소](https://narup.tistory.com/273#----%--%EC%--%B-%EB%B-%--%EC%--%--%EC%--%-C%--%EA%B-%--%EC%-D%--%--%EA%B-%--%EC%A-%B-%EC%--%A-%EB%-A%--%--api%EB%A-%BC%--%ED%--%B-%EC%B-%-C%ED%--%--%EB%-A%--%--%EA%B-%BD%EC%-A%B-)

```toc

```
