---
title: "[ JS 코딩테스트 LV2 ] 2 X n 타일링"
author: <author_id>
categories: [CodingTest,Programmers,"LV 2"]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---


### 문제 설명
가로 길이가 2이고 세로의 길이가 1인 직사각형모양의 타일이 있습니다. 이 직사각형 타일을 이용하여 세로의 길이가 2이고 가로의 길이가 n인 바닥을 가득 채우려고 합니다. 타일을 채울 때는 다음과 같이 2가지 방법이 있습니다.

- 타일을 가로로 배치 하는 경우
- 타일을 세로로 배치 하는 경우
  예를들어서 n이 7인 직사각형은 다음과 같이 채울 수 있습니다.

![](https://velog.velcdn.com/images/dltmdwls15/post/abb52620-b7d1-4be5-bd50-a5945d80c156/image.png)


직사각형의 가로의 길이 n이 매개변수로 주어질 때, 이 직사각형을 채우는 방법의 수를 return 하는 solution 함수를 완성해주세요.

### 제한사항
- 가로의 길이 n은 60,000이하의 자연수 입니다.
- 경우의 수가 많아 질 수 있으므로, 경우의 수를 1,000,000,007으로 나눈 나머지를 return해주세요.

|입출력| 예|
|:--:|:--:|
|n|	result|
|4	|5|

### 입출력 예 설명
#### 입출력 예 #1
- 다음과 같이 5가지 방법이 있다.

![](https://velog.velcdn.com/images/dltmdwls15/post/86b5dcb4-2c31-4a98-be3c-1b96c5655a5a/image.png)


![](https://velog.velcdn.com/images/dltmdwls15/post/62eb82e6-4a69-4809-8099-0cbbd4563a5d/image.png)


![](https://velog.velcdn.com/images/dltmdwls15/post/e9f35afb-9239-4933-bf8a-dc958cc85809/image.png)


![](https://velog.velcdn.com/images/dltmdwls15/post/5f620710-93b4-4932-9257-a0d73cbcaafc/image.png)


![](https://velog.velcdn.com/images/dltmdwls15/post/2a29f9e1-dc8e-4765-86e1-90ef84e22989/image.png)

### 풀이
- 처음에 가짓수를 구하는 패턴을 찾으려고 하나하나 경우의 수를 구하다가 가짓수 패턴이
  피보나치수열과 너무 유사해서 피보나치를 적용했더니 풀렸던 문제였습니다.

```javascript
 const solution = (n) => {
    // 타일링 가짓수를 담은 배열
    let arr = [0,1,2]
    // n의 값이 3까지는 타일링을 배치할수 있는 가짓수도 같으므로 그대로 리턴
    if(n <= 3) return n

    // 타일링의 가짓수는 피보나치 수열처럼 이전 값들을 더하면 됩니다,
    for(let a = 3; a <= n; a++){
      // arr[1] => a-2, arr[2] = a-1
      // arr[1]에 이전값(a - 1)을 넣기 위해 미리 arr[0]에 arr[1]과 arr[2]를
      // 더한후 1,000,000,007을 나눈값으로 변경
      // ex ) a = 3, arr = [ 0, 1, 2 ]
      arr[0] = (arr[1] + arr[2]) % ( 10** 9 + 7);
      // arr[1]을 a-2 값으로 변경
      arr[1] = arr[2];
      // arr[2]를 a-1 값으로 변경
      arr[2] = arr[0];
      // ex ) a = 3, arr = [ 3, 2, 3 ]
    }
    return arr[0];
  }
  // 0 -> 0
  // 1 = 0 + 1 -> 1
  // 2 = 1 + 1 -> 2
  // 3 = 1 + 2 -> 3
  // 4 = 2 + 3 -> 5
  // 5 = 3 + 5 -> 8
  // 6 = 5 + 8 -> 13
  // 7 = 8 + 13 -> 21
  // 8 = 13  + 21 -> 34
  // 9 = 21 + 34 -> 55
  // 10 = 34 + 55 -> 89
  // 11 = 55 + 89 -> 144
  // 12 = 89 + 144 -> 233
  // 13 = 144 + 233 -> 377
```
