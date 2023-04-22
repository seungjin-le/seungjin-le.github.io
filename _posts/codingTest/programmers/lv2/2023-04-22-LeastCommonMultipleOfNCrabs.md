---
title: "[ JS 코딩테스트 LV2 ] N개의 최소공배수"
author: <author_id>
categories: [CodingTest,Programmers,"LV 2"]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
두 수의 최소공배수(Least Common Multiple)란 입력된 두 수의 배수 중 공통이 되는 가장 작은 숫자를 의미합니다. 예를 들어 2와 7의 최소공배수는 14가 됩니다. 정의를 확장해서, n개의 수의 최소공배수는 n 개의 수들의 배수 중 공통이 되는 가장 작은 숫자가 됩니다. n개의 숫자를 담은 배열 arr이 입력되었을 때 이 수들의 최소공배수를 반환하는 함수, solution을 완성해 주세요.

### 제한 사항
+ arr은 길이 1이상, 15이하인 배열입니다.
+ arr의 원소는 100 이하인 자연수입니다.

### 입출력 예

|arr| 	result |
|:--:|:-------:|
|[2,6,8,14]	|   168   |
|[1,2,3]	|    6    |

### 풀이

```javascript
const solution = (arr) => {
    let answer = 0;
    // 배열안에 있는 모든 수들의 공배수를 구해야 하니 가장 큰수를 찾아 변수에 넣습니다.
    let max = Math.max(...arr);
    // 계속해서 가장 큰수를 더해줘야하니 가장 크수부터 시작
    let count = max;

    // 반복문 안에 있는 조건문을 통과시 answer++, answer은 arr의 길이와 같으면 종료
    while (answer !== arr.length) {
      arr.map((v) => {
        // count를 arr안에 있는 값들로 나눴을때 0일때마다 answer++
        if (count % v === 0) {
          answer++;
        }
        return v;
      });
      // answer은 arr의 길이와 같으면 현제 공배수를 담은 count를 리턴
      if (answer === arr.length) {
        return count;
      }
      // count에 가장 큰수를 계속 더해줍니다.
      count += max;
      // 반복문이 끝날때마다 answer을 초기화
      answer = 0;
    }
  };
```
