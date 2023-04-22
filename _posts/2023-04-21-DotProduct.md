---
title: "[ JS 코딩테스트 ] 내적"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
길이가 같은 두 1차원 정수 배열 a, b가 매개변수로 주어집니다. a와 b의 내적을 return 하도록 solution 함수를 완성해주세요.

이때, a와 b의 내적은 a[0]*b[0] + a[1]*b[1] + ... + a[n-1]*b[n-1] 입니다. (n은 a, b의 길이)

### 제한사항
+ a, b의 길이는 1 이상 1,000 이하입니다.
+ a, b의 모든 수는 -1,000 이상 1,000 이하입니다.

### 입출력 예

|a|b|result|
|:---:|:---:|:---:|
|[1,2,3,4]|[-3,-1,0,2]|3|
|[-1,0,1]|[1,0,-1]|-2|

### 입출력 예 설명
#### 입출력 예 #1
- a와 b의 내적은 1*(-3) + 2*(-1) + 3*0 + 4*2 = 3 입니다.

#### 입출력 예 #2
- a와 b의 내적은 (-1)*1 + 0*0 + 1*(-1) = -2 입니다.

### 풀이
```javascript
function solution(a, b) { // a와 b의 배열의 길이는 같습니다
    // a.map함수를 이용해서 a[i] 와 b[i]의 값을 곱합니다
    let q = a.map((v,i) => v * b[i]);
    // reduce함수를 이용해서 배열을 순차적으로 돌며 값들을 더합니다
    var answer = q.reduce((i,v) => i+v);
    return answer;
}
```

### 문제 풀이
>문제 설명중  a와 b는 배열의 길이가 서로 같다고 해서 a.map 함수를 이용해 a[i]와 b[i]를 서로 곱한 값을 변수 q에 넣고 reduce함수를 이용해 배열 q를 순회하면서 배열 안에 있는 값들을 서로 더했습니다
