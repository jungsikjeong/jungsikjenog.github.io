---
emoji: ✍
title: NestJS Controller
date: '2024-02-27 16:42:00'
author: 정중식
tags: nest.js
categories: nest.js
---

## Controller란?

컨트롤러는 들어오는 요청을 처리하고 클라이언트에 응답을 반환하는 로직을 뜻한다.

<img src='./controller.png' />

컨트롤러는 `@Controller` 데코레이터로 클래스를 데코레이션 하여 정의한다.

```js
@Controller('/boards') // /boards의 컨트롤라고 명시해준것
export class BoardsController {
  @Get()
  getBoards(): string {
    return 'This action return all boards';
  }
}
```

## Handler란?

핸들러는 @Get, @Post, @Delete 등과 같은 데코레이터로 장식 된 컨트롤러 클래스 내의 단순한 메서드를 칭한다.

```js
@Controller('/boards') // /boards의 컨트롤라고 명시해준것
export class BoardsController {
  @Get() // ()인자안에 경로를 넣어줄수 있다. EX) @Get(/id)
  getBoards(): string {
    return 'This action return all boards';
  }
}
```

## Board Controller 생성하기

> \*부분은 컨트롤러의 이름을 명시해준것
> --no-spec는 test파일을 생성하지 않는것을 명시해준것인데, 원래는 생성을해준다.

`nest g controller boards* --no-spec`

위의 명령어를 입력하면 자동으로 Board Module에 컨트롤러를 연결시켜준다

```js
import { Module } from '@nestjs/common';
import { BoardsController } from './boards.controller';

@Module({
  controllers: [BoardsController], // *  이부분이 자동으로 써짐
})
export class BoardsModule {}
```

## CLI로 명령어 입력시 순서

즉 CLI로(nest g ....) 입력시 다음과 같은 순서로 만들어진다.

1. cli는 먼저 boards라는 폴더를 찾는다.
2. boards폴더 안에 controller파일을 생성한다.
3. boards폴더 안에 modules 파일을 찾는다.
4. modules 파일 안에 controller을 등록해준다.

```toc

```
