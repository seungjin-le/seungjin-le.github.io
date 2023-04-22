---
title: "[ JS 코딩테스트 LV2 ] 행렬의 곱셈"
author: <author_id>
categories: [CodingTest,Programmers,"LV 2"]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---


### 문제 설명
2차원 행렬 arr1과 arr2를 입력받아, arr1에 arr2를 곱한 결과를 반환하는 함수, solution을 완성해주세요.

### 제한 조건
- 행렬 arr1, arr2의 행과 열의 길이는 2 이상 100 이하입니다.
- 행렬 arr1, arr2의 원소는 -10 이상 20 이하인 자연수입니다.
- 곱할 수 있는 배열만 주어집니다.

### 입출력 예

|arr1|	arr2|	return|
|:--:|:--:|:--:|
|[[1, 4], [3, 2], [4, 1]]|	[[3, 3], [3, 3]]|	[[15, 15], [15, 15], [15, 15]]|
|[[2, 3, 2], [4, 2, 4], [3, 1, 4]]	|[[5, 4, 3], [2, 4, 1], [3, 1, 1]]	|[[22, 22, 11], [36, 28, 18], [29, 20, 14]]|

### 풀이
```javascript
const solution = (arr1, arr2) => {
    // 행렬의 곱한 값을 담을 배열
    let answer = []

    // 이차원 배열 arr1 순회
    // ex ) arr1 = [[1, 2, 3], [4, 5, 6]]
    // ex ) arr2 = [[1, 4], [2, 5], [3, 6]]
    arr1.map((value, index) => {
      // 빈배열인 answer의 index번째 요소로 빈배열 추가
      answer[index] = []
      // arr2의 0번째 요소만큼 반복
      for (let a = 0; a < arr2[0].length; a++) {
        // 행열의 곱한 값을 더할 변수
        let b = 0
        // arr1의 index번째 요소인 배열을 순회
        // ex ) v = [ 1, 2, 3 ], i = 0, 1, 2
        value.map((v, i) => {
          // 이차원 배열 arr2의 i번째 배열의 a값을 
          // arr의 index번째 배열의 i번째 값인 v를 
          // 곱한값을 미리 선언했던 인스턴트 변수인 b에 더해줍니다
          // ex ) arr2[i] = [ 1, 4 ], arr2[i][a] = 1, 4, v = 1, 2, 3
          //  [ v * arr2[i][a] + v * arr2[i][a + 1] + v * arr2[i][a + 2]]
          //  [(1 * 1) + (2 * 2) + (3 * 3)]
          //  = 14
          b += v * arr2[i][a]
        })
        // value.map 함수가 끝나면 빈배열인 answer의 index번째에 
        // map함수에서 곱하고 더한값을 추가
        // ex ) answer = [ [ 14 ], ]
        answer[index].push(b)
      }
    })
    return answer;
  }

  // 테스트 케이스에서 arr1의 길이가 arr2의 길이보다 길 수 있어서
  // 이 부분을 주의하지 않으면 테스트 케이스 0점입니다.

  // arr1 : [[1, 2, 3], [4, 5, 6]]

  // arr2 : [[1, 4], [2, 5], [3, 6]]

  // return : [[14, 32], [32, 77]]

```
