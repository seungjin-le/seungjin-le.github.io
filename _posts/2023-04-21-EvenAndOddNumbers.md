---
title: 짝수와홀수
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
정수 num이 짝수일 경우 "Even"을 반환하고 홀수인 경우 "Odd"를 반환하는 함수, solution을 완성해주세요.

### 제한 조건

- num은 int 범위의 정수입니다.
- 0은 짝수입니다.


### 입출력 예

|num| 	return |
|:--:|:-------:|
|3	|  "Odd"  |
|4|	"Even"|



solution 함수는 num이라는 숫자형 매개변수를 받아 홀수와 짝수를 구별하는 함수이고 홀수면 'Odd' 짝수면 'Even'문자를 리턴해야 합니다

간단한 문제지만 가장 적은 양의 메모리를 사용하고 가독성이 높은 코드를 작성하고 싶었고 제한조건에 '0은 짝수입니다'라는 문구가 눈에 들어와 코드를 작성했습니다

```javascript
function solution(num) {
  return num % 2 ? 'Odd' : 'Even';
}
```

0을 불리언 값으로 치면 false 1은 true입니다 0은 짝수로 친다면 2로 나눠지면 false 나머지 값이 1이면 true를 반환하면 된다고 생각했고

물음표 연산자(조건부 연산자)를 통해 특정 조건에 맞으면 Odd와 Even을 answer에 넣어줍니다 그리고 answer을 리턴해주면 됩니다


---

