---
title: "[ JS 코딩테스트 LV2 ] 방문 길이"
author: <author_id>
categories: [CodingTest,Programmers,"LV 2"]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---


### 문제 설명
게임 캐릭터를 4가지 명령어를 통해 움직이려 합니다. 명령어는 다음과 같습니다.

- #### `U: 위쪽으로 한 칸 가기`
- #### `D: 아래쪽으로 한 칸 가기`
- #### `R: 오른쪽으로 한 칸 가기`
- #### `L: 왼쪽으로 한 칸 가기`

캐릭터는 좌표평면의 (0, 0) 위치에서 시작합니다. 좌표평면의 경계는 왼쪽 위(-5, 5), 왼쪽 아래(-5, -5), 오른쪽 위(5, 5), 오른쪽 아래(5, -5)로 이루어져 있습니다.

![](https://velog.velcdn.com/images/dltmdwls15/post/86ec18aa-7cd6-4de2-9359-8447ad1ee489/image.png){: .normal }



- 예를 들어, "ULURRDLLU"로 명령했다면

![](https://velog.velcdn.com/images/dltmdwls15/post/ffea6502-62a4-4a11-992a-97382e53549c/image.png){: .normal }



- 1번 명령어부터 7번 명령어까지 다음과 같이 움직입니다.

![](https://velog.velcdn.com/images/dltmdwls15/post/40eb8e9b-b2e2-4073-9707-b3cdb287de5a/image.png){: .normal }



- 8번 명령어부터 9번 명령어까지 다음과 같이 움직입니다.

![](https://velog.velcdn.com/images/dltmdwls15/post/d7303fe9-ee4b-4ebc-a571-d13a88e26503/image.png){: .normal }


이때, 우리는 게임 캐릭터가 지나간 길 중 캐릭터가 처음 걸어본 길의 길이를 구하려고 합니다. 예를 들어 위의 예시에서 게임 캐릭터가 움직인 길이는 9이지만, 캐릭터가 처음 걸어본 길의 길이는 7이 됩니다. (8, 9번 명령어에서 움직인 길은 2, 3번 명령어에서 이미 거쳐 간 길입니다)

단, 좌표평면의 경계를 넘어가는 명령어는 무시합니다.


예를 들어, "LULLLLLLU"로 명령했다면

![](https://velog.velcdn.com/images/dltmdwls15/post/81f481b8-8908-4fc4-ae38-217542590f28/image.png){: .normal }


- 1번 명령어부터 6번 명령어대로 움직인 후, 7, 8번 명령어는 무시합니다. 다시 9번 명령어대로 움직입니다.

![](https://velog.velcdn.com/images/dltmdwls15/post/64d53530-c127-4817-9381-158db2898aec/image.png){: .normal }


이때 캐릭터가 처음 걸어본 길의 길이는 7이 됩니다.

명령어가 매개변수 dirs로 주어질 때, 게임 캐릭터가 처음 걸어본 길의 길이를 구하여 return 하는 solution 함수를 완성해 주세요.

### 제한사항
- `dirs`는 `string`형으로 주어지며, `'U', 'D', 'R', 'L'` 이외에 문자는 주어지지 않습니다.
- `dirs`의 길이는 `500 이하의 자연수`입니다.

### 입출력 예

|dirs|	answer|
|:--:|:--:|
|"ULURRDLLU"	|7|
|"LULLLLLLU"	|7|

### 입출력 예 설명
#### 입출력 예 #1
- 문제의 예시와 같습니다.

#### 입출력 예 #2
- 문제의 예시와 같습니다.


### 풀이

```javascript
const solution = (dirs) => {
    // 캐릭터가 이동한 위치를 담을 이차원 배열
    // arr의 요소인 배열은 캐릭터의 현제 위치,
    // ex ) [  X : 0, Y : 0 ]
    let arr = [[0, 0]];
    // 캐릭터가 움직임 길을 저장할 객체
    let obj = {
      x: [],
      y: [],
    };

    // 캐릭터가 지나간 좌표를 저장
    // ex ) 캐릭터가 위로 움직 였다면 X 축은 변화가 없기때문에
    // pos = [ 캐릭터가 이동해도 변화가 없는 위치( x ) ], line = [ 캐릭터가 이동하기전 위치( y ), 이동한 후 위치( y ) ]
    const str = (pos, line) => {
      // 한번 지나간 길은 다시 지나가도 카운트되지 않기 때문에
      // 이동한 길을 오름차순으로 정렬후 JSON문자열로 치환
      // ex ) [ x, (y = 0) => (y = 1) ]
      // ex ) [ y, (x = 0) => (x = 1)  ]
      return JSON.stringify([pos, ...line.sort((a, b) => a - b)]);
    };

    // 캐릭터의 이동 명령어인 문자열을 배열로 치환하여 순회
    dirs.split('').map((v) => {
      // 캐릭터의 현제 위치인 arr의 마지막 요소를 변수에 추가
      let start = arr[arr.length - 1];

      // 캐릭터가 이동한 위치를 담을 배열
      let end = [...start];

      // 이동명령어 배열의 요소인 v가 "U" 이고
      // 캐릭터의 현제 위치인 start의 Y좌표인 2번째 값이 5보다 작으면
      // end의 2번째값 + 1
      // ex ) start = [ X, Y ], end = [ X, Y + 1 ]
      if (v === 'U' && start[1] < 5) end[1]++;

      // end의 2번째 값 - 1
      // ex) start = [ X, Y ], end = [ X, Y - 1 ]
      if (v === 'D' && start[1] > -5) end[1]--;

      // end의 1번째 값 - 1
      // ex) start = [ X, Y ], end = [ X - 1, Y ]
      if (v === 'L' && start[0] > -5) end[0]--;

      // end의 1번째 값 + 1
      // ex) start = [ X, Y ], end = [ X + 1, Y ]
      if (v === 'R' && start[0] < 5) end[0]++;

      // 이동하기전 캐릭터의 위치와 이동한후 캐릭터의 위치가 같으면
      // 반복문 다음 순번으로 넘어감
      if (JSON.stringify(start) === JSON.stringify(end)) return null;

      // v가 "U"나 "D"라면 캐릭터가 Y축으로 움직인거니
      if (v === 'U' || v === 'D') {
        // str 함수를 이용해 JSON 문자열로 치환
        // ex) line = "X, Y(캐릭터가 이동하기 전 위치), Y(캐릭터가 이동한 위치)"
        const line = str(start[0], [start[1], end[1]]);

        // 캐릭터가 한번 지나간 길은 다시 지나가도 이동 횟수를 카운트하지 않으니
        // 이동한 Y 축을 str 함수로 오름차순으로 정렬 후
        // obj.x에 line라는 문자열이 있는지 확인 후
        // line랑 같은 값이 없다면 obj.x에 line 푸시
        !obj.x.includes(line) && obj.x.push(line);
      }

      // v가 "L"나 "R"라면 캐릭터가 X축으로 움직인 거니
      if (v === 'L' || v === 'R') {
        // ex) line = "Y, X(캐릭터가 이동하기 전 위치), X(캐릭터가 이동한 위치)"
        const line = str(start[1], [start[0], end[0]]);
        !obj.y.includes(line) && obj.y.push(line);
      }

      // 캐릭터가 이동한 후의 위치를 arr에 푸시
      arr.push(end);
    });

	// ex ) 테스트 문제 1번을 예시로 보면
    // obj = {
    //   x: [ '[ X(0), Y(0), Y(1)]', '[-1,1,2]', '[1,1,2]' ],
    //   y: [ '[ Y(1), X(-1), X(0)]', '[2,-1,0]', '[2,0,1]', '[1,0,1]' ]
    // }
  	//
    // arr = 	[
    //   [ X(0), Y(0) ],  [ 0, 1 ],
    //   [ -1, 1 ], [ -1, 2 ],
    //   [ 0, 2 ],  [ 1, 2 ],
    //   [ 1, 1 ],  [ 0, 1 ],
    //   [ -1, 1 ], [ -1, 2 ]
    // ]  
  
    // 반복문을 거치면서 캐릭터가 이동한 위치의 중복을 제거했으니
    // 캐릭터가 처음 지나간 길의 길이는 obj.x와 obj.y의 길이를 더하면 됩니다
    return obj.x.length + obj.y.length;
  };
```
