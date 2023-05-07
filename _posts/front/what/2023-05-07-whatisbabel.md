---
title: '[ Front ] Babel이란?'
author: <author_id>
categories: [ Front, Compilers ]
tags: [ Front, Compilers ]
math: true
toc: true
mermaid: true
---

### Babel

Babel은 현대 JavaScript(ES6 이상)를 이전 버전의 JavaScript(주로 ES5)로 변환(transpile)해주는 컴파일러입니다. 

이는 오래된 브라우저와 호환성을 유지하면서 최신 JavaScript 기능을 사용할 수 있게 해줍니다.

### Babel의 주요 기능들
#### - Syntax Transformations(구문 변환)
  - Babel은 최신 JavaScript 문법(예: 화살표 함수, 클래스, async/await 등)을 이전 버전의 문법으로 변환하여 호환성 문제를 해결해 줍니다. 이를 통해 개발자는 최신 JavaScript 기능을 사용하면서도 구 버전의 브라우저와 호환성을 유지할 수 있습니다.
#### - Polyfills(폴리필)
  - Babel은 새로운 JavaScript 기능 중 일부는 구 버전의 브라우저에서 지원되지 않는 기능을 추가하는 코드인 폴리필을 제공합니다. 예를 들어, Promise, Array.from, Object.assign 등과 같은 새로운 객체와 메서드를 구 버전 브라우저에서 사용할 수 있도록 해줍니다.
#### - Plugins(플러그인)
  - Babel은 다양한 플러그인을 통해 사용자 지정 기능을 추가할 수 있습니다. 예를 들어, JavaScript 프로포절(proposal)을 미리 사용하거나, React JSX 문법을 변환하거나, 코드 최적화를 수행하는 등의 작업을 할 수 있습니다.
#### - Presets(프리셋)
  - 프리셋은 여러 플러그인을 묶어놓은 사전 정의된 설정 집합입니다. 개발자들은 이를 통해 다양한 프로젝트와 요구 사항에 맞게 Babel 설정을 쉽게 구성할 수 있습니다. 예를 들어, @babel/preset-env는 대부분의 경우에 사용되는 표준 프리셋으로, ECMAScript 문법 변환을 지원해주며, @babel/preset-react는 React 프로젝트에 필요한 JSX 문법 변환을 지원해줍니다.

이러한 Babel의 기능을 사용하면 개발자들은 최신 JavaScript 기능을 사용해 개발할 수 있으면서, 구 버전 브라우저에서도 웹 애플리케이션이 정상적으로 동작하도록 할 수 있습니다.
