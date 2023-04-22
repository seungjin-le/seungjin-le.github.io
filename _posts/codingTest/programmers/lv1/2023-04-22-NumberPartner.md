---
title: "[ JS 코딩테스트 ] 숫자 짝꿍"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
두 정수 X, Y의 임의의 자리에서 공통으로 나타나는 정수 k(0 ≤ k ≤ 9)들을 이용하여 만들 수 있는 가장 큰 정수를 두 수의 짝꿍이라 합니다(단, 공통으로 나타나는 정수 중 서로 짝지을 수 있는 숫자만 사용합니다).   
X, Y의 짝꿍이 존재하지 않으면, 짝꿍은 -1입니다. X, Y의 짝꿍이 0으로만 구성되어 있다면, 짝꿍은 0입니다.

예를 들어, X = 3403이고 Y = 13203이라면, X와 Y의 짝꿍은 X와 Y에서 공통으로 나타나는 3, 0, 3으로 만들 수 있는 가장 큰 정수인 330입니다. 다른 예시로 X = 5525이고 Y = 1255이면   
X와 Y의 짝꿍은 X와 Y에서 공통으로 나타나는 2, 5, 5로 만들 수 있는 가장 큰 정수인 552입니다(X에는 5가 3개, Y에는 5가 2개 나타나므로 남는 5 한 개는 짝 지을 수 없습니다.)
두 정수 X, Y가 주어졌을 때, X, Y의 짝꿍을 return하는 solution 함수를 완성해주세요.

### 제한사항
- 3 ≤ X, Y의 길이(자릿수) ≤ 3,000,000입니다.
- X, Y는 0으로 시작하지 않습니다.
- X, Y의 짝꿍은 상당히 큰 정수일 수 있으므로, 문자열로 반환합니다.

### 입출력 예

|X|	Y|	result|
|:---:|:---:|:---:|
|"100"	|"2345"|	"-1"|
|"100"	|"203045"	|"0"|
|"100"	|"123450"	|"10"|
|"12321"|	"42531"	|"321"|
|"5525"	|"1255"	|"552"|

### 입출력 예 설명
#### 입출력 예 #1

- X, Y의 짝꿍은 존재하지 않습니다. 따라서 "-1"을 return합니다.
  입출력 예 #2

- X, Y의 공통된 숫자는 0으로만 구성되어 있기 때문에, 두 수의 짝꿍은 정수 0입니다. 따라서 "0"을 return합니다.
#### 입출력 예 #3

- X, Y의 짝꿍은 10이므로, "10"을 return합니다.
#### 입출력 예 #4

- X, Y의 짝꿍은 321입니다. 따라서 "321"을 return합니다.
#### 입출력 예 #5

- 지문에 설명된 예시와 같습니다.

### 풀이

```jsx
import React from 'react';

// 숫자 짝꿍

const NumberPartner = () => {
  function solution(X, Y) {
    let answer = '';
    // 문자열 X와 Y 중 길이가 짧은 문자열의 중복을 제거 후 배열로 치환.
    const arr = [...new Set(X.length < Y.length ? X.split('') : Y.split(''))]
      // 중복을 제거한 문자 배열을 값이 큰순으로 정렬
      .sort((a, b) => b - a);
    // 문자열 X와 Y의 길이를 배열에 담아줍니다.
    let lens = [X.length, Y.length];

    arr.map((v) => {
      // 중복을 제거한 값을 정규식을 이용해서 문자열 X와 Y에서
      // 제거해 준 다음 처음에 선언한 X와 Y의 길이와 제거 후 문자열의 길이를
      // 마이너스 한 후에 둘 중 하나라도 0이 있다면 서로 X와 Y는 서로
      // 중복되는 값이 없다는 뜻이며 둘 다 0이 아니라면
      // 마이너스한 값들 중 값이 더 작은 값을 찾아내
      // arr의 현제 요소를 작은 값만큼 repeat 함수를 이용해
      // 문자를 복사해 answer에 넣어줍니다.
      const reg = new RegExp(v, 'g');
      let aLen = lens[0] - X.replace(reg, '').length;
      let bLen = lens[1] - Y.replace(reg, '').length;
      if (lens[0] !== 0 && lens[1] !== 0)
        answer += v.repeat(aLen > bLen ? bLen : aLen);
    });
    // 처음 arr을 정렬할 때 큰 순으로 했는데
    // 문자열 answer의 첫 번째 값이 0이라면 0보다 큰 값이 없다는 뜻이므로
    // 문자열 0을 리턴
    if (answer[0] === '0') return '0';
    // arr.map을 통해 비교를 반복하면서 한 번도 조건문을 통과하지 못했다면
    // answer은 빈 문자열이므로 -1을 리턴 아니라면 answer을 리턴
    return !answer ? '-1' : answer;
  }
  return <div></div>;
};

export default NumberPartner;

```
