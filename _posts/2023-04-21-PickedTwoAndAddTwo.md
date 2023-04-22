---
title: "[ JS 코딩테스트 ] 두 개 뽑아서 더하기"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
정수 배열 numbers가 주어집니다. numbers에서 서로 다른 인덱스에 있는 두 개의 수를 뽑아 더해서 만들 수 있는 모든 수를 배열에 오름차순으로 담아 return 하도록 solution 함수를 완성해주세요.

### 제한사항
- numbers의 길이는 2 이상 100 이하입니다.
  - numbers의 모든 수는 0 이상 100 이하입니다.

### 입출력 예

|numbers|result|
|:---:|:---:|
|[2,1,3,4,1]|[2,3,4,5,6,7]|
|[5,0,2,7]|[2,5,7,9,12]|

### 입출력 예 설명
#### 입출력 예 #1
- 2 = 1 + 1 입니다. (1이 numbers에 두 개 있습니다.)
- 3 = 2 + 1 입니다.
- 4 = 1 + 3 입니다.
- 5 = 1 + 4 = 2 + 3 입니다.
- 6 = 2 + 4 입니다.
- 7 = 3 + 4 입니다.

따라서 [2,3,4,5,6,7] 을 return 해야 합니다.

#### 입출력 예 #2
- 2 = 0 + 2 입니다.
- 5 = 5 + 0 입니다.
- 7 = 0 + 7 = 5 + 2 입니다.
- 9 = 2 + 7 입니다.
- 12 = 5 + 7 입니다.

따라서 [2,5,7,9,12] 를 return 해야 합니다.

### 풀이
```javascript
function solution(numbers) {
  var answer = [];
  for(let a = 0; a < numbers.length; a++){
    for(let i =a; i < numbers.length; i++){
      answer.push(i+1 < numbers.length ? numbers[a]+numbers[i+1] : '');
    }
  }
  let x = Array.from(new Set(answer));
  x.sort((f,s) => (f-s));
  return x.filter((element, i) => element !== '');
}
```

### 문제 풀이
>이중 for문을 이용해서 풀었습니다 첫 번째 for문은 배열의 길이만큼 반복하도록 하였고 두번째 for문도 첫번째 for문과 조건이 비슷하지만 변수 i 에는 변수 a가담겨 2번째 반복문이 한 번씩 수행을 완료할 때마다 i값은 1씩 증가한 다음 반복문이 실행됩니다 그렇게 해서 numbers변수 안에 있는 값들을 하나씩 더할 수 있습니다 만약 i+1이 number의 길이보다 같거나 크다면 빈 배열을 answer의 넣어줍니다
>
>반복문이 모두 끝나면 변수 x를 만들어 answer의 중복되는 숫자들을 모두 제거해주고 sort함수를 이용해 오름차순으로 정렬해줍니다
>
>마지막으로 리턴할 때 filter함수를 이용해 빈 배열을 제거해줍니다
