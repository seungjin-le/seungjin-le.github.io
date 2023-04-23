---
title: "[ JS 코딩테스트 LV2 ] 호텔 대실"
author: <author_id>
categories: [CodingTest,Programmers,"LV 2"]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---


### 문제 설명
호텔을 운영 중인 코니는 최소한의 객실만을 사용하여 예약 손님들을 받으려고 합니다. 한 번 사용한 객실은 퇴실 시간을 기준으로 10분간 청소를 하고 다음 손님들이 사용할 수 있습니다.
예약 시각이 문자열 형태로 담긴 2차원 배열 book_time이 매개변수로 주어질 때, 코니에게 필요한 최소 객실의 수를 return 하는 solution 함수를 완성해주세요.

### 제한사항
- 1 ≤ book_time의 길이 ≤ 1,000
  - book_time[i]는 ["HH:MM", "HH:MM"]의 형태로 이루어진 배열입니다
    - [대실 시작 시각, 대실 종료 시각] 형태입니다.
  - 시각은 HH:MM 형태로 24시간 표기법을 따르며, "00:00" 부터 "23:59" 까지로 주어집니다.
    - 예약 시각이 자정을 넘어가는 경우는 없습니다.
    - 시작 시각은 항상 종료 시각보다 빠릅니다.

### 입출력 예

|book_time|	result|
|:--:|:--:|
|[["15:00", "17:00"], ["16:40", "18:20"], ["14:20", "15:20"], ["14:10", "19:20"], ["18:20", "21:20"]]	|3|
|[["09:10", "10:10"], ["10:20", "12:20"]]	|1|
|[["10:20", "12:30"], ["10:20", "12:30"], ["10:20", "12:30"]]	|3|


### 입출력 예 설명
#### 입출력 예 #1

- ![](https://velog.velcdn.com/images/dltmdwls15/post/f4cf6ab0-d046-410e-98d6-d5200004a4e1/image.png)

- 위 사진과 같습니다.

#### 입출력 예 #2

- 첫 번째 손님이 10시 10분에 퇴실 후 10분간 청소한 뒤 두 번째 손님이 10시 20분에 입실하여 사용할 수 있으므로 방은 1개만 필요합니다.

#### 입출력 예 #3

- 세 손님 모두 동일한 시간대를 예약했기 때문에 3개의 방이 필요합니다.

### 풀이
```jsx
 const solution = (book_time) => {
    // 입실, 퇴실 시간을 담을 이차원 배열
    let arr = [];
    // 시간을 분으로 계산
    const getTime = (value) => {
      const [h, m] = value.split(':');
      return +h * 60 + +m;
    };

    // 시간을 분으로 계산
    //  ex ) [ "14:20", "15:20" ] => [ 860, 920 ]
    book_time
      .map((v) => v.map((v2) => getTime(v2)))
      // 손님의 입실 시간이 빠른 순부터 오름차순
      .sort((a, b) => a[0] - b[0])
      .map((v) => {
        // arr의 길이가 0이면 0번째 인덱스에 v 추가
        // ex ) arr = [ [ 860, 920 ] ]
        if (arr.length === 0) return arr.push(v);
        // arr의 길이만큼 반복
        for (let a = 0; a <= arr.length; a++) {
          // arr의 a번째 배열의 마지막 요소에 10을 더한 값이 v의 0번째 값보다 같거나 작으면 arr의 a번째 배열에 v 추가
          // ex ) arr[a] = [ 860, 920 ] ,  v = [ 940, 1000 ]  => arr[a] = [ 860, 920, 940, 1000 ]
          if (arr[a][arr[a].length - 1] + 10 <= v[0]) return arr[a].push(...v);

          // arr의 마지막 요소까지 왔을 때까지 위 조건문에 해당되지 않았다면 arr에 새로 요소 추가
          // ex ) arr = [ [ 860, 920, 940, 1000 ], [960, 1100] ], v = [ 970, 980 ] =>
          // arr = [ [ 860, 920, 940, 1000 ], [960, 1100], [ 970, 980 ] ]
          if (!arr[a + 1]) return arr.push(v);
        }
      });
    // arr의 길이를 리턴
    return arr.length;
  };
```
