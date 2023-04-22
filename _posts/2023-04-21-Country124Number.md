---
title: "[ JS 코딩테스트 LV2 ] 124 나라의 숫자"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
124 나라가 있습니다. 124 나라에서는 10진법이 아닌 다음과 같은 자신들만의 규칙으로 수를 표현합니다.
+ 124 나라에는 자연수만 존재합니다.
+ 124 나라에는 모든 수를 표현할 때 1, 2, 4만 사용합니다.
+ 예를 들어서 124 나라에서 사용하는 숫자는 다음과 같이 변환됩니다.

|10진법|124나라|10진법|124나라|
|:---:|:---:|:---:|:---:|
|1|1|6|14|
|2|2|7|21|
|3|4|8|22|
|4|11|9|24|
|5|12|10|41|
자연수 n이 매개변수로 주어질 때, n을 124 나라에서 사용하는 숫자로 바꾼 값을 return 하도록 solution 함수를 완성해 주세요.

### 제한사항

+ n은 500,000,000이하의 자연수 입니다.

### 입출력 예

|n|result|
|:---:|:---:|
|1|1|
|2|2|
|3|4|
|4|11|

### 풀이
```javascript
function solution (n) {
  var answer = '';
  // 124 나라 숫자 배열
  let nation124 = [4,1,2];
  // 10진법을 3진법으로 변경해야하니 3으로 나눈 값을 넣어줄 변수
  let value = 0;
  while(n > 0) {
    // n을 3으로 나눴을때 나머지를 담음
    value = n%3;
    // 소수점을 내림해줄 내장함수
    n = parseInt(n/3);
    //만약에 value가 0이라면 n--로 반복문 중단
    value === 0 ?  n-- : false
    // answer문자열에 nation124배열의value인덱스 위치의 값 + answer을더합니다
    answer = nation124[value] + answer;
  }
  return answer;
}
```

### 문제 풀이
> nation124라는 124나라의 숫자를 담을 배열을 만든 다음 나눈 값을 저장할 변수 value도 만듭니다 그리고 반복문을 만들어 n이 0이 될 때까지 반복하도록 합니다 value에 n%3 을해서 n을 3으로 나눈 나머지 값을 넣어줍니다 그리고 n에는 내장 함수 ParseInt를 이용해 n을 3으로 나눈 몫을 넣어줍니다 그리고 코드를 간결하게 쓰고 싶어서 삼항 연산자를 써서 value가 0이라면 --n로 반복문을 중단해줍니다 그리고 마지막으로 answer 문자열에 nation124 숫자 배열의 value인덱스 위치의 값을 찾아 이전에 있던 answer과 함 쳐서 넣어줍니다 
