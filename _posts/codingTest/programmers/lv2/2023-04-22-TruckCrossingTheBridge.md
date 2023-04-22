---
title: "[ JS 코딩테스트 LV2 ] 다리를 지나는 트럭"
author: <author_id>
categories: [CodingTest,Programmers,"LV 2"]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
트럭 여러 대가 강을 가로지르는 일차선 다리를 정해진 순으로 건너려 합니다. 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 알아내야 합니다. 다리에는 트럭이 최대 bridge_length대 올라갈 수 있으며, 다리는 weight 이하까지의 무게를 견딜 수 있습니다. 단, 다리에 완전히 오르지 않은 트럭의 무게는 무시합니다.

예를 들어, 트럭 2대가 올라갈 수 있고 무게를 10kg까지 견디는 다리가 있습니다. 무게가 [7, 4, 5, 6]kg인 트럭이 순서대로 최단 시간 안에 다리를 건너려면 다음과 같이 건너야 합니다.

|경과 시간| 	다리를 지난 트럭  | 	다리를 건너는 트럭 |   	대기 트럭   |
|:--:|:-----------:|:-----------:|:----------:|
|0|    	[ ]     |    	[ ]     | 	[7,4,5,6] |
|1~2|    [ ]	     |     [7]     |  	[4,5,6]  |
|3|    	[7]     |    	[4]     |   	[5,6]   |
|4	|    [7]	     |    [4,5]    |    	[6]    |
|5|   	[7,4]	   |    [5]	     |    [6]     |
|6~7|  	[7,4,5]	  |     [6]     |    	[ ]    |
|8| 	[7,4,5,6]	 |     [ ]     |    	[ ]    |

따라서, 모든 트럭이 다리를 지나려면 최소 8초가 걸립니다.

solution 함수의 매개변수로 다리에 올라갈 수 있는 트럭 수 bridge_length, 다리가 견딜 수 있는 무게 weight, 트럭 별 무게 truck_weights가 주어집니다. 이때 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 return 하도록 solution 함수를 완성하세요.

### 제한 조건
+ bridge_length는 1 이상 10,000 이하입니다.
+ weight는 1 이상 10,000 이하입니다.
+ truck_weights의 길이는 1 이상 10,000 이하입니다.
+ 모든 트럭의 무게는 1 이상 weight 이하입니다.

### 입출력 예

|bridge_length|	weight|	truck_weights| 	return |
|:--:|:--:|:--:|:-------:|
|2|	10|	[7,4,5,6]|   	8    |
|100	|100	|[10]	|   101   |
|100|	100|	[10,10,10,10,10,10,10,10,10,10]	|   110   |

### 풀이
```jsx
const solution = (bridge_length, weight, truck_weights) => {
    let answer = 0;
    // 다리의 길이만큼 0으로된 배열생성
    let arr = new Array(bridge_length).fill(0);
    // do는 반복문 while의 조건을 판단하기 전에 한번은 실행됩니다.
    do {
      // 첫번째 트럭이 다리에 올라가서 answer++
      answer++;
      // arr의 마지막 요소 삭제
      arr.pop();
      // unshift는 배열의 첫번째 위치에 요소를 추가해주는 함수
      // reduce함수를 이용해 arr의 총합과 대기중인 트럭(truck_weights)
      // 첫번째 요소를 더했을때 다리가 견딜수 있는 무게(weight)보다
      // 작거나 같으면 truck_weights의 첫번째 요소를
      // arr의 맨 앞자리에 추가
      // 다리가 견딜수 있는 무게보다 크다면 0을 추가
      arr.unshift(
        arr.reduce((a, b) => a + b) + truck_weights[0] <= weight
          ? truck_weights.shift()
          : 0
      );
      // do스코프 안에 코드를 한번 실행했으니 arr의 총합이 
      // 0이 아니게되므로 반복문을 0이 될때까지 실행
    } while (arr.reduce((a, b) => a + b) !== 0);
    return answer;
  };
```
