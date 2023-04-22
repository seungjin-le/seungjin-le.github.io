---
title: "[ JS 코딩테스트 LV2 ] 타겟 넘버"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
n개의 음이 아닌 정수들이 있습니다. 이 정수들을 순서를 바꾸지 않고 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.

+ -1+1+1+1+1 = 3
+ +1-1+1+1+1 = 3
+ +1+1-1+1+1 = 3
+ +1+1+1-1+1 = 3
+ +1+1+1+1-1 = 3

사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

### 제한사항
- 주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
- 각 숫자는 1 이상 50 이하인 자연수입니다.
- 타겟 넘버는 1 이상 1000 이하인 자연수입니다.

### 입출력 예

|numbers|	target| 	return |
|:--:|:--:|:-------:|
|[1, 1, 1, 1, 1]	|3	|    5    |
|[4, 1, 2, 1]|	4|   	2    |

### 입출력 예 설명
#### 입출력 예 #1

+ 문제 예시와 같습니다.

#### 입출력 예 #2

- +4 + 1 - 2 + 1 = 4
- +4 - 1 + 2 - 1 = 4

총 2가지 방법이 있으므로, 2를 return 합니다.


### 풀이
```javascript
const solution = (numbers, target) => {
    let answer = 0;
    // 함수 counts에 매개변수가 주어지지 않았을 경우 기본값 0
    const counts = (count = 0, sum = 0) => {
      // count가 numbers의 길이와 같아졌을경우
      if (count === numbers.length) {
        // 반복해서 더하고 뺀sum가 target과 같을경우 answer + 1 한다음 함수 종료
        if (target === sum) {
          answer++;
        }
        return;
      }
      // count가 numbers의 길이와 다를 경우 sum 과 numbers[count]를
      // 더하거나 빼도록 2개의 함수 실행
      counts(count + 1, sum + numbers[count]);
      counts(count + 1, sum - numbers[count]);
    };

    counts();
    return answer;
  };
```
