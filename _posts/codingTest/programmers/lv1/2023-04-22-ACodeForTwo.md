---
title: "[ JS 코딩테스트 ] 둘만의 암호"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명

- 두 문자열 s와 skip, 그리고 자연수 index가 주어질 때, 다음 규칙에 따라 문자열을 만들려 합니다. 암호의 규칙은 다음과 같습니다.
- 문자열 s의 각 알파벳을 index만큼 뒤의 알파벳으로 바꿔줍니다.
- index만큼의 뒤의 알파벳이 z를 넘어갈 경우 다시 a로 돌아갑니다.
- skip에 있는 알파벳은 제외하고 건너뜁니다.
- 예를 들어 s = "aukks", skip = "wbqd", index = 5일 때, a에서 5만큼 뒤에 있는 알파벳은 f지만 [b, c, d, e, f]에서 'b'와 'd'는 skip에 포함되므로 세지 않습니다. 따라서 'b', 'd'를 제외하고 'a'에서 5만큼 뒤에 있는 알파벳은 [c, e, f, g, h] 순서에 의해 'h'가 됩니다. 나머지 "ukks" 또한 위 규칙대로 바꾸면 "appy"가 되며 결과는 "happy"가 됩니다.
- 두 문자열 s와 skip, 그리고 자연수 index가 매개변수로 주어질 때 위 규칙대로 s를 변환한 결과를 return하도록 solution 함수를 완성해주세요.

### 제한사항
- 5 ≤ s의 길이 ≤ 50
- 1 ≤ skip의 길이 ≤ 10
- s와 skip은 알파벳 소문자로만 이루어져 있습니다.
- skip에 포함되는 알파벳은 s에 포함되지 않습니다.
- 1 ≤ index ≤ 20

### 입출력 예
|s|	skip |	index|	result|
|:---:|:---:|:---:|:---:|
|"aukks"|	"wbqd"|	5|	"happy"|

### 입출력 예 설명
#### 입출력 예 #1
- 본문 내용과 일치합니다.


### 풀이

```javascript
const solution = (s, skip, index) => {
    // 소문자 알파벳 마지막인 z를 숫자로 변환
    const last = 'z'.charCodeAt();
    // 스킵할 알파벳 문자열을 배열로 변환하면서 숫자로 변환
    skip = skip.split('').map((v) => v.charCodeAt());
    // 문자열 s를 skip처럼 배열로 변환하면서 숫자로 변환
    return s.split('')
        .map((v) => v.charCodeAt())
        .map((v) => {
          // 알파벳을 이동할때 카운트할 변수 newIndex선언
          let newIndex = index;
          for (let a = 0; a < newIndex; a++) {
            // 시작부터 알파벳이 z일수 있으니 v가 z일경우 v에 26을 빼줍니다.
            if (v === last) {
              v -= 26;
            }
            // 알파벳 뒤로 한칸 이동, ex) a > b
            v++;
            // 만약 이동한 알파벳이 skip에 포함되어 있을 경우 newIndex에 1을 더해 한 번 더 반복
            skip.includes(v) && newIndex++;
          }
          // 반복문이 끝나면 문자로 변환해서 리턴
          return String.fromCharCode(v);
        })
        // 배열을 문자열로 변환
        .join('');
  };
```
