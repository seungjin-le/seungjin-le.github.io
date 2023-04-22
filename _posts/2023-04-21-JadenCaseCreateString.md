---
title: "[ JS 코딩테스트 LV2] JadenCase 문자열 만들기"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 단, 첫 문자가 알파벳이 아닐 때에는 이어지는 알파벳은 소문자로 쓰면 됩니다. (첫 번째 입출력 예 참고)
문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

### 제한 조건
+ s는 길이 1 이상 200 이하인 문자열입니다.
+ s는 알파벳과 숫자, 공백문자(" ")로 이루어져 있습니다.
+ 숫자는 단어의 첫 문자로만 나옵니다.
+ 숫자로만 이루어진 단어는 없습니다.
+ 공백문자가 연속해서 나올 수 있습니다.

### 입출력 예

|s	|return|
|:--:|:--:|
|"3people unFollowed me"|	"3people Unfollowed Me"|
|"for the last week"|	"For The Last Week"|

### 풀이
```javascript
const solution = (s) => {
    // 공백을 기준으로 문자열을 나눠 배열로 만든후
    // map 함수로 배열을 순회하면서 문자열의 첫번재 문자를 대문자로 변경하고
    // 문자열의 첫번째 문자를 slice 로 자른후 toLowerCase 함수로 소문자로 변경후
    // 변경한 문자열들을 합쳐서 반환
    s = s.split(" ").map((v) => 
      v.charAt(0).toUpperCase() + v.slice(1).toLowerCase());
    // 문자 배열을 원소를 기준으로 공백을 넣어 문자열로 형 변환 후 반환
    return s.join(" ");
  };
```
