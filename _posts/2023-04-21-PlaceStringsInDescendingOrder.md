---
title: "[ JS 코딩테스트 ] 문자열 내림차순으로 배치하기"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
+ 문자열 s에 나타나는 문자를 큰것부터 작은 순으로 정렬해 새로운 문자열을 리턴하는 함수, solution을 완성해주세요.
  s는 영문 대소문자로만 구성되어 있으며, 대문자는 소문자보다 작은 것으로 간주합니다.

### 제한 사항
+	str은 길이 1 이상인 문자열입니다.

|입출력|예|
|:--:|:--:|
|s|return|
|"Zbcdefg"|"gfedcbZ"|



### 풀이
```javascript
const solution = (s) => {
    // 문자열을 배열로 변환
    let answer = s.split('')
    // 대문자를 담을 배열 a
    let a = [];
    // 소문자를 담을 배열 b
    let b = [];
    // 문자열 배열 answer 을 순회 하면서
    // v 가 v.toUpperCase() (대문자로 변환하는 함수) 랑 같으면 a 아니면 b 에 push
    answer.map((v) => v === v.toUpperCase() ? a.push(v) : b.push(v))
    // 문자배열을 올림차순으로 정렬후 reverse 로 반전
    b = b.sort().reverse();
    a = a.sort().reverse();
    // 소문자배열 b 뒤에 대문자배열 a를 스프레드 문법으로 push
	// 문제 설명중 대문자는 소문자보다 작으니 소문자 뒤에 대문자 push
    b.push(...a);
    // 문자 배열을 문자열로 join
    b = b.join('')
    return b;
  }
```

### [깃허브 링크](https://github.com/seungjin-le/JsCodingTest)
