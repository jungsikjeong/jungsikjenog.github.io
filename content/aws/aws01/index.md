---
emoji: ✍
title: IAM
date: '2024-02-26 20:56:00'
author: 정중식
tags: aws
categories: aws
---

## IAM이란?

> 참고로, IAM은 지역 설정이 필요없다.

`I`dentity and `A`ccess `M`anagement의 약자로, 유저를 관리하고 접근 레벨 및 권한에 대한 관리를 가능하게 해준다.

<br/>

## 기능

- 접근키(Access Key), 비밀키(Secret Access Key)

- 매우 세밀한 접근 권한 부여 가능(Granular Permission)

- 비밀번호를 수시로 변경 가능케 해줌

  - 한달 또는 분기별로 모든 aws계정들의 비밀번호를 강제로 변경하게함

- Multi-Factor Authentication(다중 인증) 가능

  - 다른 Account를 사용해 보안이 더 두터워지게 만듦(ex:페이스북,구글)

<br/>

## 용어 설명

- 그룹 (Group): 하나의 그룹은 하나 혹은 다수의 User가 존재할 수 있다.

- 유저 (User)

- 역할 (Role): 하나 혹은 다수의 정책을 지정해줄 수 있다. 유저마다 다양한 정책을 부여할 수 있다.

- 정책 (Policy): JSON형태로 되어있는 Document를 가르키며, 세밀한 접근 권한을 일일히 설정하여 만들 수 있다.

```toc

```
