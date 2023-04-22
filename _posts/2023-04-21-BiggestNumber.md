---
title: "[ JS 코딩테스트 LV2 ] 가장 큰 수"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.

예를 들어, 주어진 정수가 `[6, 10, 2]`라면 `[6102, 6210, 1062, 1026, 2610, 2106]`를 만들 수 있고, 이중 가장 큰 수는 6210입니다.

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.

### 제한 사항
+ numbers의 길이는 1 이상 100,000 이하입니다.
+ numbers의 원소는 0 이상 1,000 이하입니다.
+ 정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.

### 입출력 예

|numbers|return|
|:--:|:--:|
|[6, 10, 2]|"6210"|
|[3, 30, 34, 5, 9]|"9534330"|

### 풀이
### 1차 시도(실패)

```javascript
const solution = (numbers) => {
    let arr = numbers.map((v) => String(v))
    arr = arr.sort((a,b) => {
      if(+b[0] === +a[0]){
        if(+b === 0 && +a === 0){
          return false
        }
        for(let x = 1; x <= Math.max(a.length,b.length); x++){
          let l = 1
          let r = 1
          if(isNaN(+b[x]) || isNaN(+a[x])){
            if(isNaN(+b[x])){
              if(+b[x-l] !== +a[x]){
                return  +b[x-l] - +a[x]
              }
              l++
            }else if(isNaN(+a[x])){
              if(+b[x] !== +a[x-r]){
                return +b[x] - +a[x-r]
              }
              r++
            }
          }else{
            if(+b[x] !== +a[x]){
              return +b[x] - +a[x]
            }
          }
        }}
      return +b[0] - +a[0]
    })
    if(arr[0] === '0'){
      return '0'
    }
    return arr.join('');
  }
```
> 처음에 생각한 건 10보다 작은 수들은 큰 수로 나열하면 되지만 10부터는 뒷자리까지 비교를 해줘야 하기 때문에 요소의 첫 번째 숫자(string)가 같을 시 두 번째 세 번째 자리까지 비교를 해주도록 코드를 작성했었습니다. 하지만 길이가 다르고 길이가 짧은 숫자의 길이까지 비교했을 때 값이 같으면 짧은 배열 순서상 앞에 있는 값을 반환해서 틀렸습니다.

### 2차 시도(정답)
```javascript
const solution = (numbers) => {
    let arr = numbers.map((v) => String(v))
    arr = arr.sort((a,b) =>  parseInt( b + a ) - parseInt(a + b));
    return arr[0] === '0' ? '0' : arr.join('');
  }
```

### 후기
> 프로그래머스 질문하기에서 어떤 분이 힌트로 a+b랑 b+a를 비교해 보라 해서 비교했더니 쉽게 풀렸습니다.
