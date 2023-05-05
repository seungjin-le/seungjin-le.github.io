---
title: "[ React ] Props란?"
author: <author_id>
categories: [ React, Props]
tags: [ React, Props]
math: true
toc: true
mermaid: true
image: /images/backgrounds/react.png
---


## props란?

> React의 props는 컴포넌트 간에 데이터를 전달하는 데 사용되는 객체입니다.  
> 부모 컴포넌트에서 자식 컴포넌트로 정보를 전달하기 위해 사용되며, 이를 통해 컴포넌트 간의 상호작용 및 재사용성을 증가시킵니다.  
> props는 컴포넌트에 전달되는 속성과 값의 집합으로, 자식 컴포넌트에서 읽기 전용으로 사용되며
> React의 데이터 흐름 원칙 중 하나인 "단방향 데이터 흐름" 또는 "top-down 데이터 흐름"을 따르고 있습니다.  
> 이것은 데이터가 항상 상위 컴포넌트에서 하위 컴포넌트로 전달되며, 자식 컴포넌트가 직접 부모 컴포넌트의 상태를 수정할 수 없다는 것을 의미합니다.
> 

#### 부모 컴포넌트
```javascript
const Parents = (props) => {
  return <Children name="BiBiBig" />;
}

```
#### 자식 컴포넌트
```javascript
function Children(props) {
  console.log(props.name) // BiBiBig
  return <h1>Hello, {props.name}!</h1>;
}
```

> props를 사용할때는 변수의 값을 변경하지 말고 사용하면 됩니다.

#### [출처 : React 공식 사이트](https://ko.reactjs.org/docs/components-and-props.html#props-are-read-only)
