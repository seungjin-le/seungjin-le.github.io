---
title: "[ JS 코딩테스트 ] 명예의 전당 (1)"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
"명예의 전당"이라는 TV 프로그램에서는 매일 1명의 가수가 노래를 부르고, 시청자들의 문자 투표수로 가수에게 점수를 부여합니다. 매일 출연한 가수의 점수가 지금까지 출연 가수들의 점수 중 상위 k번째 이내이면 해당 가수의 점수를 명예의 전당이라는 목록에 올려 기념합니다. 즉 프로그램 시작 이후 초기에 k일까지는 모든 출연 가수의 점수가 명예의 전당에 오르게 됩니다. k일 다음부터는 출연 가수의 점수가 기존의 명예의 전당 목록의 k번째 순위의 가수 점수보다 더 높으면, 출연 가수의 점수가 명예의 전당에 오르게 되고 기존의 k번째 순위의 점수는 명예의 전당에서 내려오게 됩니다.

이 프로그램에서는 매일 "명예의 전당"의 최하위 점수를 발표합니다. 예를 들어, k = 3이고, 7일 동안 진행된 가수의 점수가 [10, 100, 20, 150, 1, 100, 200]이라면, 명예의 전당에서 발표된 점수는 아래의 그림과 같이 [10, 10, 10, 20, 20, 100, 100]입니다.

![](https://velog.velcdn.com/images/dltmdwls15/post/be53b054-a7de-415f-8125-c62bc0efa6be/image.png)


명예의 전당 목록의 점수의 개수 `k`, 1일부터 마지막 날까지 출연한 가수들의 점수인 `score`가 주어졌을 때, 매일 발표된 명예의 전당의 최하위 점수를 return하는 solution 함수를 완성해주세요.

### 제한사항
- 3 ≤ k ≤ 100
- 7 ≤ score의 길이 ≤ 1,000
- 0 ≤ score[i] ≤ 2,000

### 입출력 예

|k|	score|	result|
|:--:|:--:|:--:|
|3	|[10, 100, 20, 150, 1, 100, 200]	|[10, 10, 10, 20, 20, 100, 100]|
|4|	[0, 300, 40, 300, 20, 70, 150, 50, 500, 1000]	|[0, 0, 0, 0, 20, 40, 70, 70, 150, 300]|


### 입출력 예 설명
#### 입출력 예 #1

- 문제의 예시와 같습니다.
#### 입출력 예 #2

- 아래와 같이, [0, 0, 0, 0, 20, 40, 70, 70, 150, 300]을 return합니다.

![](https://velog.velcdn.com/images/dltmdwls15/post/8d7786e9-b583-4440-a870-a7febe67bb17/image.png)

### 풀이

```jsx
const solution = (k, score) => {
    // k의 크기만큼 변수를 담을 배열
    let answer = [];
    // 점수 배열인 score 순회
    return score.map((v) => {
      // answer에 v를 추가
      answer.push(v);
      // answer에 변수를 추가한 후에 k보다 크다면
      if (answer.length > k) {
        // answer을 내림차순으로 정렬 후
        answer = answer.sort((a, b) => b - a);
        // 마지마 요소 삭제
        answer.pop();
      }
      // answer 안에 있는 요소들 중 가장 작은 요소를 리턴
      // 위 조건문을 통해 answer의 길이는 k와 같은 길이를
      // 유지하면서 새로 들어온 값이 기존에 있던 값보다 작으면
      // sort(), pop()을 통해서 알아서 삭제가 되고
      // 삭제 후에 배열 안에 요소들 중 가장 작은 값을 리턴하면 됩니다.
      return Math.min(...answer);
    });
  };
```
