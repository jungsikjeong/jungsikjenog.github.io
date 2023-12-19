---
emoji: ✍
title: 다크모드 구현
date: '2023-12-19 16:08:00'
author: 정중식
tags: stepByStep
categories: stepByStep
---

> 프로그래머스 FE채용과제로 배우는 자바스크립트 강의중, 테스트를 다시 보면서 공부하던중 제가 직접 구현한 코드입니다.

<br/>

## 구현 과제

OS의 다크모드의 활성화 여부를 기반으로 동작하게 하되, 유저가 테마를 토글링 할 수 있도록 좌측 상단에 해당 기능을 토글하는 체크박스를 만드는거였다.<br/>

나는 여기서 추가로 로컬스토리지를 추가하여, 처음 사용자가 웹에 접속하면 OS기반으로 다크모드를 적용시켜주고, 사용자가 토글버튼을 눌러서 다크모드의 활성화 여부를 로컬스토리지에 적용시켜, 다음 접속시 사용자가 설정한 값으로 적용이되게끔 사용자 편의성 측면에서 문제를 접근하여 추가로 구현을 해주었다.

## 구현 코드

```js
// 현재 사용자 테마
const currentTheme = localStorage.getItem('theme');
// 현재 사용자의 os테마 설정값
const osUserTheme = window.matchMedia('(prefers-color-scheme: dark)').matches;
```

사용자가 현재 웹 사이트에서 설정한 테마, 현재 사용자의 os테마 각각의 변수를 설정후 값을 대입 시켜주고,
그 값들을 조건문을 사용하여 값을 변경해주었다.

### 전체 코드

```js
class DarkModeToggle {
  isDarkMode = null;

  constructor({ $target }) {
    const $wrapper = document.createElement('section');
    const $DarkModeToggle = document.createElement('input');
    this.$DarkModeToggle = $DarkModeToggle;
    this.$DarkModeToggle.type = 'checkbox';

    $DarkModeToggle.className = 'DarkModeToggle';
    $target.appendChild($wrapper);
    $wrapper.appendChild($DarkModeToggle);

    $DarkModeToggle.addEventListener('change', (e) => {
      this.setColorMode(e.target.checked);
    });

    this.initColorMode();
  }

  initColorMode() {
    // 현재 사용자 테마
    const currentTheme = localStorage.getItem('theme');
    // 현재 사용자의 os테마 설정값
    const osUserTheme = window.matchMedia('(prefers-color-scheme: dark)').matches;

    if (currentTheme) {
      this.isDarkMode = currentTheme === 'dark' ? true : false;
      this.$DarkModeToggle.checked = this.isDarkMode;
      this.setColorMode(this.isDarkMode);
    } else {
      this.isDarkMode = osUserTheme;
      this.$DarkModeToggle.checked = this.isDarkMode;
      this.setColorMode(this.isDarkMode);
    }
  }

  setColorMode(isDarkMode) {
    document.documentElement.setAttribute('color-mode', isDarkMode ? 'dark' : 'light');
    localStorage.setItem('theme', isDarkMode ? 'dark' : 'light');
  }
}
```

```toc

```
