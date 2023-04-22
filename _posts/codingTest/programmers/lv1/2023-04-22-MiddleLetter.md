---
title: "[ JS 코딩테스트 ] 가운데 글자 가져오기"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
단어 s의 가운데 글자를 반환하는 함수, solution을 만들어 보세요. 단어의 길이가 짝수라면 가운데 두 글자를 반환하면 됩니다.

### 재한 사항
- s는 길이가 1 이상, 100 이하인 스트링입니다.

### 입출력 예

|s|return|
|:---:|:---:|
|"abcde"|"c"|
|"qwer"|"we"|

### 풀이
```javascript
function solution(s) {
    return (s.length %2) === 0 ? s[s.length/2-1]+s[s.length/2] : s[s.length/2-0.5];
}
```

### 문제 풀이
> 문자열 s의 길이를 2로 나눴을 때 0이면 문자열의 길이는 짝수이니 2개를 반환해야 하므로 문자열의 길이 값을 반으로 나누고 나눈 값을 1을 빼고  반으로 나눈값을 문자열에서 찾아 반환합니다 문자열의 길이가 홀수이면 반으로 나누고 0.5를 뺀 값을 문자열에서 찾아 반환합니다



---

