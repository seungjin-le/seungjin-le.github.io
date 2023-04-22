---
title: "[ JS 코딩테스트 LV2 ] 소수 찾기"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

### 제한사항
+ numbers는 길이 1 이상 7 이하인 문자열입니다.
+ numbers는 0~9까지 숫자만으로 이루어져 있습니다.
+ "013"은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.

### 입출력 예

|numbers	| return  |
|:--:|:-------:|
|"17"	|    3    |
|"011"	|    2    |

### 입출력 예 설명

#### 예제 #1
+ [1, 7]으로는 소수 [7, 17, 71]를 만들 수 있습니다.

#### 예제 #2
+ [0, 1, 1]으로는 소수 [11, 101]를 만들 수 있습니다.

**11과 011은 같은 숫자로 취급합니다.**

### 풀이

```javascript
const solution = (numbers) => {
    
    let answer = 0;
    const numArr = numbers.split('');
    const permutationAll = [];
    for (let r = 1; r <= numbers.length; r++) {
      const permutationR = Permutation(numArr, r).map((arr) =>
        parseInt(arr.join(''))
      );
      for (let i = 0; i < permutationR.length; i++)
        permutationAll.push(permutationR[i]);
    }
    const permutationSet = [...new Set(permutationAll)];
    for (const number of permutationSet) {
      if (isPrime(number)) answer += 1;
    }
    return answer;
  };

  function Permutation(arr, r) {
    const result = [];
    if (r === 1) return arr.map((num) => [num]);
    arr.forEach((fixed, index, org) => {
      const rest = [...org.slice(0, index), ...org.slice(index + 1)];
      const permutation = Permutation(rest, r - 1);
      const attached = permutation.map((numbers) => [fixed, ...numbers]);
      result.push(...attached);
    });
    return result;
  }
  function isPrime(num) {
    for (let i = 2; i <= Math.sqrt(num); i++) {
      if (num % i === 0) return false;
    }
    return num >= 2;
  }
```

