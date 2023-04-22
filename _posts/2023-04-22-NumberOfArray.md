---
title: "[ JS 코딩테스트 ] 자연수 뒤집어 배열 만들기"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
자연수 n을 뒤집어 각 자리 숫자를 원소로 가지는 배열 형태로 리턴해주세요. 예를들어 `n`이 `12345`이면 `[5,4,3,2,1]`을 리턴합니다.

### 제한 조건
n은 10,000,000,000이하인 자연수입니다.

|입출력|예|
|:---:|:---:|
|n|return|
|12345|[5,4,3,2,1]|

### 풀이
```javascript
const solution = (n) => {
    let answer = [...String(n)];
    answer = answer.reverse().map(v => Number(v))
    return answer;
}
```
### 후기
>요즘 코딩테스트를 풀면서 느낀거지만 처음부터 완벽한 코드보다는 일단 풀고 최적화를 하는게 정신건강에 좋다고 생각합니다.
