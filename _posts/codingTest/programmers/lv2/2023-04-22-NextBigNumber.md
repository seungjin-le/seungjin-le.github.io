---
title: "[ JS 코딩테스트 LV2 ] 다음 큰 숫자"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
자연수 n이 주어졌을 때, n의 다음 큰 숫자는 다음과 같이 정의 합니다.

+ 조건 1. n의 다음 큰 숫자는 n보다 큰 자연수 입니다.
+ 조건 2. n의 다음 큰 숫자와 n은 2진수로 변환했을 때 1의 갯수가 같습니다.
+ 조건 3. n의 다음 큰 숫자는 조건 1, 2를 만족하는 수 중 가장 작은 수 입니다.

예를 들어서 78(1001110)의 다음 큰 숫자는 83(1010011)입니다.

자연수 n이 매개변수로 주어질 때, n의 다음 큰 숫자를 return 하는 solution 함수를 완성해주세요.

### 제한 사항
+ n은 1,000,000 이하의 자연수 입니다.

### 입출력 예

|n| 	result  |
|:--:|:--------:|
|78	|    83    |
|15	|    23    |

### 입출력 예 설명
#### 입출력 예#1
+ 문제 예시와 같습니다.

#### 입출력 예#2
+ 15(1111)의 다음 큰 숫자는 23(10111)입니다.

### 풀이
```javascript
 const solution = (n) => {
    // n보다 커야하니 시작은 n + 1
    let answer = n+1;
    // n과 answer을 2진수로 변환하고 0을 제거했을때 같을때까지 answer++ 반복
    while(answer.toString(2).replace(/0/g,'') !== n.toString(2).replace(/0/g,'')){
      answer++
    }
    // answer 리턴
    return answer;
  }
```
