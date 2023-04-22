---
title: "[ JS 코딩테스트 ] 직사각형 별찍기"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
이 문제에는 표준 입력으로 두 개의 정수 n과 m이 주어집니다.
별(*) 문자를 이용해 가로의 길이가 n, 세로의 길이가 m인 직사각형 형태를 출력해보세요.

### 제한 조건
- n과 m은 각각 1000 이하인 자연수입니다.

#### 예시입력
> 5 3


#### 출력

```
*****
*****
*****
```

### 풀이
```javascript
process.stdin.setEncoding('utf8');
process.stdin.on('data', data => {
    const n = data.split(" ");
    const a = Number(n[0]), b = Number(n[1]);
    let q = '';
    for(let v = 0; v < b; v++){
        for(let z = 0; z <= a; z++){
            q.length < a ? q+='*' : false     
        }
    }
});
```

### 문제 풀이
> q라는 빈 문자열을 만들고 1차 반복문을 만들어 별표 사각형의 세로(b) 길이만큼 반복하고 그 안에 가로(a) 길이만큼 " * " 문자를 q에 넣어주는 반복문을 만들어 줍니다
