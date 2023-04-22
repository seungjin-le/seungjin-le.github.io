---
title: "[ JS 코딩테스트 LV2 ] 연속 부분 수열 합의 개수"
author: <author_id>
categories: [CodingTest,Programmers,"LV 2"]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---


### 문제 설명
철호는 수열을 가지고 놀기 좋아합니다. 어느 날 철호는 어떤 자연수로 이루어진 원형 수열의 연속하는 부분 수열의 합으로 만들 수 있는 수가 모두 몇 가지인지 알아보고 싶어졌습니다. 원형 수열이란 일반적인 수열에서 처음과 끝이 연결된 형태의 수열을 말합니다. 예를 들어 수열 [7, 9, 1, 1, 4] 로 원형 수열을 만들면 다음과 같습니다.
![](https://velog.velcdn.com/images/dltmdwls15/post/3dc6d4c0-59eb-43eb-972c-42a3e67582d2/image.png)

원형 수열은 처음과 끝이 연결되어 끊기는 부분이 없기 때문에 연속하는 부분 수열도 일반적인 수열보다 많아집니다.
원형 수열의 모든 원소 elements가 순서대로 주어질 때, 원형 수열의 연속 부분 수열 합으로 만들 수 있는 수의 개수를 return 하도록 solution 함수를 완성해주세요.

### 제한사항
- 3 ≤ elements의 길이 ≤ 1,000
- 1 ≤ elements의 원소 ≤ 1,000

### 입출력 예

|elements|	result|
|:--:|:--:|
|[7,9,1,1,4]	|18|

### 입출력 예 설명
#### 입출력 예 #1
- 길이가 1인 연속 부분 수열로부터 [1, 4, 7, 9] 네 가지의 합이 나올 수 있습니다.
- 길이가 2인 연속 부분 수열로부터 [2, 5, 10, 11, 16] 다섯 가지의 합이 나올 수 있습니다.
- 길이가 3인 연속 부분 수열로부터 [6, 11, 12, 17, 20] 다섯 가지의 합이 나올 수 있습니다.
- 길이가 4인 연속 부분 수열로부터 [13, 15, 18, 21] 네 가지의 합이 나올 수 있습니다.
- 길이가 5인 연속 부분 수열로부터 [22] 한 가지의 합이 나올 수 있습니다.
- 이들 중 중복되는 값을 제외하면 다음과 같은 18가지의 수들을 얻습니다.
  `[1, 2, 4, 5, 6, 7, 9, 10, 11, 12, 13, 15, 16, 17, 18, 20, 21, 22]`

### 풀이

```javascript
const solution = (elements) => {
    // 수열을 추가할 배열
    const seqArr = [];
    // 반복문 실행 중 i + index가 elements의 길이를 넘어서면 elements의
    // 0번 인덱스부터 시작해야 하기 때문에 elements를 2개 붙여줍니다
    // ( i + index)의 최대 길이는 elements의 길이 * 2
    const arr = [...elements, ...elements];
    // 이중 반복문 실행
    elements.map((v, i) => {
      elements.map((valye, index) => {
        // 배열 arr의 index부터 index + i + 1까지 배열을 자른 다음
        // reduce 함수를 통해 자른 배열 안에 값들을 전부 더해서 seqArr에 추가해 줍니다
        seqArr.push(arr.slice(index, index + i).reduce((acc, v) => acc + v, 0));
      });
    });
    // Set 함수로 seqArr의 중복을 제거 후 객체의 길이를 리턴
    return new Set(seqArr).size;
  };
```
- 입출력 설명에서 중복을 제거하고 정렬했다고 안 적혀 있어서 왜 저런 값이 나올까? 문제를 이해하는데
  시간이 걸렸던 문제였습니다
  -  반복문 진행 순서도

 ``` javascript
 elements = [7,9,1,1,4], arr = [ 7, 9, 1, 1, 4, 7, 9, 1, 1, 4]
 
 seqArr = [7, 9, 1, 1, 4] => 중복 제거후 정렬하면 [1, 4, 7, 9]
 index = 1, i = 0, arr.elice(index, index + i + 1) = [ 7 ], .reduce() = 7;
 index = 1, i = 1, arr.elice(index, index + i + 1) = [ 9 ], .reduce() = 9;
 index = 1, i = 2, arr.elice(index, index + i + 1) = [ 1 ], .reduce() = 1;
 index = 1, i = 3, arr.elice(index, index + i + 1) = [ 1 ], .reduce() = 1;
 index = 1, i = 4, arr.elice(index, index + i + 1) = [ 4 ], .reduce() = 4;

 seqArr = [16, 10, 2, 5, 11] => 중복 제거후 정렬하면 [2, 5, 10, 11, 16]
 index = 2, i = 0, arr.elice(index, index + i + 1) = [ 7, 9 ], .reduce() = 16;
 index = 2, i = 1, arr.elice(index, index + i + 1) = [ 9, 1 ], .reduce() = 10;
 index = 2, i = 2, arr.elice(index, index + i + 1) = [ 1, 1 ], .reduce() = 2;
 index = 2, i = 3, arr.elice(index, index + i + 1) = [ 1, 4 ], .reduce() = 5;
 index = 2, i = 4, arr.elice(index, index + i + 1) = [ 4, 7 ], .reduce() = 11;

 seqArr = [17, 11,  6, 12, 20] => 중복 제거후 정렬하면 [2, 5, 10, 11, 16]
 index = 3, i = 0, arr.elice(index, index + i + 1) = [ 7, 9, 1 ], .reduce() = 17;
 index = 3, i = 1, arr.elice(index, index + i + 1) = [ 9, 1, 1 ], .reduce() = 11;
 index = 3, i = 2, arr.elice(index, index + i + 1) = [ 1, 1, 4 ], .reduce() = 6;
 index = 3, i = 3, arr.elice(index, index + i + 1) = [ 1, 4, 7 ], .reduce() = 12;
 index = 3, i = 4, arr.elice(index, index + i + 1) = [ 4, 7, 9 ], .reduce() = 20;

 seqArr = [18, 15, 13, 21, 21] => 중복 제거후 정렬하면 [2, 5, 10, 11, 16]
 index = 4, i = 0, arr.elice(index, index + i + 1) = [ 7, 9, 1, 1 ], .reduce() = 18;
 index = 4, i = 1, arr.elice(index, index + i + 1) = [ 9, 1, 1, 4 ], .reduce() = 15;
 index = 4, i = 2, arr.elice(index, index + i + 1) = [ 1, 1, 4, 7 ], .reduce() = 13;
 index = 4, i = 3, arr.elice(index, index + i + 1) = [ 1, 4, 7, 9 ], .reduce() = 21;
 index = 4, i = 4, arr.elice(index, index + i + 1) = [ 4, 7, 9, 1 ], .reduce() = 21;
