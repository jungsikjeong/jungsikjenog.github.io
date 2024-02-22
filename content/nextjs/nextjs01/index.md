---
emoji: ✍
title: Next.js 여러 기능 살펴보기
date: '2024-02-22 16:08:00'
author: 정중식
tags: next.js
categories: next.js
---

> Next.js 13 이전버전임

# getStaticProps

- `정적 페이지 생성`을 위한 데이터 가져오기 함수다.
- 런타임이 아닌, 빌드(build)타임에서만 실행이 되므로, 변동이 거의 없는 데이터 대상으로만 적용하는게 좋다.
  - Ex) FAQ 글 목록리스트 등등..

```js
export async function getStaticProps(){
 const posts = await fetchPosts();
 return{
    props:{
        posts
    }
 }
}
```

<br/>

# getStaticPaths

- `동적 경로`를 위한 정적 경로 생성 함수다.
- 동적으로 생성되는 페이지를 사전 렌더링할 때 사용한다.
  - Ex) 하나의 FAQ 데이터(id:1)가 존재하면, faqs/1 라는 경로를 빌드 타임에 미리 사전 렌더링 할 수 있다.

```js
export async function getStaticPaths(){
 const paths = await fetchDynamicPaths(); // 동적 경로 생성 함수
 return{
    paths,
    tallback:false, // 없는 경로는 404 페이지로 처리
 }
}
```
<br/>

# getServerSideProps

- 서버 사이드 렌더링을 위한 데이터 가져오기 함수
- 매 요청마다 데이터를 서버에서 가져온다
  - 자주 업데이트 되는 posts 데이터들을 외부 API로부터 fetch해서 사전 렌더링 하고 싶을 때 사용함
  
```js
export async function getServerSideProps(){
 const data = await fetchData();
 return{
    props:{
        data
    }
 }
}
```

<br />

# 페이지 라우팅

- 페이지 경로 설정은 pages 디렉토리 내에서 자동으로 처리된다.
  - pages/about.js는 '/about' 경로와 연결됨

<br />

# useRouter

- 페이지 내에서 라우팅을 조작할 수 있는 훅

```js
import {useRouter} from 'next/router';
const router = useRouter();

router.push({
    pathname:'/post/[pid]',
    query:{
        pid:post.id
    }
})

```

<br />

# next/link

클라이언트 사이드 라우팅을 위한 컴포넌트

```js
import Link from 'next/link';

<Link href='/about'>About 페이지로 이동</Link>

```

<br/>

# Next.js 13

- 기존 pages 라우터가 `app 라우터로 변경`
- /app 이라는 새로운 디렉터리로 라우팅 설정 가능
- 레이아웃, 서버 컴포넌트, 스트리밍,데이터 페칭을 지원하는 형태로 업데이트됨
- 기존 pages 파일구조에서 점진적 업데이트 할 수 있도록 지원


```toc

```
