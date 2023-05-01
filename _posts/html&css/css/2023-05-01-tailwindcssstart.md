---
title: '[ Next.js ] Next.js에 TailwindCSS 적용하기'
author: <author_id>
categories: [ Next.js, css ]
tags: [ Next.js, TailwindCSS]
math: true
toc: true
mermaid: true
image: /images/backgrounds/nextjs.png
---

## Install

```jsx
// yarn 
yarn add tailwindcss postcss autoprefixer -D

// npm
npm i tailwindcss postcss autoprefixer -D
```

## Setting

tailwindcss를 설치했다면 다음 `tailwindcss`설정 파일을 루트디렉토리에 생성(**`tailwind.config.js`**)합니다.

```jsx
// yarn 
yarn tailwindcss init -p

// npm
npx tailwindcss init -p
```

### Project / tailwind.config.js

```jsx
module.exports = {
  content: [  // tailwind를 사용할 경로들을 입력
    "./pages/**/*.{js,jsx,ts,tsx}",
    "./components/**/*.{js,jsx,ts,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

마지막으로

`styles/globals.css` 의 기존의 코드를 모두 지우고 코드를 추가해줍니다

```jsx
// @tailwind base : Tailwind의 기본 스타일을 적용하기 위함입니다. 이렇게 하면 프로젝트에서 Tailwind CSS의 기본 스타일(예: 폰트, 마진, 패딩 등)이 적용됩니다.
@tailwind base;

// @tailwind components : Tailwind의 컴포넌트 클래스를 적용하기 위함입니다. 이것은 Tailwind가 제공하는 컴포넌트 스타일과 플러그인에 의해 생성된 추가 컴포넌트 스타일을 적용합니다.
@tailwind components;

// @tailwind utilities : Tailwind의 유틸리티 클래스를 적용하기 위함입니다. 유틸리티 클래스는 개발자가 빠르게 원하는 스타일을 적용할 수 있게 해주는 클래스입니다. 예를 들어, 여백이나 패딩, 글꼴 크기, 색상 등을 조정할 수 있습니다.
@tailwind utilities;
```

### 결과

![img](/images/postImages/css/tailwindcssTest.gif)
