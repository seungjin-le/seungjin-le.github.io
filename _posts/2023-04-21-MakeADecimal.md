---
title: "[ JS 코딩테스트 ] 소수 만들기"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
주어진 숫자 중 3개의 수를 더했을 때 소수가 되는 경우의 개수를 구하려고 합니다. 

숫자들이 들어있는 배열 nums가 매개변수로 주어질 때, nums에 있는 숫자들 중 서로 다른 3개를 골라 더했을 때 소수가 되는 경우의 개수를 return 하도록 solution 함수를 완성해주세요.

### 제한사항
- nums에 들어있는 숫자의 개수는 3개 이상 50개 이하입니다.
- nums의 각 원소는 1 이상 1,000 이하의 자연수이며, 중복된 숫자가 들어있지 않습니다.

### 입출력 예

|nums|result|
|:--:|:--:|
|[1,2,3,4]|1|
|[1,2,7,6,4]|4|

### 입출력 예 설명
#### 입출력 예 #1
- [1,2,4]를 이용해서 7을 만들 수 있습니다.

#### 입출력 예 #2
- [1,2,4]를 이용해서 7을 만들 수 있습니다.
- [1,4,6]을 이용해서 11을 만들 수 있습니다.
- [2,4,7]을 이용해서 13을 만들 수 있습니다.
- [4,6,7]을 이용해서 17을 만들 수 있습니다.

### 풀이
```javascript
const solution = (nums) => {
    let answer = 0;
    // for 문을 3qjs 중첩해서 사용하기 때문에 코드 간결하게 쓰기위한 nums 길이를 담은 변수
    let len = nums.length;
    // 반복문 안에서 소수인지 확인할 함수
    const decimal = (n) => {
      // Math.sprt : 매개변수로 주어진 값의 제곱근을 구하는 내장함수
      for (let i = 2; i <= Math.sqrt(n); i++) {
        // 소수는 1과 자신 외에는 나누어지는 숫자가 없어야 하므로 나눠지면 false를 리턴
        if (n % i === 0) {
          return false;
        }
      }
      return true;
    }
    // 숫자를 선택할 3개중 1번째 자리 앞에 2개가 숫자를 선택할수 있도록 nums 길이의 -2까지만 반복
    for(let a = 0; a < len-2; a++){
      // 숫자를 선택할 3개중 2번째 자리 앞에 1개가 숫자를 선택할수 있도록 nums 길이의 -1까지만 반복
      for(let b = a+1; b < len-1; b++){
        // 숫자를 선택할 3개중 3번째 마지막이니 nums 길이의 끝까지 반복
        for(let c = b+1; c < len; c++){
          // decimal 에 nums[a]+nums[b]+nums[c]를 매개변수로 넣어줍니다.
          if(decimal(nums[a]+nums[b]+nums[c])){
            // true 결과 리턴시 answer++
            answer++
          }
        }
      }
    }
    return answer;
  }
```

### 후기
> 몇 시간 동안 고민하다가 다른 분이 푸신 걸 참고해서 겨우 풀었네요 나중에 다시 복습해 봐야 할 문제
