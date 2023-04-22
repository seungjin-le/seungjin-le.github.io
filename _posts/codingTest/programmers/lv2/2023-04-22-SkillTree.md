---
title: "[ JS 코딩테스트 LV2 ] 스킬트리"
author: <author_id>
categories: [CodingTest,Programmers,"LV 2"]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---


### 문제 설명
선행 스킬이란 어떤 스킬을 배우기 전에 먼저 배워야 하는 스킬을 뜻합니다.

예를 들어 선행 스킬 순서가 `스파크 → 라이트닝 볼트 → 썬더`일때, 썬더를 배우려면 먼저 라이트닝 볼트를 배워야 하고, 라이트닝 볼트를 배우려면 먼저 스파크를 배워야 합니다.

위 순서에 없는 다른 스킬(힐링 등)은 순서에 상관없이 배울 수 있습니다. 따라서 `스파크 → 힐링 → 라이트닝 볼트 → 썬더`와 같은 스킬트리는 가능하지만, `썬더 → 스파크`나 `라이트닝 볼트 → 스파크 → 힐링 → 썬더`와 같은 스킬트리는 불가능합니다.

선행 스킬 순서 `skill`과 유저들이 만든 스킬트리1를 담은 배열 `skill_trees`가 매개변수로 주어질 때, 가능한 스킬트리 개수를 return 하는 solution 함수를 작성해주세요.

### 제한 조건
- 스킬은 알파벳 대문자로 표기하며, 모든 문자열은 알파벳 대문자로만 이루어져 있습니다.
- 스킬 순서와 스킬트리는 문자열로 표기합니다.
  - 예를 들어, `C → B → D` 라면 `"CBD"`로 표기합니다
- 선행 스킬 순서 skill의 길이는 1 이상 26 이하이며, 스킬은 중복해 주어지지 않습니다.
- skill_trees는 길이 1 이상 20 이하인 배열입니다.
- skill_trees의 원소는 스킬을 나타내는 문자열입니다.
- skill_trees의 원소는 길이가 2 이상 26 이하인 문자열이며, 스킬이 중복해 주어지지 않습니다.

### 입출력 예

|skill|	skill_trees|	return|
|:--:|:--:|:--:|
|"CBD"|	["BACDE", "CBADF", "AECB", "BDA"]	|2|

### 입출력 예 설명
- "BACDE": B 스킬을 배우기 전에 C 스킬을 먼저 배워야 합니다. 불가능한 스킬트립니다.
- "CBADF": 가능한 스킬트리입니다.
- "AECB": 가능한 스킬트리입니다.
- "BDA": B 스킬을 배우기 전에 C 스킬을 먼저 배워야 합니다. 불가능한 스킬트리입니다.

### 풀이


```javascript
// ex) skill = "CBD", skill_trees = ["BACDE", "CBADF", "AECB", "BDA"]
 const solution = (skill, skill_trees) => {
    // skill의 순서를 담을 객체
    let obj = {};
    // 문자열 skill을 배열로 치환하고 알파벳은 obj에 key 값으로 넣고
    // 알파벳의 인덱스 값을 value 값으로 obj에 추가
    // ex) { C : 0, B : 1, D : 2 }
    skill.split('').map((v, i) => {
      obj[v] = i;
    });
    // 스킬트리 배열 순회
    return (
      skill_trees
        .map((v) => {
          // 스킬트리의 요소인 문자열을 obj의 index값으로 치환하기 위한 배열
          let skill = [];
          // 스킬트리의 요소인 문자열을 배열로 치환후 순회
          v.split('').map((v) => {
            // obj 안에 v라는 key 값이 있다면 obj 안에 있는 인덱스 값을 skill에 추가
            // ex) "BACDE" => skill = [ 1, 0, 2 ]
            // ex) B = 1, C = 0, D = 2
            obj.hasOwnProperty(v) && skill.push(obj[v]);
          });

          // 배열 skill 리턴
          return skill;
        })
        // filter함수로 스킬트리 이차원 배열 다시 순회
        .filter((v) => {
          // 스킬 순서가 담긴 요소인 배열을 반복문을 통해서
          // 배열 안에 값이 오름차순인지 조건문을 통해 검사하고
          // 오름차순이 아니라면 해당 스킬은 배울 수 없으니 false 리턴
          // ex) v = [ 1, 0, 2 ], a = 0, v[a] = 1
          for (let a = 0; a < v.length; a++) {
            if (v[a] !== a) return false;
          }
          // filter 함수로 배울 수 있는 스킬만 걸러냈으니 해당 배열의 길이를 리턴
          return true;
        }).length
    );
  };
```
