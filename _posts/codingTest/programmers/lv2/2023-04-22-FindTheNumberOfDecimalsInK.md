---
title: "[ JS 코딩테스트 LV2 ] k진수에서 소수 개수 구하기"
author: <author_id>
categories: [CodingTest,Programmers,"LV 2"]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
양의 정수 n이 주어집니다. 이 숫자를 k진수로 바꿨을 때, 변환된 수 안에 아래 조건에 맞는 소수(Prime number)가 몇 개인지 알아보려 합니다.

+ `0P0`처럼 소수 양쪽에 `0`이 있는 경우
+ `P0`처럼 소수 오른쪽에만 `0`이 있고 왼쪽에는 아무것도 없는 경우
+ `0P`처럼 소수 왼쪽에만 `0`이 있고 오른쪽에는 아무것도 없는 경우
+ `P`처럼 소수 양쪽에 아무것도 없는 경우
+ 단, `P`는 각 자릿수에 `0`을 포함하지 않는 소수입니다.

예를 들어, `101`은 `P`가 될 수 없습니다. 예를 들어, `437674`을 3진수로 바꾸면 `211020101011`입니다. 여기서 찾을 수 있는 조건에 맞는 소수는 왼쪽부터 순서대로 `211, 2, 11`이 있으며, 총 3개입니다. (211, 2, 11을 k진법으로 보았을 때가 아닌, 10진법으로 보았을 때 소수여야 한다는 점에 주의합니다.) `211`은 `P0` 형태에서 찾을 수 있으며, `2`는 `0P0`에서, `11`은 `0P`에서 찾을 수 있습니다.

정수 n과 k가 매개변수로 주어집니다. n을 k진수로 바꿨을 때, 변환된 수 안에서 찾을 수 있는 위 조건에 맞는 소수의 개수를 return 하도록 solution 함수를 완성해 주세요.

### 제한사항
+ 1 ≤ n ≤ 1,000,000
+ 3 ≤ k ≤ 10

### 입출력 예

|n|	k| 	result  |
|:--:|:--:|:--------:|
|437674|	3|    	3    |
|110011|	10|    	2    |

### 입출력 예 설명
#### 입출력 예 #1

+ 문제 예시와 같습니다.

#### 입출력 예 #2

+ 110011을 10진수로 바꾸면 110011입니다. 여기서 찾을 수 있는 조건에 맞는 소수는 11, 11 2개입니다. 이와 같이, 중복되는 소수를 발견하더라도 모두 따로 세어야 합니다.

### 풀이
```javascript
const solution = (n, k) => {
    return n
      // k 진수로 변환
      .toString(k)
      // 0을 기준으로 잘라 문자 배열로 치환
      .split('0')
      // split로 문자열을 자를때 '00'일경우 빈배열 생성되고
      // 문제에서 1은 소수가 아니므로 filter함수의 조건문을
      // v !== '1'( v는 1이 아니다 ), v(v가 빈 문자열일경우 filter함수가 걸러줍니다.)
      // 위 2개 조건을 통과하면 재귀함수 primeNumberCheck에 문자열(v)를 parseInt 함수를
      // 이용해 숫자로 변환후 매개 변수로 넣어줍니다.
      .filter((v) => v !== '1' && v && primeNumberCheck(parseInt(v))).length;;
  };

  function primeNumberCheck(n) {
    // Math.sqrt(n)를 이용해 n의 제곱근을 구하고 n까지 반복
    // 원리는 "에라토스테네스의 체" 참고
    const sqrt = Math.sqrt(n);
    for (let a = 3; a <= sqrt; a += 2) {
      // n을 a로 나눴을때 0 이 아니라면 소수가 아니니 false리턴
      if (n % a === 0) return false;
    }
    // 반복문을 통과하면 return리턴
    return true;
  }
```
### 후기
> 문제를 푸는 시간보다 "에라토스테네스의 체"를 이해하는게 더 시간이 걸렸네요.
