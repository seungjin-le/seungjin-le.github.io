---
title: '[ Front ] WebPack이란?'
author: <author_id>
categories: [ Front, bundler ]
tags: [ Front, bundler, WebPack ]
math: true
toc: true
mermaid: true
image: /images/backgrounds/webpack.png
---

### WebPack이란?

![](/images/postImages/front/bundler/webpackbuild.png)

Webpack은 오픈 소스 자바스크립트 모듈 번들러로써 여러개로 나누어져 있는 파일들(이미지, 스타일시트, 폰트 등)을 하나의 자바스크립트 코드로 압축(번들링)하고 최적화 하는 라이브러리 입니다,

웹 애플리케이션 개발에 있어 Webpack은 빌드 및 배포 단계에서 매우 중요한 도구입니다.

### WebPack의 장점

1. 여러 파일의 자바스크립트 코드를 압축하여 최적화 할 수 있기 때문에 로딩에 대한 네트워크 비용을 줄일 수 있습니다.
2. 모듈 단위로 개발이 가능하여, 가독성과 유지보수가 쉽습니다.

### Create-React-App 패키지를 이용하면

리액트를 설치할 때 내부에서 이미 `Webpack`을 사용해서 Development environment(개발 환경)을 생성하며 
사용자에게 기본적으로 `Webpack` 설정 파일을 제공하지 않으며, `Webpack` 설정을 감추고 내부적으로 관리합니다.
이로인해 사용자는 `Create-React-App` 으로 생성한 프로젝트를 별도의 설정 없이 바로 프로젝트를 시작할 수 있습니다.

그래서 리액트를 사용할 때 아무런 설정도 않하고 다른 파일에 있는 `function이나 css, img 등` 을 `import` 하고 사용할 수 있으며
소스코드를 적용하면 바로 반영이 되는 등의 효과를 가져올 수 있습니다.

그 외에도 SnowPack나 Parser와 같은 대체제도 존재합니다.

### WebPack의 구성
- #### Entry(엔트리)
  - 엔트리 포인트는 Webpack이 의존성 트리를 생성하는데 사용하는 시작점입니다. 일반적으로 웹 애플리케이션의 주요 자바스크립트 파일이 엔트리 포인트가 되며 엔드리 포인트를 통해서 필요한 모듈을 로딩하고 하나의 파일로 묶습니다. 여러개의 엔트리 포인트를 설정할 수도 있습니다.
- #### Output(아웃풋)
  - 출력 설정은 번들링 과정에서 Webpack이 생성한 번들 파일의 이름과 저장 위치를 지정합니다. 이를 통해 번들링된 파일들을 저장할 경로를 설정할 수 있습니다.
- #### Loader(로더)
  - 로더는 Webpack이 JavaScript와 JSON만 이해하는 부분을 보완하고자 자바스크립트 파일 외에 다양한 파일 형식을 처리하고 번들에 포함시키기 위해 사용됩니다. 로더는 파일을 읽고 WebPack가 이해하고 처리가 가능한 모듈로 변환하는 작업을 수행합니다. 예를 들어, CSS, img, font 파일 등을 처리할 수 있습니다.
- #### Plugin(플러그인)
  - 플러그인은 Webpack의 빌드 및 최적화 과정에 추가 기능을 제공하는데 사용됩니다. 플러그인은 번들링 과정의 특정 시점에 작동하며 번들링된 결과물들 처리합니다, 플러그인은 다양한 목적으로 사용되며 Loader가 번들하는동안  번들된 크기를 줄이거나, 파일을 압축하거나, 빌드 시 발생하는 오류를 처리하는 등의 작업을 수행합니다.
- #### Mode(모드)
  - 모드 설정은 Webpack이 개발 또는 프로덕션 환경에서 동작하는지를 지정합니다. 개발 모드에서는 빌드 속도를 높이기 위해 최적화 작업을 생략하고, 프로덕션 모드에서는 최적화를 수행하여 최종 결과물의 크기를 줄입니다.
- #### DevServer(개발 서버)
  - Webpack Dev Server는 로컬 개발 환경에서 빠른 프로토타이핑을 돕는 웹 서버입니다. 이 서버는 파일 변경을 감지하고 자동으로 번들을 재생성하고 웹 페이지를 새로고침합니다.
- #### Module(모듈)
  - 모듈은 프로그램을 구성하는 구성 요소의 일부 관련된 데이터와 함수들이 묶여서 모듈을 형성하고 파일 단위로 나뉘는것이 일반적이며, 모듈화 프로그래밍은 기능별로 파일을 나눠가며 프로그래밍을 하는 것으로 유지보수가 쉽다는 장점이 있습니다.

---

### WebPack의 주요 기능들
- #### Module bundling(모듈 번들링)
  - Webpack은 웹 애플리케이션의 코드와 각종 정적 자원을 처리하고 분석하여 의존성 트리를 생성합니다. 이를 통해 웹 애플리케이션의 복잡한 구조를 간소화하고 브라우저에서 쉽게 로드할 수 있는 번들 파일로 변환합니다.
- #### Loader(로더)
  - Webpack은 기본적으로 자바스크립트 파일을 처리할 수 있지만, 로더를 사용하여 다양한 타입의 리소스를 모듈로 변환하고 애플리케이션에 포함시킬 수 있습니다. 예를 들어, CSS, 이미지, 폰트 파일 등을 로더를 통해 처리할 수 있습니다.
- #### Plugin(플러그인)
  - Webpack은 다양한 플러그인을 지원하여 번들링 과정을 더욱 최적화하고 고급 기능을 추가할 수 있습니다. 예를 들어, 번들 크기를 줄이기 위해 난독화와 압축을 수행하는 UglifyJSPlugin, 배포 전에 빌드 폴더를 정리하는 CleanWebpackPlugin 등의 플러그인을 사용할 수 있습니다.
- #### Development server(개발 서버)
  - Webpack Dev Server는 개발 환경에서 빠르게 프로토타이핑을 진행하도록 도와주는 개발 서버입니다. 이 서버는 변경 사항을 감지하면 자동으로 번들을 재생성하고 웹 페이지를 새로고침하여 개발 생산성을 향상시킵니다.
- #### Code Splitting(코드 스플리팅) 및 최적화
  - Webpack은 코드 스플리팅을 지원하여 번들의 크기를 줄이고 초기 로딩 속도를 개선할 수 있습니다. 이를 통해 필요한 모듈을 동적으로 로드하여 애플리케이션 성능을 향상시킬 수 있습니다.

이처럼 Webpack은 웹 개발에서 중요한 최적화 도구이며. 번들링, 최적화, 코드 스플리팅, 모듈 변환 등의 기능을 통해 웹 애플리케이션의 성능을 향상시키고 개발자의 생산성을 높입니다. 또한, Webpack의 플러그인 및 로더 시스템은 매우 확장성이 높아 맞춤형 웹 개발 환경을 구축할 수 있습니다.

