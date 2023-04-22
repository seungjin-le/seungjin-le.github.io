---
title: "[ JS 코딩테스트 ] 문자열 나누기"
author: <author_id>
categories: [CodingTest,Programmers]
tags: [JavaScript,CodingTest,Programmers,LV_1]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---

### 문제 설명
문자열 s가 입력되었을 때 다음 규칙을 따라서 이 문자열을 여러 문자열로 분해하려고 합니다.

- 먼저 첫 글자를 읽습니다. 이 글자를 x라고 합시다.
- 이제 이 문자열을 왼쪽에서 오른쪽으로 읽어나가면서, x와 x가 아닌 다른 글자들이 나온 횟수를 각각 셉니다. 처음으로 두 횟수가 같아지는 순간 멈추고, 지금까지 읽은 문자열을 분리합니다.
- s에서 분리한 문자열을 빼고 남은 부분에 대해서 이 과정을 반복합니다. 남은 부분이 없다면 종료합니다.
- 만약 두 횟수가 다른 상태에서 더 이상 읽을 글자가 없다면, 역시 지금까지 읽은 문자열을 분리하고, 종료합니다.
- 문자열 s가 매개변수로 주어질 때, 위 과정과 같이 문자열들로 분해하고, 분해한 문자열의 개수를 return 하는 함수 solution을 완성하세요.

### 제한사항
- 1 ≤ s의 길이 ≤ 10,000
- s는 영어 소문자로만 이루어져 있습니다.

### 입출력 예

|s|	result|
|:--:|:--:|
|"banana"	|3|
|"abracadabra"|	6|
|"aaabbaccccabba"	|3|

### 입출력 예 설명
#### 입출력 예 #1
- s="banana"인 경우 ba - na - na와 같이 분해됩니다.

#### 입출력 예 #2
- s="abracadabra"인 경우 ab - ra - ca - da - br - a와 같이 분해됩니다.

#### 입출력 예 #3
- s="aaabbaccccabba"인 경우 aaabbacc - ccab - ba와 같이 분해됩니다.

### 풀이

```jsx
 const solution = (s) => {
    // 문자열을 나눈 횟수 카운트할 변수
    let answer = 0;

    // 문자열의 첫 번째 문자와 그렇지 않은 문자를 카운트해야 하기 때문에
    // sum은 문자열의 첫 번째 문자와 다른 문자를 카운트
    let obj = { sum: 0 };

    // 문자열 s를 배열로 치환하고 map 함수로 배열을 순회
    s.split('').map((v) => {
      // obj의 길이가 1이라면 s의 요소인 v라는 단어를 obj에 추가 후
      // return을 통해서 다음 순서로 진행
      if (Object.keys(obj).length === 1) return (obj[v] = 1);

      // 바로 위 조건문을 통해서 v라는 단어를 추가했기 때문에
      // obj 안에 v라는 단어가 있으면 obj[v] + 1
      // obj 안에 v라는 단어가 없으면 obj.sum + 1
      obj.hasOwnProperty(v) ? obj[v]++ : obj.sum++;

      // obj를 순회하면서 key가 sum이 아니고 obj.sum과 값이 같으면
      // answer++, obj를 초기화
      // obj를 초기화하면 obj의 길이는 다시 1이 되고
      // 첫 번째 조건문에서 obj의 길이가 1이라면
      // 해당 단어가 첫 번째 단어로 추가됩니다.
      Object.keys(obj).forEach((key) => {
        if (key !== 'sum' && obj[key] === obj.sum) {
          answer++;
          return (obj = { sum: 0 });
        }
      });
    });
    // obj의 길이가 1보다 크다면 answer + 1, 1보다 작거나 같으면 answer 리턴
    return Object.keys(obj).length > 1 ? answer + 1 : answer;
  };
```
#### s.map() 을 통해서 추가될 obj의 순서
- 문자열 `s = aaabbaccccabba`를 에시로 들어서

>
>`obj = { sum: 0 }, v = a` :  map 함수 안에 첫 번째 조건문에서 obj의 길이가 1이라면 obj에 a 변수 추가
>
>`obj = { sum: 0, a: 1 }, v = a` : 두 번째 조건 문인  obj.hasOwnProperty(v)에서 obj 안에 v라는
> key가 있다면 obj[v]를 카운트, v라는 key가 없다면 obj.sum 카운트 그 후 Object.keys 함수를 통해
> obj를 순회하면서 key는 sum이 아니면서 obj[key]의 값이 obj.sum의 값과 같은지 확인 후 조건에 해당되지
> 않는다면 그대로 반복문 종료
>
>`obj = { sum: 0, a: 2 }, v = a` : 다시 obj[v] 카운트 후 Object.keys 함수를 통해서 값 비교
>
>`obj = { sum: 0, a: 3 }, v = a` : ~~~
>
>`obj = { sum: 1, a: 3 }, v = b` : map 함수 안에 첫 번째 조건문에서 obj의 길이는 2이기 때문에 통과 후
> 2번째 조건문에서 obj 안에 b라는 단어가 없으므로 obj.sum 카운트
>
>`obj = { sum: 2, a: 3 }, v = b` : ~~~
>
>`obj = { sum: 2, a: 4 }, v = a` : ~~~
>
>`obj = { sum: 3, a: 4 }, v = c` : obj 안에 c라는 단어도 없으므로 obj.sum 카운트
>
>`obj = { sum: 4, a: 4 }, v = c` : obj.sum을 카운트해서 obj 안에 두값이 같아졌으므로
> Object.keys 반복문 안에 조건문에 해당됩니다, 조건문을 통과했으니
> 문자열을 자른 횟수인 answer을 카운트하고 obj를 초기화
>
>`obj = { sum: 0, c: 1 }, v = c` : obj를 초기화했으니 obj의 길이는 다시 1이 되고
> 해당 단어는 문자열을 자른 후 첫 번째 문자이기 때문에 첫 번째 조건문에서 obj에 c라는 변수를
> 추가해 줍니다.
>
>`obj = { sum: 0, c: 2 }, v = c` : obj 안에 c라는 변수가 있으므로 obj[v] 카운트
>
>`obj = { sum: 1, c: 2 }, v = a` : 처음과 달리 obj 안에 a라는 변수가 없으므로 obj.sum 카운트
>
>`obj = { sum: 2, c: 2 }, v = b` : obj 안에 b라는 단어가 없으니 obj.sum 카운트 후
> Object.keys 반복문 안에 조건문을 통해 answer을 카운트 후 obj 초기화
>
>`obj = { sum: 1 }, v = b` : 다시 첫 번째 단어로 b 추가
>
>`obj = { sum: 1, b: 1 }, v = a` : obj.sum 카운트 후 Object.keys를 통해 answer 카운트
>
> map 함수가 끝난 후 obj 안에 sum 말고 다른 key가 있다면 문자열을 자르고 나머지가 있다는
> 뜻이므로 return 할 때 obj의 길이가 1보다 크다면 answer + 1을 return
