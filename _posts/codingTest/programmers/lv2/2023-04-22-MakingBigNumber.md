---
title: "[ JS 코딩테스트 LV2 ] 큰 수 만들기"
author: <author_id>
categories: [CodingTest,Programmers,"LV 2"]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.

예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다.

문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

### 제한 조건
- number는 2자리 이상, 1,000,000자리 이하인 숫자입니다.
- k는 1 이상 number의 자릿수 미만인 자연수입니다.

### 입출력 예

|number|	k|	return|
|:--:|:--:|:--:|
|"1924"|	2|	"94"|
|"1231234"	|3|	"3234"|
|"4177252841"|	4	|"775841"|

### 풀이( 테스트 케이스 9, 10 런타임 에러 )
```javascript
 // 테스트 케이스 9, 10 런타임 에러
    const solution = (number, k) => {
        let answer = [];
        let arr = [...number]
    
        while(arr.length && k > 0){
            answer.push(arr.shift())
            while(answer[answer.length-1] < arr[0] && k > 0) {
                answer.pop();
                k = k-1;
            }
        }
        answer.push(...arr);
        
        return k !== 0 ? answer.slice(0, -k).join('') : answer.join('')
    }

    

```
### 정답
```javascript
const test = (number,k) => {
      let stack = [];
      let arr = number.split('').reverse();
      while(arr.length && k>0){
          stack.push(arr.pop())
          while(stack[stack.length-1] < arr[arr.length-1] && k>0) {
              stack.pop();
              k = k-1;
          }
      }
      if(k !== 0) stack = stack.slice(0, -k) 
      return stack.join('') + arr.reverse().join('')
    }
```
