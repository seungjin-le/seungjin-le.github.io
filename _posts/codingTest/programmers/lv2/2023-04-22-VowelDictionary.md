---
title: "[ JS 코딩테스트 LV2 ] 모음 사전"
author: <author_id>
categories: [CodingTest,Programmers,"LV 2"]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---


### 문제 설명
사전에 알파벳 모음 'A', 'E', 'I', 'O', 'U'만을 사용하여 만들 수 있는, 길이 5 이하의 모든 단어가 수록되어 있습니다. 사전에서 첫 번째 단어는 "A"이고, 그다음은 "AA"이며, 마지막 단어는 "UUUUU"입니다.

단어 하나 word가 매개변수로 주어질 때, 이 단어가 사전에서 몇 번째 단어인지 return 하도록 solution 함수를 완성해주세요.

### 제한사항
- word의 길이는 1 이상 5 이하입니다.
- word는 알파벳 대문자 'A', 'E', 'I', 'O', 'U'로만 이루어져 있습니다.

### 입출력 예

|word|	result|
|:--:|:--:|
|"AAAAE"|	6|
|"AAAE"	|10|
|"I"	|1563|
|"EIO"	|1189|

### 입출력 예 설명
#### 입출력 예 #1

- 사전에서 첫 번째 단어는 "A"이고, 그다음은 "AA", "AAA", "AAAA", "AAAAA", "AAAAE", ... 와 같습니다. "AAAAE"는 사전에서 6번째 단어입니다.

#### 입출력 예 #2

- "AAAE"는 "A", "AA", "AAA", "AAAA", "AAAAA", "AAAAE", "AAAAI", "AAAAO", "AAAAU"의 다음인 10번째 단어입니다.

#### 입출력 예 #3

- "I"는 1563번째 단어입니다.

#### 입출력 예 #4

- "EIO"는 1189번째 단어입니다.

### 풀이

```javascript
 const solution = (word) => {
    // 알파벳 단어 순서가 담긴 배열
    const arr = ['A', 'E', 'I', 'O', 'U'];

    // word알파벳 index에 곱할 가중치 배열
    let weighted = [5 ** 4, 5 ** 3, 5 ** 2, 5 ** 1, 5 ** 0];

    // 문자열 word를 배열로 치환후 순회
    return word.split('')
      .map((v, i) => {
        // ex ) i === 0 이라면 weighted의 0번째 인덱스부터 마지막 인덱스까지
        // 값을 더하고 arr안에 v의 인덱스를 곱한다음 + 1
        return weighted.slice(i).reduce((a, b) => a + b) * arr.indexOf(v) + 1;
      })
      .reduce((a, b) => a + b);

```

### 풀이 설명
> - ####  `arr = [A = 0, E = 1, I = 2, O = 3, U = 4]`
> - ####  `weighted = [ 625, 125, 25, 5, 1 ]`
>
> 문재 해결 방법은 word 요소의 index를 구해서 가중치 배열인 weighted의
> index부터 마지막 값을 더한다음 word의 요소가 arr의 몇번째 값인지 구하고 그 값을
> weighted의 index부터 마지막 값을 더한 값에 곱하면 됩니다
>
>
> 1. `word`의 `0번째 인덱스`는 값이 바뀔 때마다 `781의 가중치`를 가집니다
>  - A = 1
>  - E = A + 781 = 782
>  - I = E + 781 = 1563
>  - O = I + 781 = 2344
>  - U = O + 781 = 3125
>
>2. `word`의 `1번째 인덱스`는 값이 바뀔 때마다 `156의 가중치`를 가집니다
>  - AA = 2
>  - AE = AA + 156 = 158
>  - AI = AE + 156 = 314
>  - AO = AI + 156 = 470
>  - AU = AO + 156 = 626
>3. `word`의 `2번째 인덱스`는 값이 바뀔 때마다 `31의 가중치`를 가집니다
>  - AAA = 3
>  - AAE = AAA + 31 = 34
>  - AAI = AAE + 31 = 65
>  - AAO = AAI + 31 = 96
>  - AAU = AAO + 31 = 127
>
>4. `word`의 `3번째 인덱스`는 값이 바뀔 때마다 `6의 가중치`를 가집니다
>  - AAAA = 4
>  - AAAE = AAAA + 6 = 10
>  - AAAI = AAAE + 6 = 16
>  - AAAO = AAAI + 6 = 22
>  - AAAU = AAAO + 6 = 28
>
>5. `word`의 `4번째 인덱스`는 값이 바뀔 때마다 `1의 가중치`를 가집니다
>  - AAAAA = 5
>  - AAAAE = AAAAA + 1 = 6
>  - AAAAI = AAAAE + 1 = 7
>  - AAAAO = AAAAI + 1 = 8
>  - AAAAU = AAAAO + 1 = 9



### 상세 풀이

- #### `weighted = [ 625, 125, 25, 5, 1 ]`

- #### `word = AAAAA`

```jsx
  ( index = 0 ) => weighted의 0번째부터 마지막 요소
    ( 625 + 125 + 25 + 5 + 1 ) * 0 + 1 = 781 * 0( A ) + 1 = 1
  ( index = 1 ) => weighted의 1번째부터 마지막 요소
    ( 125 + 25 + 5 + 1 ) * 0 + 1 = 156 * 0( A ) + 1 = 1
  ( index = 2 ) => weighted의 2번째부터 마지막 요소
    ( 25 + 5 + 1 ) * 0 + 1 = 31 * 0( A ) + 1 = 1
  ( index = 3 ) => weighted의 3번째부터 마지막 요소
    ( 5 + 1 ) * 0 + 1 = 6 * 0( A ) + 1 = 1
  ( index = 4 ) => weighted의 4번째부터 마지막 요소
    ( 1 ) * 0 + 1 = 781 * 0( A ) + 1 = 1

  result = [ 1 + 1 + 1 + 1 + 1 ] = 5

```
---
- #### `word = AAAAE`

```jsx
  ( index = 0 ) => weighted의 0번째부터 마지막 요소
    ( 625 + 125 + 25 + 5 + 1 ) * 0( A ) + 1 = 781 * 0( A ) + 1 = 1
  ( index = 1 ) => weighted의 1번째부터 마지막 요소
    ( 125 + 25 + 5 + 1 ) * 0( A ) + 1 = 156 * 0( A ) + 1 = 1
  ( index = 2 ) => weighted의 2번째부터 마지막 요소
    ( 25 + 5 + 1 ) * 0( A ) + 1 = 31 * 0( A ) + 1 = 1
  ( index = 3 ) => weighted의 3번째부터 마지막 요소
    ( 5 + 1 ) * 0( A ) + 1 = 6 * 0( A ) + 1 = 1
  ( index = 4 ) => weighted의 4번째부터 마지막 요소
    ( 1 ) * 1( E ) + 1 = 781 * 0( E ) + 1 = 2

  result = [ 1 + 1 + 1 + 1 + 2 ] = 6

  AAAAI = 7
    result = [ 1 + 1 + 1 + 1 + 3 ] = 7

  AAAAO = 8
    result = [ 1 + 1 + 1 + 1 + 3 ] = 8

  AAAAU = 9
    result = [ 1 + 1 + 1 + 1 + 3 ] = 9


```
