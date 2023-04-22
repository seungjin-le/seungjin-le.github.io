---
title: "[ JS 코딩테스트 ] x만큼 간격이 있는 n개의 숫자"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
함수 solution은 정수 x와 자연수 n을 입력받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴해야 합니다. 다음 제한 조건을 보고, 조건을 만족하는 함수, solution을 완성해주세요.

### 제한 조건
- x는 -10000000 이상, 10000000 이하인 정수입니다.
- n은 1000 이하인 자연수입니다.
### 입출력 예

|x|n|answer|
|:---:|:---:|:---:|
|2|5|[2,4,6,8,10]|
|4|3|[4,8,12]|
|-4|2|[-4, -8]|

### 풀이
```javascript
function solution(x, n) {
    var answer = [];
    for(i = 1; i <= n; i++){
      answer[i - 1] = x * i;
    }
    return answer;
}
```

### 문제 풀이
> for문 을 사용해서 i는 0부터 시작해서 배열의 길이를 바는 매개변수인 `n`과 같아질 때까지 반복해 answer `[ i - 1 ]` 번째에  `x * i` 값을 넣습니다

