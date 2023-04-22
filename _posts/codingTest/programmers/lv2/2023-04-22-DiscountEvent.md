---
title: "[ JS 코딩테스트 LV2 ] 할인 행사"
author: <author_id>
categories: [CodingTest,Programmers,"LV 2"]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---


### 문제 설명
XYZ 마트는 일정한 금액을 지불하면 10일 동안 회원 자격을 부여합니다. XYZ 마트에서는 회원을 대상으로 매일 한 가지 제품을 할인하는 행사를 합니다. 할인하는 제품은 하루에 하나씩만 구매할 수 있습니다. 알뜰한 정현이는 자신이 원하는 제품과 수량이 할인하는 날짜와 10일 연속으로 일치할 경우에 맞춰서 회원가입을 하려 합니다.

예를 들어, 정현이가 원하는 제품이 바나나 3개, 사과 2개, 쌀 2개, 돼지고기 2개, 냄비 1개이며, XYZ 마트에서 15일간 회원을 대상으로 할인하는 제품이 날짜 순서대로 치킨, 사과, 사과, 바나나, 쌀, 사과, 돼지고기, 바나나, 돼지고기, 쌀, 냄비, 바나나, 사과, 바나나인 경우에 대해 알아봅시다. 첫째 날부터 열흘 간에는 냄비가 할인하지 않기 때문에 첫째 날에는 회원가입을 하지 않습니다. 둘째 날부터 열흘 간에는 바나나를 원하는 만큼 할인구매할 수 없기 때문에 둘째 날에도 회원가입을 하지 않습니다. 셋째 날, 넷째 날, 다섯째 날부터 각각 열흘은 원하는 제품과 수량이 일치하기 때문에 셋 중 하루에 회원가입을 하려 합니다.

정현이가 원하는 제품을 나타내는 문자열 배열 want와 정현이가 원하는 제품의 수량을 나타내는 정수 배열 number, XYZ 마트에서 할인하는 제품을 나타내는 문자열 배열 discount가 주어졌을 때, 회원등록시 정현이가 원하는 제품을 모두 할인 받을 수 있는 회원등록 날짜의 총 일수를 return 하는 solution 함수를 완성하시오. 가능한 날이 없으면 0을 return 합니다.

### 제한사항
- 1 ≤ want의 길이 = number의 길이 ≤ 10
  - 1 ≤ number의 원소 ≤ 10
  - number[i]는 want[i]의 수량을 의미하며, number의 원소의 합은 10입니다.
- 10 ≤ discount의 길이 ≤ 100,000
  - want와 discount의 원소들은 알파벳 소문자로 이루어진 문자열입니다.
  - 1 ≤ want의 원소의 길이, discount의 원소의 길이 ≤ 12

### 입출력 예

|want|	number|	discount|	result|
|:--:|:--:|:--:|:--:|
|["banana", "apple", "rice", "pork", "pot"]	|[3, 2, 2, 2, 1]	|["chicken", "apple", "apple", "banana", "rice", "apple", "pork", "banana", "pork", "rice", "pot", "banana", "apple", "banana"]	|3|
|["apple"]|	[10]	|["banana", "banana", "banana", "banana", "banana", "banana", "banana", "banana", "banana", "banana"]	|0|

### 입출력 예 설명
#### 입출력 예 #1
- 문제 예시와 같습니다.
- 
#### 입출력 예 #2
- 사과가 할인하는 날이 없으므로 0을 return 합니다.

### 풀이

```javascript
 const solution = (want, number, discount) => {
    // 구매해야 하는 과일 개수를 담을 객체
    let obj = {};
   
    // 과일을 전부 구매할 수 있는 날을 담을 이차원 배열
    let arr = [];
   
    // 구매할 과일을 담은 배열 want 순회
    // 빈 객체인 obj에 v라는 key 값으로 number의 i 번째 값을 추가
    // *배열 number는 want의 개수를 순서대로 담겨있습니다.
    want.map((v, i) => (obj[v] = number[i]));

    // 문제 1번 예시
    // obj = { banana: 3, apple: 2, rice: 2, pork: 2, pot: 1 }
   
    // 과일 할인하는 날이 담긴 배열 dusciunt순회
    discount.map((v, i) => {
      // 10일 동안 가입할 수 있으므로 i부터 i + 10까지 잘라서
      // arr에 push
      arr.push(discount.slice(i, i + 10));
    });
   
    // 문제 1번 예시
    // 요소의 Index + 1이 회원가입한 날이며
    // 각 요소마다 회원가입 후 10일간 구매할 수 있는 과일
    // arr = [
    //   [
    //     'chicken', 'apple',
    //     'apple',   'banana',
    //     'rice',    'apple',
    //     'pork',    'banana',
    //     'pork',    'rice'
    //   ],
    //   [
    //     'apple',  'apple',
    //     'banana', 'rice',
    //     'apple',  'pork',
    //     'banana', 'pork',
    //     'rice',   'pot'
    //   ], 
    //   ....
    //   [ 'apple', 'banana' ],
    //   [ 'banana' ]
    // ]
   
    // i 일부터 i + 10일까지 판매하는 과일 배열이 담긴 이차원배열 arr을
    // filter함수로 순회
    arr = arr.filter((v, i) => {
      
      // 필요한 과일 개수가 담긴 객체 obj를 얕은 복사
      let wants = { ...obj };
      
      // i 일부터 i + 10일까지 판매하는 과일 리스트 배열 순회
      v.map((value) => {
        // wants의 valye라는 key 값을 가진 변수가 0이 아니라면 -1
        if (wants[value] > 0) wants[value]--;
      });
      
      // 필요한 과일 개수가 담긴 객체 wants를 순회하면서
      // value 값이 0이라면 해당 객체에서 변수 삭제
      Object.entries(wants).forEach(
        ([key, value]) => value === 0 && delete wants[key]
      );
      
      // 필요한 과일을 모두 샀다면 wants에서 모든 변수가 삭제되었으니
      // wnats의 길이가 0이라면 return 값이 turn 값이 되고
      // arr.filter 함수를 통해 arr에 추가되고
      // wants의 길이가 0이 아니라면 arr에 추가되지 않습니다.
      return Object.keys(wants).length === 0;
    });
   
    // filter 함수를 통해서 모든 과일을 살수 있는 날만
    // arr에 추가되었으므로 arr의 길이를 return
    return arr.length;
  };
```
