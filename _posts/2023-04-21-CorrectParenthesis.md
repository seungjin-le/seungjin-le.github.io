---
title: "[ JS 코딩테스트 LV2 ] 올바른 괄호"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

## 문제 설명
괄호가 바르게 짝지어졌다는 것은 '(' 문자로 열렸으면 반드시 짝지어서 ')' 문자로 닫혀야 한다는 뜻입니다. 예를 들어

+ "()()" 또는 "(())()" 는 올바른 괄호입니다.
+ ")()(" 또는 "(()(" 는 올바르지 않은 괄호입니다.

'(' 또는 ')' 로만 이루어진 문자열 s가 주어졌을 때, 문자열 s가 올바른 괄호이면 true를 return 하고, 올바르지 않은 괄호이면 false를 return 하는 solution 함수를 완성해 주세요.

### 제한사항
+ 문자열 s의 길이 : 100,000 이하의 자연수
+ 문자열 s는 '(' 또는 ')' 로만 이루어져 있습니다.

### 입출력 예


|    s     | 	answer |
|:--------:|:-------:|
| "()()"	  |  true   |
| "(())()" |  	true  |
| ")()("	  |  false  |
| "(()("	  |  false  |

### 입출력 예 설명
#### 입출력 예 #1,2,3,4
- 문제의 예시와 같습니다.

### 풀이
```javascript
const solution = (s) => {
    // 괄호 개수 체크 [ '(', ')' ]
    let check = [0,0]
    // 문자열 s의 길이만큼 만복
    for(let a = 0; a < s.length; a++){
      // s의 a 번째 문자가 ' ( '일 경우 check[0] + 1
      if(s[a] === '('){
        check[0]++
      // s의 a 번째 문자가 ' ) '일 경우 check[0] 과 check[1]의 값이 같으면
      // false를 리턴하기 위해 check[1] = -9
      }else if(s[a] === ')' && check[0] === check[1]){
        check[1] = -9
      // else if의 조건에 맞지 않다면 check[1] + 1
      }else{
        check[1]++
      }
    }
    // check[0] 과 check[1]의 값이 같다며 true를 리턴 아니라면 false를 리턴
    return check[0] === check[1];
  }
```
