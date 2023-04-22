---
title: "[ JS 코딩테스트 ] 부족한 금액 계산하기"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
새로 생긴 놀이기구는 인기가 매우 많아 줄이 끊이질 않습니다. 이 놀이기구의 원래 이용료는 price원 인데, 놀이기구를 N 번 째 이용한다면 원래 이용료의 N배를 받기로 하였습니다. 즉, 처음 이용료가 100이었다면 2번째에는 200, 3번째에는 300으로 요금이 인상됩니다.
놀이기구를 count번 타게 되면 현재 자신이 가지고 있는 금액에서 얼마가 모자라는지를 return 하도록 solution 함수를 완성하세요.
단, 금액이 부족하지 않으면 0을 return 하세요.

### 제한사항
- 놀이기구의 이용료 price : 1 ≤ price ≤ 2,500, price는 자연수
- 처음 가지고 있던 금액 money : 1 ≤ money ≤ 1,000,000,000, money는 자연수
- 놀이기구의 이용 횟수 count : 1 ≤ count ≤ 2,500, count는 자연수

### 입출력 예

|price|	money|	count|	result|
|:---:|:---:|:---:|:---:|
|3|	20	|4|	10|

### 입출력 예 설명
#### 입출력 예 #1
- 이용금액이 3인 놀이기구를 4번 타고 싶은 고객이 현재 가진 금액이 20이라면, 총 필요한 놀이기구의 이용 금액은 30 (= 3+6+9+12) 이 되어 10만큼 부족하므로 10을 return 합니다.

### 풀이
```javascript
function solution(price, money, count) {
  	// price 놀이기구 이용요금
	// money 처음에 가지고 있던 돈
  	// count 놀이기구 이용 횟수
    let answer = 0;
  	// 반복문을 count(놀이기구 이용 횟수) 만큼 반복
    for (let a = 0; a <= count; a++) {
      // 이용요금 * 이용횟수 를 answer에 계속 더해줍니다.
      answer += price * a;
    }
    // 만약 총 이용요금이 소지금액보다 높으면 부족한 금액을 리턴해줍니다.
  	// 소지금액이 이용요금보다 많으면 0을 리턴
    return answer > money ? money - answer : 0;
}
```
