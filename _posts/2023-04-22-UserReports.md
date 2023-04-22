---
title: "[ JS 코딩테스트 ] 신고 결과 받기"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
>신입사원 무지는 게시판 불량 이용자를 신고하고 처리 결과를 메일로 발송하는 시스템을 개발하려 합니다. 무지가 개발하려는 시스템은 다음과 같습니다.

+	각 유저는 한 번에 한 명의 유저를 신고할 수 있습니다.
   -	신고 횟수에 제한은 없습니다. 서로 다른 유저를 계속해서 신고할 수 있습니다.
   -	한 유저를 여러 번 신고할 수도 있지만, 동일한 유저에 대한 신고 횟수는 1회로 처리됩니다.
+	k번 이상 신고된 유저는 게시판 이용이 정지되며, 해당 유저를 신고한 모든 유저에게 정지 사실을 메일로 발송합니다.
   -	유저가 신고한 모든 내용을 취합하여 마지막에 한꺼번에 게시판 이용 정지를 시키면서 정지 메일을 발송합니다.
   -	다음은 전체 유저 목록이 ["muzi", "frodo", "apeach", "neo"]이고, k = 2(즉, 2번 이상 신고당하면 이용 정지)인 경우의 예시입니다.

|유저 ID|유저가신고한 ID|설명|
| :--:|:--:|:--:|
|"muzi"|"frodo"|"muzi"가 "frodo"를 신고했습니다.|
|"apeach"|"frodo"|"apeach"가 "frodo"를 신고했습니다.|
|"frodo"|"neo"|"frodo"가 "neo"를 신고했습니다.|
|"muzi"|"neo"|"muzi"가 "neo"를 신고했습니다.|
|"apeach"|"muzi"|"apeach"가 "muzi"를 신고했습니다.|

각 유저별로 신고당한 횟수는 다음과 같습니다.

|유저 ID|신고당한 횟수|
|:--:|:--:|
|"muzi"|1|
|"frodo"|2|
|"apeach"|0|
|"neo"|2|

위 예시에서는 2번 이상 신고당한 "frodo"와 "neo"의 게시판 이용이 정지됩니다. 이때, 각 유저별로 신고한 아이디와 정지된 아이디를 정리하면 다음과 같습니다.

|유저 ID|유저가 신고한 ID|정지된 ID|
|:--:|:--:|:--:|
|"muzi"|["frodo", "neo"]|["frodo", "neo"]|
|"frodo"|["neo"]|["neo"]|
|"apeach"|["muzi", "frodo"]|["frodo"]|
|"neo"|없음|없음|

따라서 "muzi"는 처리 결과 메일을 2회, "frodo"와 "apeach"는 각각 처리 결과 메일을 1회 받게 됩니다.

이용자의 ID가 담긴 문자열 배열 id_list, 각 이용자가 신고한 이용자의 ID 정보가 담긴 문자열 배열 report, 정지 기준이 되는 신고 횟수 k가 매개변수로 주어질 때, 각 유저별로 처리 결과 메일을 받은 횟수를 배열에 담아 return 하도록 solution 함수를 완성해주세요.

### 제한사항
+ 2 ≤ id_list의 길이 ≤ 1,000
  + 1 ≤ id_list의 원소 길이 ≤ 10
  + id_list의 원소는 이용자의 id를 나타내는 문자열이며 알파벳 소문자로만 이루어져 있습니다.
  + id_list에는 같은 아이디가 중복해서 들어있지 않습니다.
- 1 ≤ report의 길이 ≤ 200,000
  - 3 ≤ report의 원소 길이 ≤ 21
  - report의 원소는 "이용자id 신고한id"형태의 문자열입니다.
  - 예를 들어 "muzi frodo"의 경우 "muzi"가 "frodo"를 신고했다는 의미입니다.
  - id는 알파벳 소문자로만 이루어져 있습니다.
  - 이용자id와 신고한id는 공백(스페이스)하나로 구분되어 있습니다.
  - 자기 자신을 신고하는 경우는 없습니다.
  - 1 ≤ k ≤ 200, k는 자연수입니다.
