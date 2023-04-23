---
title: "[ JS 코딩테스트 LV2 ] 2개 이하로 다른 비트 (첫 10점 짜리 정답)"
author: <author_id>
categories: [CodingTest,Programmers,"LV 2"]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---


### 문제 설명
양의 정수 x에 대한 함수 f(x)를 다음과 같이 정의합니다.
- x보다 크고 x와 비트가 1~2개 다른 수들 중에서 제일 작은 수
  예를 들어,

- f(2) = 3 입니다. 다음 표와 같이 2보다 큰 수들 중에서 비트가 다른 지점이 2개 이하이면서 제일 작은 수가 3이기 때문입니다.

|수|	비트|	다른 비트의 개수|
|:--:|:--:|:--:|
|2|	000...0010	||
|3|	000...0011	|1|

- `f(7) = 11` 입니다. 다음 표와 같이 7보다 큰 수들 중에서 비트가 다른 지점이 2개 이하이면서 제일 작은 수가 11이기 때문입니다.

|수	|비트|	다른 비트의 개수|
|:--:|:--:|:--:|
|7|	000...0111	||
|8|	000...1000	|4|
|9	|000...1001	|3|
|10	|000...1010	|3|
|11	|000...1011	|2|

- 정수들이 담긴 배열 numbers가 매개변수로 주어집니다. numbers의 모든 수들에 대하여 각 수의 f 값을 배열에 차례대로 담아 return 하도록 solution 함수를 완성해주세요.

### 제한사항
- 1 ≤ numbers의 길이 ≤ 100,000
- 0 ≤ numbers의 모든 수 ≤ 1015

### 입출력 예

|numbers|	result|
|:--:|:--:|
|[2,7]|	[3,11]|

### 입출력 예 설명
#### 입출력 예 #1

- 문제 예시와 같습니다.

### 풀이
- 처음으로 10점 받은 문제였습니다.

```javascript
 const solution = (numbers) => {
    // ex ) numbers = [ 2, 7 ]
    return numbers.map((v) => {
      // numbers의 요소인 v를 2진수로 만들고 배열로 치환한 뒤 배열을 뒤집고 가장 가까운 "0"의 index를 찾습니다
      // ex) 2 => "10" => [ "1", "0" ] => [ "0", "1" ] => 0 = 가장 가까운 0의 Index
      let toStr = v.toString(2).split('').reverse().indexOf('0')

      // indexOf 함수로 "0"을 찾을 수 없다면 -1이기 때문에 2진수로 치환한 문자열의 길이 - 1값을
      // 2에 거듭제곱해 준 후 10진수인 v( 7 )에 더해줍니다
      // ex ) 7 = "111" => "111".length = 3 => 2 ** (3 - 1) = 4 => v( 7 ) + 4 = 11
      if (toStr === -1) return v + 2 ** (v.toString(2).length - 1)

      // 0의 index를 - 1 해준 값을 2에 거듭제곱을 해주고 올림 함수를 이용해 올림 해주고
      // 10진수인 v( 2 )에 더해줍니다
      return v + Math.ceil(2 ** (toStr - 1))
    });
  }
```
