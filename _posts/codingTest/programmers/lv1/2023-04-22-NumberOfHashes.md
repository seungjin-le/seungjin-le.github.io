---
title: "[ JS 코딩테스트 ] 하샤드 수"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
- 양의 정수 x가 하샤 드 수이려면 x의 자릿수의 합으로 x가 나누어져야 합니다. 예를 들어 18의 자릿수 합은 1+8=9이고, 18은 9로 나누어 떨어지므로 18은 하샤 드 수입니다. 자연수 x를 입력받아 x가 하샤 드 수인지 아닌지 검사하는 함수, solution을 완성해주세요.

### 제한 조건
- x는 1 이상, 10000 이하인 정수입니다.

### 입출력 예

| arr | return |
|:---:|:------:|
| 10  | 	true  |
| 12	 |  true  |
| 11	 | false  |
| 13  | 	false |

### 입출력 예 설명
#### 입출력 예 #1
- 10의 모든 자릿수의 합은 1입니다. 10은 1로 나누어 떨어지므로 10은 하샤드 수입니다.

#### 입출력 예 #2
- 12의 모든 자릿수의 합은 3입니다. 12는 3으로 나누어 떨어지므로 12는 하샤드 수입니다.

#### 입출력 예 #3
- 11의 모든 자릿수의 합은 2입니다. 11은 2로 나누어 떨어지지 않으므로 11는 하샤 드 수가 아닙니다.

#### 입출력 예 #4
- 13의 모든 자릿수의 합은 4입니다. 13은 4로 나누어 떨어지지 않으므로 13은 하샤드 수가 아닙니다.

### 풀이
```javascript
function solution(x) {
    var answer= 0;
    let a = (x + '').split('');
    a.map(x => answer += Number(x));
    return x %answer===0;
}
```

### 문제 풀이
> 매개변수 x로 숫자값을 받아와 (x + ''로) 문자 열로 만들고 split함수로 문자 배열로 만들어줍니다 그 후 map을 이용해서 배열을 순회하면서 배열 안의 문자 값을 숫자 값으로 변환 후 answer변수에 더해주고 x를 answer로 나눴을 때 나머지가 0이면 true 아니면 false를 반환해줍니다

