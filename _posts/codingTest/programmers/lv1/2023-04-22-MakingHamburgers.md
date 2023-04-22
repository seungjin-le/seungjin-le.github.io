---
title: "[ JS 코딩테스트 ] 햄버거 만들기"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

## 문제 설명
햄버거 가게에서 일을 하는 상수는 햄버거를 포장하는 일을 합니다. 함께 일을 하는 다른 직원들이 햄버거에 들어갈 재료를 조리해 주면 조리된 순서대로 상수의 앞에 아래서부터 위로 쌓이게 되고, 상수는 순서에 맞게 쌓여서 완성된 햄버거를 따로 옮겨 포장을 하게 됩니다. 상수가 일하는 가게는 정해진 순서(아래서부터, 빵 – 야채 – 고기 - 빵)로 쌓인 햄버거만 포장을 합니다. 상수는 손이 굉장히 빠르기 때문에 상수가 포장하는 동안 속 재료가 추가적으로 들어오는 일은 없으며, 재료의 높이는 무시하여 재료가 높이 쌓여서 일이 힘들어지는 경우는 없습니다.

예를 들어, 상수의 앞에 쌓이는 재료의 순서가 [야채, 빵, 빵, 야채, 고기, 빵, 야채, 고기, 빵]일 때, 상수는 여섯 번째 재료가 쌓였을 때, 세 번째 재료부터 여섯 번째 재료를 이용하여 햄버거를 포장하고, 아홉 번째 재료가 쌓였을 때, 두 번째 재료와 일곱 번째 재료부터 아홉 번째 재료를 이용하여 햄버거를 포장합니다. 즉, 2개의 햄버거를 포장하게 됩니다.

상수에게 전해지는 재료의 정보를 나타내는 정수 배열 ingredient가 주어졌을 때, 상수가 포장하는 햄버거의 개수를 return 하도록 solution 함수를 완성하시오.

### 제한사항
- 1 ≤ ingredient의 길이 ≤ 1,000,000
- ingredient의 원소는 1, 2, 3 중 하나의 값이며, 순서대로 빵, 야채, 고기를 의미합니다.

### 입출력 예

|ingredient	|result|
|:--:|:--:|
|[2, 1, 1, 2, 3, 1, 2, 3, 1]	|2|
|[1, 3, 2, 1, 2, 1, 3, 1, 2]	|0|

### 입출력 예 설명
#### 입출력 예 #1

- 문제 예시와 같습니다.
#### 입출력 예 #2

- 상수가 포장할 수 있는 햄버거가 없습니다.

### 풀이
> **데이터의 크기가 클수록 정규식(1번 풀이)을 사용한 코드보다, for 문으로 배열을 순회해서 비교(2번째 풀이)
  하는게 6번 테스트에서 약 24배나 빠른 속도를** 보였습니다 정규식이 메모리를 많이 사용한다는 건 알았는데
  이 정도로 차이가 크게 날 줄은 생각도 못 했네요

```jsx
// 정규식 (실패 : 메모리 부족)
  const solution = (ingredient) => {
    // ingredient의 초기 길이값을 저장
    const len = ingredient.length;
    // 숫자 배열을 문자열로 치환
    ingredient = ingredient.join('');
    // 문자열 ingredient 안에 문자열 '1231'이 있으면 반복
    while (ingredient.includes('1231')) {
      // 문자열 ingredient 앞에사부터 '1231' 반복해서 제거
      ingredient = ingredient.replace(/1231/, '');
    }
    // 문자열에서 4개씩 제거를 하니 초기 문자열의 길이 - 문자 제거후 길이
    // 문자열 길이를 뺀다음 나머지를 4로 나누면 제거한 '1231'의 갯수
    return (len - ingredient.length) / 4;
  };

  // 정답
  const solution2 = (ingredient) => {
    // ingredient의 초기 길이값을 저장
    const len = ingredient.length;
    // ingredient의 길이만큼 반복
    for (let a = 0; a <= ingredient.length; a++) {
      if (
        // ingredient의 a번째 값이 숫자열 1이면 다음 조건 확인
        ingredient[a] === 1 &&
        // ingredient의 (a + 1)번째 값이 숫자열 2이면 다음 조건 확인
        ingredient[a + 1] === 2 &&
        // ingredient의 (a + 2)번째 값이 숫자열 3이면 다음 조건 확인
        ingredient[a + 2] === 3 &&
        // ingredient의 (a + 3)번째 값이 숫자열 1이면 다음 조건 확인
        ingredient[a + 3] === 1
      ) {
        // ingredient배열의 a번째부터 뒤로 4칸 삭제
        ingredient.splice(a, 4);
        // a를 앞으로 4칸 이동
        a -= 4;
      }
    }
    // 문자열에서 4개씩 제거를 하니 초기 문자열의 길이 - 문자 제거후 길이
    // 문자열 길이를 뺀다음 나머지를 4로 나누면 제거한 '1231'의 갯수
    return (len - ingredient.length) / 4;
  };
```
### 1번 코드와 2번 코드의 메모리 사용량
- #### 1번 풀이(메모리 부족)
  ![](https://velog.velcdn.com/images/dltmdwls15/post/6592854a-a310-4b5d-bd53-8181f3399af9/image.png)
- #### 2번 풀이(정답)
  ![](https://velog.velcdn.com/images/dltmdwls15/post/bacf0516-9783-4f7e-8abb-90a480f6cb66/image.png)


