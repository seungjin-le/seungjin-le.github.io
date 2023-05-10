---
title: '[ Front ] 브라우저의 렌더링 원리'
author: <author_id>
categories: [ Front, CS ]
tags: [ Front, CS ]
math: true
toc: true
mermaid: true
image: /images/backgrounds/cs.png
---

### 브라우저의 렌더링 원리
브라우저가 화면에 나타나는 요소를 렌더링 할때, 웹킷(Webkit)이나 게코(Gecko) 등과 같은 `렌더링엔진` 을 사용합니다. 렌더링 엔진이
HTML, CSS, JavaScript로 렌더링할 때 `CRP`라는 프로세스를 사용하며 여러 단계들로 실행됩니다.

1. #### 요청 및 응답 (HTTP Request and Response) 
   - 사용자가 주소창에 URL을 입력하거나, 링크를 클릭하면 웹 브라우저는 해당 웹 페이지의 서버에 HTTP 요청을 보냅니다. 서버는 응답으로 HTML 문서, CSS, 자바스크립트 파일 등을 반환합니다.
2. #### HTML 파싱 (Parsing) 
   - 브라우저는 응답받은 HTML 문서를 파싱하여 DOM 트리를 생성합니다.
     - 파싱중 `<script>` 태그를 만나면 파싱을 `잠시 중단`하고 `자바스크립트 파일 또는 코드를 실행`하며, `자바스크립트 파일 실행이 끝나면 HTML 파싱을 재개`합니다.
     - #### 자바스크립트 실행 (JavaScript Execution) 
       - 자바스크립트 코드가 실행되면 DOM 요소를 추가, 수정, 제거할 수 있습니다. 자바스크립트는 페이지를 동적으로 변경하고 상호작용성을 추가함으로써 렌더링 과정에 영향을 줍니다. 자바스크립트 코드 실행이 완료되면, DOM 트리는 변경된 상태로 업데이트됩니다.
3. #### CSS 파싱
   - 브라우저는 CSS 파일과 HTML 문서에 포함된 `<style>` 태그 내부의 CSS 코드를 파싱하여 `CSSOM(CSS Object Model)` 트리를 생성합니다.
4. #### 렌더 트리 생성 (Render Tree Construction)
   - 생성된 DOM 트리와 CSSOM 트리를 합쳐 렌더 트리를 만듭니다.
5. #### 레이아웃 (Layout) 
   - 렌더 트리를 통해 브라우저는 각 요소의 크기, 위치 등의 정보를 계산하고 뷰포트에 배치합니다. 이 과정을 레이아웃이라고 합니다.
6. #### 페인팅 (Painting)
   - 레이아웃 단계에서 계산된 요소들을 화면에 그립니다. 요소의 배경색, 텍스트, 그림자 등의 시각적 스타일을 적용하여 렌더링하는 과정을 페인팅이라고 합니다.
7. #### 합성 및 레이어 (Compositing and Layers) 
   - 복잡한 요소들은 개별 레이어로 분리되어 관리됩니다. 이러한 레이어들은 합성 단계에서 하나의 이미지로 결합됩니다. 이를 통해 브라우저는 레이어들의 순서와 중첩을 관리하고, 사용자에게 최종적으로 완성된 이미지를 표시합니다.


### 용어 공부
> 출처 : [https://github.com/Esoolgnah](https://github.com/Esoolgnah/Frontend-Interview-Questions/blob/main/Notes/important-5/browser-rendering.md)

#### 렌더링엔진
  - 브라우저 마다 다르지만, 브라우저는 렌더링을 수행하는 렌더링 엔진을 가지고 있습니다. 크롬은 블링크(Blink), 사파리는 웹킷(Webkit) 그리고 파이어폭스는 게코(Gecko)라는 렌더링 엔진을 사용합니다.

#### CRP
  - CRP (Critical Rendering Path, 중요 렌더링 경로)는 브라우저가 HTML, CSS, Javascipt를 화면에 픽셀로 변화하는 일련의 단계를 말합니다. CRP는 Document Object Model (DOM), CSS Object Model (CSSOM), 렌더 트리 그리고 레이아웃을 포함합니다.

#### 파싱
  - 파싱은 하나의 프로그램을 런타임 환경(예를 들면, 브라우저 내 자바스크립트 엔진)이 실제로 실행할 수 있는 내부 포맷으로 분석하고 변환하는 것을 의미합니다. 즉, 파싱은 문서의 내용을 토큰(token)으로 분석하고, 문법적 의미와 구조를 반영한 파스 트리(parse tree)를 생성하는 과정입니다.

#### DOM
  - DOM(Document Object Model)이란? 웹 페이지를 이루는 태그들을 자바스크립트가 이용할 수 있게끔 브라우저가 트리구조로 만든 객체 모델을 의미합니다. 영어 뜻풀이 그대로 하자면 문서 객체 모델을 의미합니다. 문서 객체란 html, head, body와 같은 태그들을 javascript가 이용할 수 있는 (메모리에 보관할 수 있는) 객체를 의미합니다. DOM은 HTML과 스크립팅 언어(JavaScript)를 서로 이어주는 역할을 합니다.

#### CSSOM
  - CSSOM(CSS Object Model)이란? CSS 내용을 파싱하여 자료를 구조화 한 것을 CSSOM이라고 합니다. 즉 DOM처럼 CSS의 내용을 해석하고 노드를 만들어 트리 구조로 만든 것을 CSSOM이라 합니다.

#### 렌더트리
  - 렌더트리(Render Tree)란? 렌더 트리는 CSSOM과 DOM 트리의 결합으로 만들어집니다. 렌더 트리는 웹 페이지에 나타낼 각 요소들의 위치(Layout, 레이아웃)을 계산하는데 사용되고 픽셀을 화면에 렌더링하는 페인트(Paint) 즉 화면에 요소들을 표현하는 프로세스를 위해 존재합니다.


#### Layout
  - Layout(Reflow)이란? 뷰포트 내에서 노드의 정확한 위치와 크기를 계산합니다. 이것이 바로 'Layout' 단계이며 경우에 따라 'Reflow' 라고도 합니다.

#### Paint
  - Paint란? 노드와 해당 노드의 계산된 스타일 및 기하학적 형태에 대해 파악했으므로, 렌더링 트리의 각 노드를 화면의 실제 픽셀로 변환하는 마지막 단계에 이러한 정보를 전달합니다. 이 단계를 흔히 '페인팅' 또는 '래스터화'라고 합니다.
