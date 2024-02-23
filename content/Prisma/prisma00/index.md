---
emoji: ✍
title: Prisma
date: '2024-02-23 17:44:00'
author: 정중식
tags: prisma
categories: prisma
---

## Prisma를 구성하는 대표적인 요소들

- Prisma Client: Node.js & TypeScript용 쿼리 작성 클라이언트이다.
- Prisma Migrate: 마이그레이션 시스템을 사용가능
- Prisma Studio: 데이터베이스의 데이터를 보고 편집하는 GUI 툴 제공함

## Prisma 장점

- 개발자가 직접 SQL문을 작성하지 않아도, 데이터베이스와 상호작용할 수 있는 ORM

- 타 ORM과는 달리, 자체적인 스키마 문법을 제공하여 직접 DB마이그레이션, 클라이언트 코드 생성 등의 작업이 가능하다.

- CLI,Prisma Studio등 편리한 GUI도구를 제공하여 생산성 향상

즉 개발자 입장에서 DB작성을위한 코드작성을 줄일 수 있고 스키마 파일 하나만 잘 관리하면 되기 때문에 유지보수가 수월하다.

## Prisma 기능

- Prisma Client: 데이터베이스와 상호 작용하기 위한 자바스크립트 코드를 자동으로 생성해주는 도구.

- 스키마 정의: 데이터베이스 스키마를 정의하고 관리해줌.

- DB 마이그레이션: 데이터베이스 스키마 변경을 추적하고 적용할 수 있는 마이그레이션 기능을 제공함.

- DB 관계 정의: 복잡한 데이터베이스 관계를 정의하고 쿼리 기능을 제공함

예를들면 다음코드처럼 Prisma를 짤 수 있다.

```js
datasource db{
    provider = "postgresql"
    url = env('DATABASE_URL')
}

generator client {
    provider = "prisma-client-js"
}

modal Post {
    id Int @id @default(autoincrement())
    title String
    content String?
    published Boolean @default(false)
    author user? @releation(fields:[authorId],references:[id])
    autorId Int?
}

modal User {
    id Int @id @default(autoincrement())
    email String @unique
    name String?
    posts Post[]
}
```

## Prisma 스키마

> 작성한 스키마를 DB에 반영하기위해선 마이그레이션 명령어 작성해줘야함

- 모델(Modal): 모델은 데이터베이스의 특정 테이블이나 컬렉션과 대응한다. Prisma에서 모델을 정의하면 해당 모델에 대한 데이터베이스 테이블이나 컬렉션이 생성된다.

- 필드(Field): 모델 내에서 필드는 해당 모델이 가지는 데이터 속성을 나타낸다. 각 필드는 데이터 타입과 제약 조건을 가질 수 있다.

- 관계 (Relation): Prisma에서 관계는 모델 간의 연결을 나타낸다. 두 테이블 간의 외래 키 (Foreign Key)를 관리하고 연관된 데이터를 쿼리 가능함

모델,필드,관계는 아래 코드처럼 연결이된다.

```js
datasource db{
    provider = "postgresql"
    url = env('DATABASE_URL')
}

generator client {
    provider = "prisma-client-js"
}

// modal
modal Post {
    /**필드 */ id  Int @id @default(autoincrement())
    title String
    content String?
    published Boolean @default(false)
    author user? @releation(fields:[authorId],references:[id])
    autorId Int?
}

modal User {
    id Int @id @default(autoincrement())
    email String @unique
    name String?
    posts Post[] // 위의 Post modal과 연결
}
```

## Prisma를 활용한 CRUD

### 생성

create API를 사용해서 데이터를 생성한다.

```js
const user = await prisma.create({
  data: {
    email: 'email@example.com',
    name: 'example',
  },
});
```

### 데이터 조회

- findaMany 또는 findUnique를 사용한다.

- where, orderBy, include, select등의 옵션으로 쿼리 조절이 가능하다.

```js
const user = await prisma.user.findMany({
  where: {
    age: {
      gte: 18,
    },
  },
  orderBy: {
    name: 'asc',
  },
  include: {
    posts: true,
  },
  select: {
    id: true,
    name: true,
  },
});
```

### 업데이트

- 하나만 수정하기위해선 update 사용
- 여러 레코드를 한번에 업데이트 하려면 updateMany 사용

```js
const user = await prisma.user.update({
  where: {
    id: '1',
  },
  date: {
    name: 'update Name',
  },
});
```

### 삭제

- 데이터를 삭제하기 위해서 delete 메서드 사용

- 여러 레코드 삭제엔 deleteMany 사용

```js
const user = await prisma.user.delete({
  where: {
    id: '1',
  },
});

const user = await prisma.user.deleteMany({
  where: {
    email: {
      contains: 'prisma.io',
    },
  },
});
```

## 마이그레이션

- 스키마를 DB에 반영하기 위해 마이그레이션을 작성해줘야한다.

`npx prisma migrate dev` 으로 인스톨해주고,

`npx prisma migrate dev --name init` 로 마이그레이션 이름을 만들어줄 수 있다.

- 마이그레이션 된 파일들은 prisma/migration에 생성이된다.

### 마이그레이션 파일 예시

`마이그레이션 파일은 직접 수정하면 안된다고한다.`

항상 prisma migrate 명령어를 통해서만 파일 생성과 디비를 수정해줘야한다.

다음과 같은 파일이 만들어지면, 실제 테이블이 DB에도 만들어지고, 데이터 CRUD가 가능해진다.

```js
-- CreateTable
CREATE TABLE "User" (
    "id" TEXT NOT NULL,
    "email" TEXT NOT NULL,
    "name" TEXT,

    CONSTRAINT "User_pkey" PRIMARY KEY ("id")
);

-- CreateTable
CREATE TABLE "Post" (
    "id" TEXT NOT NULL,
    "title" TEXT NOT NULL,
    "content" TEXT NOT NULL,
    "createdAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP,
    "updatedAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP
    "userId" TEXT,

    CONSTRAINT "Post_pkey" PRIMARY KEY ("id")
);

-- CreateIndex
CREATE UNIQUE INDEX "User_emil_key" ON "User"("email");

-- CreateIndex
CREATE INDEX "Post_userId_idx" ON "Post"("userId");

-- AddForeignKey
ALTER TABLE "Post" ADD CONSTRAINT "Post_userId_fkey" FOREIGN KEY ("userid")
REFERENCES "User"("id") ON DELETE SET NULL ON UPDATE CASCADE;

```
