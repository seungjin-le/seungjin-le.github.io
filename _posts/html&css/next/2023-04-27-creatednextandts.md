---
title: '[ Next.js ] Next + TypeScript 프로젝트 생성'
author: <author_id>
categories: [ Next.js ]
tags: [ Next.js, TypeScript ]
math: true
toc: true
mermaid: true
image: /images/backgrounds/typescript.jpeg
---

### 새로운 프로젝트 생성

```javascript
// npm
npx create-next-app@latest {Project-Name} --ts

// yarn
yarn create next-app {Project-Name} --typescript
```

### 기존에 생성된 프로젝트에 TS설치
1. TypeScript설치
>```javascript
>// npm
>npm install --save-dev typescript @types/react @types/node
>
>// yarn
>yarn add --dev typescript @types/react @types/node
>  ```
>

2. 기존 프로젝트 루트디렉토리에 "tsconfig.json"생성
> 루트디렉토리는 프로젝트 최상위 디렉토리 입니다.
>```javascript
>touch tsconfig.json
>```
>이 파일은 TypeScript 설정을 담당하며, Next.js가 이 파일의 존재를 감지하여 TypeScript를 사용한다고 인식합니다.

3. 'package.json' 파일의 설정 변경
> - 'package.json' 파일의 scripts 섹션에 "dev": "next dev"로 설정되어 있는 부분을 "dev": "next"로 변경합니다. 이렇게 하면 Next.js가 TypeScript 파일을 자동으로 처리합니다.
> - 이제 기존의 JavaScript 파일 확장자를 전부 TypeScript 확장자로 변환합니다.
>   - index.js => index.ts or index.tsx

4. 파일 확장자를 변경후 서버 실행
>```shell
>npm run dev
>```
