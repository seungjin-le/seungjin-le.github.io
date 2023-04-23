---
title: "[ JS 코딩테스트 ] 달리기 경주"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
얀에서는 매년 달리기 경주가 열립니다. 해설진들은 선수들이 자기 바로 앞의 선수를 추월할 때 추월한 선수의 이름을 부릅니다. 예를 들어 1등부터 3등까지 "mumu", "soe", "poe" 선수들이 순서대로 달리고 있을 때, 해설진이 "soe"선수를 불렀다면 2등인 "soe" 선수가 1등인 "mumu" 선수를 추월했다는 것입니다. 즉 "soe" 선수가 1등, "mumu" 선수가 2등으로 바뀝니다.

선수들의 이름이 1등부터 현재 등수 순서대로 담긴 문자열 배열 players와 해설진이 부른 이름을 담은 문자열 배열 callings가 매개변수로 주어질 때, 경주가 끝났을 때 선수들의 이름을 1등부터 등수 순서대로 배열에 담아 return 하는 solution 함수를 완성해주세요.

### 제한사항
- 5 ≤ players의 길이 ≤ 50,000
  - players[i]는 i번째 선수의 이름을 의미합니다.
  - players의 원소들은 알파벳 소문자로만 이루어져 있습니다.
  - players에는 중복된 값이 들어가 있지 않습니다.
  - 3 ≤ players[i]의 길이 ≤ 10
- 2 ≤ callings의 길이 ≤ 1,000,000
  - callings는 players의 원소들로만 이루어져 있습니다.
  - 경주 진행중 1등인 선수의 이름은 불리지 않습니다.

### 입출력 예

|players|	callings|	result|
|:--:|:--:|:--:|
|["mumu", "soe", "poe", "kai", "mine"]	|["kai", "kai", "mine", "mine"]|	["mumu", "kai", "mine", "soe", "poe"]|

### 입출력 예 설명
#### 입출력 예 #1

- 4등인 "kai" 선수가 2번 추월하여 2등이 되고 앞서 3등, 2등인 "poe", "soe" 선수는 4등, 3등이 됩니다. 5등인 "mine" 선수가 2번 추월하여 4등, 3등인 "poe", "soe" 선수가 5등, 4등이 되고 경주가 끝납니다. 1등부터 배열에 담으면 ["mumu", "kai", "mine", "soe", "poe"]이 됩니다.

### 풀이
```jsx
const solution = (players, callings) => {
    // players의 이름에 등수를 저장할 map선언
    // ex ) { name => 1}
    const playMap = new Map();

    // players의 등수에 이름을 저장할 map선언
    // ex ) { 1 => name}
    const scoreMap = new Map();

    // 배열 players를 순회하면서 2개에 map에
    // 등수와 이름을 저장
    players.map((v, i) => {
      playMap.set(v, i);
      scoreMap.set(i, v);
    });

    // 배열 callings를 순회
    callings.map((v) => {
      // 해설자가 부른 선수( v )가 현제 1등인경우 다음으로 넘어감
      if (playMap.get(v) === 0) return;

      // 해설자가 부른 선수의 이름, 선수의 현제 등수, 한 명을 제치고 상승한 등수를 변수에 저장
      const up = [v, playMap.get(v), playMap.get(v) - 1];

      // 해설자가 부른 선수의 한등수 앞선 선수의 이름, 선수의 현제 등수, 제쳐지고 떨어진 등수를 변수에 저장
      const down = [scoreMap.get(up[2]), up[2], up[1]];

      // 선수 이름에 등수가 저장된 map에서
      // 해설자가 부른 선수의 등수를 새로 초기화
      playMap.set(v, up[2]);
      // 제쳐진 선수의 등수를 새로 초기화
      playMap.set(down[0], up[1]);

      // 등수에 선수 이름이 저장된 map에서
      // 해설자가 부른 선수의 등수를 새로 초기화
      scoreMap.set(down[1], up[0]);
      // 제쳐진 선수의 등수를 새로 초기화
      scoreMap.set(up[1], down[0]);
    });

    return [...scoreMap].map((v) => v[1]);
  };
```
