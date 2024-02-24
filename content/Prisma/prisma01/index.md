---
emoji: ✍
title: Prisma,Supabase 세팅 및 사용
date: '2024-02-24 08:46:00'
author: 정중식
tags: prisma Supabase
categories: prisma Supabase
---

# 1

[Supabase](https://supabase.com)에서 회원가입후 프로젝트를 생성한다.

<img src='./1-1.png' alt=' img' />
위의 사진처럼 데이터베이스 패스워드를 작성후,
Region은 한국 서울로해주자

`데이터베이스 패스워드는 추후 prisma 세팅할 때 사용되므로 복사해주자`

<img src='./1-2.png' alt=' img' />
이후 프로젝트가 생성되면 project setting 탭에서 URI를 복사해서 아래에서
prisma세팅할 때 붙여넣어주자.

# 2

`npm i -D prisma`

`npm i @prisma/client`

`npx prisma init`

여기까지 하면 prisma/schema.prisma 파일이 생성되고,

.env 파일에 자동으로 `DATABASE_URL="postgresql://...."` 이 추가된다.

초기에 생성된 .env파일의 DATABASE_URL은 prisma에서 임의로 설정해준것이기 때문에,
이 경로를 위의 `#1`에서 카피한 Supabase의 URI를 넣어주고
`[YOUR-PASSWORD]` 부분엔 `#1`에서 설정했던 데이터베이스 패스워드를 넣어주자

`npx prisma studio` 를 해서 localhost:5555에서 화면이 잘나오면 세팅은 잘 끝난거다.

<img src='./2-1.png' alt=' img' />

에러가 나오는 이유는 아직 데이터베이스 모델링을 안해줬기 때문인데 잘된거임

# 3

```toc

```
