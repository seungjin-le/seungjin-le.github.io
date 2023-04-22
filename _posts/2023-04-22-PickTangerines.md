---
title: "[ JS 코딩테스트 LV2 ] 귤 고르기"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
경화는 과수원에서 귤을 수확했습니다. 경화는 수확한 귤 중 'k'개를 골라 상자 하나에 담아 판매하려고 합니다. 그런데 수확한 귤의 크기가 일정하지 않아 보기에 좋지 않다고 생각한 경화는 귤을 크기별로 분류했을 때 서로 다른 종류의 수를 최소화하고 싶습니다.

예를 들어, 경화가 수확한 귤 8개의 크기가 [1, 3, 2, 5, 4, 5, 2, 3] 이라고 합시다. 경화가 귤 6개를 판매하고 싶다면, 크기가 1, 4인 귤을 제외한 여섯 개의 귤을 상자에 담으면, 귤의 크기의 종류가 2, 3, 5로 총 3가지가 되며 이때가 서로 다른 종류가 최소일 때입니다.

경화가 한 상자에 담으려는 귤의 개수 k와 귤의 크기를 담은 배열 tangerine이 매개변수로 주어집니다. 경화가 귤 k개를 고를 때 크기가 서로 다른 종류의 수의 최솟값을 return 하도록 solution 함수를 작성해주세요.

### 제한사항
- 1 ≤ k ≤ tangerine의 길이 ≤ 100,000
- 1 ≤ tangerine의 원소 ≤ 10,000,000

### 입출력 예

|k|	tangerine|	result|
|:--:|:--:|:--:|
|6	|[1, 3, 2, 5, 4, 5, 2, 3]	|3|
|4	|[1, 3, 2, 5, 4, 5, 2, 3]	|2|
|2|	[1, 1, 1, 1, 2, 2, 2, 3]	|1|

### 입출력 예 설명
#### 입출력 예 #1
- 본문에서 설명한 예시입니다.

#### 입출력 예 #2
- 경화는 크기가 2인 귤 2개와 3인 귤 2개 또는 2인 귤 2개와 5인 귤 2개 또는 3인 귤 2개와 5인 귤 2개로 귤을 판매할 수 있습니다. 이때의 크기 종류는 2가지로 이 값이 최소가 됩니다.

#### 입출력 예 #3
- 경화는 크기가 1인 귤 2개를 판매하거나 2인 귤 2개를 판매할 수 있습니다. 이때의 크기 종류는 1가지로, 이 값이 최소가 됩니다.

### 풀이
>- 여러 방법으로 코드를 최적화 할려고 했지만 돌고돌아 결국 `tangerine`을 한번 순회하는걸로 끝났네요.
>  ```javascript
>   // 귤의 크기가 담긴 배열을 문자열로 치환
>    tangerine = tangerine.join;
>    // 중복을 제거한 귤의 크기를 담은 배열만큼 반복문 실행
>    for (let a = 0; a < set.length; a++) {
>      // 정규식 선언
>      const reg = new RegExp(set[a],'g');
>      // 중복을 제거하기전 귤의 크기가 담긴 문자열의 길이를 미리 선언
>      const len = tangerine.length;
>      // 문자열에서 해당 크기를 전부 제거한 후 제거하기 전과 길이를 비교 후
>      // 삭제한 문자의 길이만큼 arr에 추가
>      arr.push(len - tangerine.replace(reg,''));
>    }
>  ```
>
>처음엔 이 방법으로 했다가 메모리 사용량이 정답보다 10배가량 높게 나와서 `filter`함수도 사용해 봤지만
>`map`함수로 전부 확인하는 게 가장 메모리 효율이 좋았습니다.

```jsx
const solution = (k, tangerine) => {
    // 상자에 담을 최소한의 귤 크기 갯수를 를 담을 변수
    let answer = 0;
    // 귤의 크기마다 가지고 있는 개수를 담을 배열
    let arr = [];
    // 귤의 크기가 담긴 배열에서 중복을 제거
    const set = [...new Set(tangerine)];
    // 귤의 크기마다 가지고 있는 갯수를 를 구분할 객체
    const obj = {};
    // 만약 상자에 담을 굴의 개수(k) 가 귤의 총개수(tangerine) 와 같다면 중복을 제거한 귤의 크기 배열의 길이를 리턴
    if (k === tangerine.length) return set.length;

    // 귤의 크기가 담긴 배열 tangerine 순회
    tangerine.map((v) => {
      // obj에 v라는 크기가 있다면 obj[귤의 크기] + 1, 없다면 obj[귤의 크기] = 1
      obj.hasOwnProperty(v) ? obj[v]++ : (obj[v] = 1);
    });
    // 귤의 크기 종류를 담은 배열 set 순회
    // arr에 크기마다 가지고 있는 개수를 추가
    set.map((v) => arr.push(obj[v]));
    // 귤의 크기마다 가지고있는 개수를 내림차순으로 정렬
    arr = arr.sort((a, b) => b - a);

    // arr의 길이만큼 반복문 실행
    for (let a = 0, b = 0; a < arr.length; a++) {
      // 변수 b에 귤에 갯수를 더해줍니다.
      b += arr[a];
      // (a + 1) = 상자에 담을 귤의 종류
      answer = a + 1;
      // 만약 b가 상자에 담을 귤에 개수(k)와 같거나 그보다 크다면 answer 리턴
      if (b >= k) return answer;
    }
    return answer;
  };

```
