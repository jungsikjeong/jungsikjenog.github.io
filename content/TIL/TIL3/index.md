---
emoji: ✍
title: 기록3
date: '2023-11-22 11:36:00'
author: 정중식
tags: TIL
categories: TIL
---

# 11월 22일

팀 프로젝트 작업

- 새롭게 디자인된 제품 상세페이지 css 작업
- 로딩때 스켈레톤 이미지 보여주는 작업

# 11월 23일 ~ 11월 24일

팀 프로젝트 작업

- 새롭게 디자인된 제품 상세페이지 css 작업을 했다. (1200px 사이즈로 리디자인됨)
  - 리뷰 컴포넌트 css 작업

제품 상세페이지에 들어가는 리뷰 컴포넌트가 있는데, 고민을 좀 많이했다.
메인 페이지에 있는 리뷰와 제품 상세페이지 리뷰 UI가 겹쳐서 공통컴포넌트로 만들까 고민을했었는데
프론트 리더분께서 공통 컴포넌트 기준은 데이터 기준으로 하는게 나을거라고하셔서 그 말을 따랐다.

그럼 여기서 다시 고민이 되는게, 기존 작업자가 해놓은 리뷰 UI를 그대로 가져다 쓰느냐, 아니면 내가 다시 작업해서 쓰느냐인데
많은 고민끝에 후자로 결정했다.

## 11월 25일

휴식

## 11월 26일

팀 프로젝트 작업

- 팀 프로젝트에서 사용하는 Flex-box 컴포넌트를 리팩토링 했다.

  - 기존에 사용하던 스타일 컴포넌트인 flex-box는 인라인 스타일을 주고있었는데, 이렇게되면 컴포넌트 재랜더링과 성능이슈가 발생할 수 있다고한다.
  - 그래서 기존의 코드에서 useMemo를 사용해서 이슈를 해결하려고했는데,
    이미 아래와같이 인라인 스타일을 주고있어서 무용지물이였다.
    `<div style={display:'flex',...style}>`
    그래서 방법을 찾은게 mui의 `Box sx={{}}` 방식이였다.
    지금 프로젝트의 css를 mui로 하고있어서 가능한 방식이다.

Box 컴포넌트를 활용하여 flex-box 컴포넌트를 만든 예제

```js
import {Box} from '@mui/material'

interface FlexBoxProps {
  children: any
  direction?: any | undefined
  justifyContent?: string
  alignItems?: string
  gap?: string
  style?: any
  onClick?: React.MouseEventHandler<HTMLDivElement>
}

const FlexBox = ({
  children,
  direction = 'row',
  justifyContent,
  alignItems,
  gap,
  style,
  onClick,
}: FlexBoxProps) => {
  return (
    <Box
      role={'presentation'}
      onClick={onClick}
      sx={{
        display: 'flex',
        flexDirection: direction,
        justifyContent: justifyContent,
        alignItems: alignItems,
        gap: gap,
        ...style,
      }}
    >
      {children}
    </Box>
  )
}

export default FlexBox
```

## 11월27일

팀 프로젝트 작업

- 제품 상세 페이지 사소한 UI 버그를 수정해줬다.
- api 연결작업 진행중..

## 11월28일

팀 프로젝트 작업 및 모던 자바스크립트 공부

- 카테고리 컴포넌트에서 화살표를 누를때 400에러가 나는 이유 해결
- 상세페이지 api 연결 작업 완료
  - 향수 이름, 카테고리 이름,태그 연결
  - 노트 섹션 api 연결
- 상세페이지 노트 섹션에서 노트가 4개이상일때 캐러셀로 보여주게하기

- 모던 자바스크립트 재귀와 스택 부분 공부
  - 함수가 자기 자신을 호출하는 것을 재귀라한다.
  - 파트 하단부분의 문제들은 알고리즘 비슷한거같은데 어려워서 해답을 봤다.

## 11월 29일

팀 프로젝트 작업 및 인라인스타일 ,mui sx, mui - Box 차이점 공부

- 데이터를 받아올 동안 스켈레톤 UI를 보여주는 작업 일부 완료
- 인라인 스타일을 지양하는 이유에대해서 공부하고 기록했다.[기록한 곳](https://jungsikjeong.github.io/css/css00/)

## 뒤돌아보기

12월의 내가, 11월의 나를 돌아봤다.

> `나는 게으른가?`

아니다. 나는 해야되는 일이 많아지면 압박감에 잘 수행해내지 못하는것 같다. 정확하게는 게으른게 아니라 회피하는것 같다.
11월의 내 계획은 막연하게 무언가를 많이 해야한다고 계획을 짜놨는데 다음에 또 다음에 하며, 미루고 회피하기를 반복한 것 같다.
이러한 점을 피하지말고 똑바로 인식하고 받아들이고 12월은 어떻게해 나가야할지 수정하고 실행해야겠다.

> 12월의 나는..

- 오늘 할 일과, 이번주 할 일을 계획하고 실행하기
- 너무 타이트하게 계획하지 말기 - 오히려 일정을 빨리끝낼 수 있는 정도의 양만 계획하기
- 압박과 강념에 시달리지 말기

```toc

```
