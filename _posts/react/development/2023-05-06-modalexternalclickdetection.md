---
title: "[ React ] 모달 컴포넌트 외부 클릭 감지"
author: <author_id>
categories: [ React,  Development]
tags: [ React, JavaScript ]
math: true
toc: true
mermaid: true
image: /images/backgrounds/react.png
---

이전에 외주를 하는 곳에서 UI 라이브러리를 사용중에 라이브러리의 모달을 닫는 함수 Props를  
 
사용 시 useState의 변화가 생기지 않아서 모달을 닫는 Props를 닫고 새로 기능을 구현했습니다.

![1](/images/postImages/react/modalexternalclickdetection.png)

모달 `BackGround`에 따로 `ClassName`이나 `ID`값을 부여하거나 변경할 수가 없어서 여러 방법을 찾다가 이 방법을 사용했습니다.  
 
이 방법은 모달을 클릭해도 동작하는 방법이라 그다지 효율이 좋다고 볼 수 없습니다.

### Modal.js
```javascript
// 모달을 띄웠을 때 이벤트 활성화
const click = ({target: {className}}) => {
  	// 클릭한 컴포넌트의 classname에 아래 문자가 전부 포함되어있을경우
  	// 모달을 닫는 함수 실행
    if (
      className?.includes('modal') &&
      className?.includes('fade') &&
      className?.includes('d-block') &&
      className?.includes('show')
    ) {
      return onClose()
    }
  }


useEffect(() => {
  // 모달을 띄웠을 때 이벤트 생성
  document.addEventListener('mousedown', click)
  return () => {
    // 모달이 사라졌을 때 이벤트 삭제
    document.removeEventListener('mousedown', click)
  }
})
```
