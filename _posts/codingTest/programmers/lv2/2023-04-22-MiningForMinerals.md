---
title: "[ JS 코딩테스트 LV2 ] 광물 캐기"
author: <author_id>
categories: [CodingTest,Programmers,"LV 2"]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---


### 문제 설명
마인은 곡괭이로 광산에서 광석을 캐려고 합니다. 마인은 다이아몬드 곡괭이, 철 곡괭이, 돌 곡괭이를 각각 0개에서 5개까지 가지고 있으며, 곡괭이로 광물을 캘 때는 피로도가 소모됩니다. 각 곡괭이로 광물을 캘 때의 피로도는 아래 표와 같습니다.

![](https://velog.velcdn.com/images/dltmdwls15/post/fae87c86-b9df-4172-9433-1370e4c657b6/image.png)


예를 들어, 철 곡괭이는 다이아몬드를 캘 때 피로도 5가 소모되며, 철과 돌을 캘때는 피로도가 1씩 소모됩니다. 각 곡괭이는 종류에 상관없이 광물 5개를 캔 후에는 더 이상 사용할 수 없습니다.

마인은 다음과 같은 규칙을 지키면서 최소한의 피로도로 광물을 캐려고 합니다.

- 사용할 수 있는 곡괭이중 아무거나 하나를 선택해 광물을 캡니다.
- 한 번 사용하기 시작한 곡괭이는 사용할 수 없을 때까지 사용합니다.
- 광물은 주어진 순서대로만 캘 수 있습니다.
- 광산에 있는 모든 광물을 캐거나, 더 사용할 곡괭이가 없을 때까지 광물을 캡니다.
  즉, 곡괭이를 하나 선택해서 광물 5개를 연속으로 캐고, 다음 곡괭이를 선택해서 광물 5개를 연속으로 캐는 과정을 반복하며, 더 사용할 곡괭이가 없거나 광산에 있는 모든 광물을 캘 때까지 과정을 반복하면 됩니다.

마인이 갖고 있는 곡괭이의 개수를 나타내는 정수 배열 `picks`와 광물들의 순서를 나타내는 문자열 배열 `minerals`가 매개변수로 주어질 때, 마인이 작업을 끝내기까지 필요한 최소한의 피로도를 return 하는 solution 함수를 완성해주세요.

### 제한사항
- picks는 [dia, iron, stone]과 같은 구조로 이루어져 있습니다.
  - 0 ≤ dia, iron, stone ≤ 5
  - dia는 다이아몬드 곡괭이의 수를 의미합니다.
  - iron은 철 곡괭이의 수를 의미합니다.
  - stone은 돌 곡괭이의 수를 의미합니다.
  - 곡괭이는 최소 1개 이상 가지고 있습니다.
- 5 ≤ minerals의 길이 ≤ 50
  - minerals는 다음 3개의 문자열로 이루어져 있으며 각각의 의미는 다음과 같습니다.
  - diamond : 다이아몬드
  - iron : 철
  - stone : 돌

### 입출력 예

|picks|	minerals|	result|
|:--:|:--:|:--:|
|[1, 3, 2]|	["diamond", "diamond", "diamond", "iron", "iron", "diamond", "iron", "stone"]	|12|
|[0, 1, 1]|	["diamond", "diamond", "diamond", "diamond", "diamond", "iron", "iron", "iron", "iron", "iron", "diamond"]	|50|

### 입출력 예 설명
#### 입출력 예 #1

- 다이아몬드 곡괭이로 앞에 다섯 광물을 캐고 철 곡괭이로 남은 다이아몬드, 철, 돌을 1개씩 캐면 12(1 + 1 + 1 + 1+ 1 + 5 + 1 + 1)의 피로도로 캘 수 있으며 이때가 최소값입니다.

#### 입출력 예 #2

- 철 곡괭이로 다이아몬드 5개를 캐고 돌 곡괭이고 철 5개를 캐면 50의 피로도로 캘 수 있으며, 이때가 최소값입니다.

### 풀이
```javascript
const solution = (picks, minerals) => {
    var answer = 0;
    let len = Math.ceil(minerals.length / 5);
    let maxLen = picks.reduce((a, b) => a + b);
    let arr = [];
    if (maxLen === 0) return 0;
    minerals = minerals.splice(0, maxLen * 5);

    for (let a = 0; a < len; a++) {
      let obj = { d: 0, i: 0, s: 0 };
      // minerals의 0번째부터 5번째까지 자른후 배열을 순회하면서
      // 자른 배열의 해당 요소를 obj에 카운터
      minerals.splice(0, 5).map((v) => obj[v[0]]++);
      // 각 곡괭이로 5개의 광석을 캤을때 사용되는 피로도를 arr에 추가
      // 순서대로 [ dia, iron, stone ]
      arr.push([
        obj.d + obj.i + obj.s,
        obj.d * 5 + obj.i + obj.s,
        obj.d * 25 + obj.i * 5 + obj.s,
      ]);
    }
    // stone 곡괭이로 캤을 때 가장 큰값이 앞에 오도록 내림차순으로 정렬 후
    // 배열을 순회 하면서 stone 곡괭이로 캤을 때 가장 큰값은 다이아가 많다는 뜻이므로
    // 다이아 곡괭이(picks[0])를 먼저 사용
    // 다이아 곡괭이가 없다면 철 곡괭이(picks[1])를 사용
    // 철 곡괭이도 없다면 돌 곡괭이 사용
    arr
      .sort((a, b) => b[2] - a[2])
      .map((v) => {
        if (picks[0] > 0) return picks[0]--, (answer += v[0]);
        if (picks[1] > 0) return picks[1]--, (answer += v[1]);
        if (picks[2] > 0) return picks[2]--, (answer += v[2]);
      });

    return answer;
  };
```