+ return 하는 배열은 id_list에 담긴 id 순서대로 각 유저가 받은 결과 메일 수를 담으면 됩니다.

### 입출력 예

|id_list|                               report                               |k|result|
|:---:|:------------------------------------------------------------------:|:---:|:---:|
|["muzi", "frodo", "apeach", "neo"] | ["muzi frodo","apeach frodo","frodo neo","muzi neo","apeach muzi"] | 2 | [2,1,1,0] |
|["con", "ryan"]|["ryan con", "ryan con","ryan con", "ryan con"]|3|[0,0]|

### 입출력 예 설명
#### 입출력 예 #1

- 문제의 예시와 같습니다.

#### 입출력 예 #2

- "ryan"이 "con"을 4번 신고했으나, 주어진 조건에 따라 한 유저가 같은 유저를 여러 번 신고한 경우는 신고 횟수 1회로 처리합니다. 따라서 "con"은 1회 신고당했습니다. 3번 이상 신고당한 이용자는 없으며, "con"과 "ryan"은 결과 메일을 받지 않습니다. 따라서 [0, 0]을 return 합니다.

### 풀이
```javascript
function solution(idList, report, k) {
    let answer = [];
  	// 유저가 신고당한 횟수를 담을 유저 이름의 객체.
    let reportCount = {};
  	// 신고당한 횟수가 k 보다 많거나 같으면 정지당할 유저의 이름을 담을 배열.
    let stopUsers = [];
  	// 중복신고는 안되니 배열안에 같은값을 정리해줍니다.
    let arrSet = [...new Set(report)];
  	// 한 문자열안에 신고자와 신고당한자가 스페이스바로 나뉘어있어 나눈다음
  	// 배열로 만들어 담을 2차원 배열
    let textArr = [];
  	// reportCount 안에 모든 유저객체를 만들고 그안에 유저가 신고한 유저의 문자열을 담을 배열을 만들어줍니다.
    idList.map((v) => (reportCount[`${v}`] = { report: [] }));
	// 위에서 reportCount 안에 모든유저 객체를 만들어줬으니 객체 안에 해당유저의 신고당한 횟수를 담을 count를 만들어줍니다 초기값은 0으로 설정
    idList.map((v, i) => ((reportCount[`${v}`].count = 0), (answer[i] = 0)));
  	// 이제 신고한유저와 신고당한 유저를 2차원 배열안에 답아줍니다.
  	// 2차원 배열안에 신고한유저는 [0], 신고당한 유저는 [1]로 담아줍니다.
    for (let i = 0; i < arrSet.length; i++) {
      textArr.push(arrSet[i].split(" "));
    }
  	// textArr 를 이용해 신고한유저를 찾고 객체안 배열에 신고당한 유저의 이름을 담아줍니다
    textArr.map((v) => reportCount[v[0]].report.push(v[1]));
  	// 윗줄과 같은 방식으로 신고당한 유저의 객체를 찾고 신고당한 카운트에 횟수를 더해줍니다.
    textArr.map((v) => ++reportCount[v[1]].count);
    // 모든유저 리스트를 이용해 유저 객체속 신고당한 카운트가 k 보다 같거나 높으면 stopUsers배열에 유저 이름을 넣어줍니다.
    idList.map((v) => reportCount[v].count >= k && stopUsers.push(v));
  	// 마지막으로 신고당한 횟수가 k보다 높은사람을 정지시켰으니 신고한사람에게 메일을 보내야하니
	// 모든 유저 리스트를 활용해 reportCount[v].report 안에 정지당한 유저가 있는지 확인하고 
  	// 있으면 idList속 신고자가 있는 index에 메일을 보낼횟수(answer)를 +1을 해줍니다.
    idList.map((v, i) =>
      stopUsers.map(
        (value, index) => reportCount[v].report.includes(value) && ++answer[i]
      )
    );
  return answer;
  }
```

### 후기
> 정신 줄 놓고 풀었더니 쓸데없는 변수가 있고 변수 이름을 막 써버렸네요(stopUsers) 그리고 좀 더 단축해서 풀 수 있었을 텐데 풀고보니 뭔가 아쉽네요.
