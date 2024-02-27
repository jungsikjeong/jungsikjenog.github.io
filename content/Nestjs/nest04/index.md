---
emoji: ✍
title: Modal 정의하기
date: '2024-02-27 18:37:00'
author: 정중식
tags: nest.js
categories: nest.js
---

## 모델 정의

> 스키마 정의라고 생각함

게시물을 생성한다고 했을때, 게시물에 필요한 데이터가 어떤것이 필요한지를 정의해주기 위해서 게시물의 모델을 만들어줘야한다.
예를들면 ID, 이름, 설명 등등..

board.model.ts를 생성한다.

<br/>

## 모델 정의할 때

다음 두가지로 정의해 줄 수있다.

- interface정의 : 변수의 타입만을 정의한다.

- classes정의 : 변수의 타입도 체크하고 인스턴스 또한 생성할 수 있다.

다음은 interface의 예이다

/board/board.modal.ts

```js
export interface Board {
  id: string;
  title: string;
  description: string;
  status: BoardStatus;
}

export enum BoardStatus {
  PUBLIC = 'PUBLIC',
  PRIVATE = 'PRIVATE',
}


```

enum은 타입스크립트 열거형 방식으로 PUBLIC과 PRIVATE 둘중 하나만 오게끔 하기위해서 사용해줬다.

이렇게 정의된 모델은 boards.service.ts 파일에서 사용이 가능하다

```js
import { Injectable } from '@nestjs/common';
import { Board } from './board.modal';

@Injectable()
export class BoardsService {
  private boards: Board[] = [];  // 모델 적용

  getAllBoards(): Board[] { // 모델 적용
    return this.boards;
  }
}

```

컨트롤러에 있는 코드에도 Board모델 타입을 정의해 줄 수 있다.

```js
import { Controller, Get } from '@nestjs/common';
import { BoardsService } from './boards.service';
import { Board } from './board.modal';

@Controller('boards')
export class BoardsController {
  constructor(private boardService: BoardsService) {}


  @Get('/')
  getAllBoard(): Board[] /**이부분을 적용시켜줬음 */ {
    return this.boardService.getAllBoards();
  }
}

```

```toc

```
