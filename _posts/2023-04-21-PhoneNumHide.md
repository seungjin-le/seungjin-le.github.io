---
title: "[ JS 코딩테스트 ] 핸드폰 번호 가리기"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
프로그래머스 모바일은 개인정보 보호를 위해 고지서를 보낼 때 고객들의 전화번호의 일부를 가립니다.
전화번호가 문자열 phone_number로 주어졌을 때, 전화번호의 뒷 4자리를 제외한 나머지 숫자를 전부 *으로 가린 문자열을 리턴하는 함수, solution을 완성해주세요.

### 제한 조건
- s는 길이 4 이상, 20 이하인 문자열입니다.

### 입출력 예

|phone_number |	return |
|:---:|:---:|
|"01033334444" | "*******4444" |
|"027778888" |	"*****8888" |


### 풀이
```javascript
function solution(phone_number) {
    let answer = Array.from(phone_number);
    let x = answer.map((i, j) => j < answer.length-4 ? "*" : i);
    return x.join('');
}
```

### 문제 풀이
> `phone_number` 매개변수를 배열로 변환시키고 배열의 내장함수를 이용해 총길이와 비교해서 총길이의 -4까지 문자를 *로 변환시키고 변환시킨 값을 리턴할 때 join('')으로 문자열로 변환시켰습니다

---

