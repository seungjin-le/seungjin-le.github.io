---
title: "[ JS 코딩테스트 LV2 ] [1차] 뉴스 클러스터링"
author: <author_id>
categories: [CodingTest,Programmers,"LV 2"]
tags: [JavaScript,CodingTest,Programmers,LV_2]
math: true
toc: true
mermaid: true
image: /images/backgrounds/javascript.png
---



### 문제 설명
여러 언론사에서 쏟아지는 뉴스, 특히 속보성 뉴스를 보면 비슷비슷한 제목의 기사가 많아 정작 필요한 기사를 찾기가 어렵다.   
Daum 뉴스의 개발 업무를 맡게 된 신입사원 튜브는 사용자들이 편리하게 다양한 뉴스를 찾아볼 수 있도록 문제점을 개선하는 업무를 맡게 되었다.

개발의 방향을 잡기 위해 튜브는 우선 최근 화제가 되고 있는 "카카오 신입 개발자 공채" 관련 기사를 검색해보았다.

- 카카오 첫 공채..'블라인드' 방식 채용
- 카카오, 합병 후 첫 공채.. 블라인드 전형으로 개발자 채용
- 카카오, 블라인드 전형으로 신입 개발자 공채
- 카카오 공채, 신입 개발자 코딩 능력만 본다
- 카카오, 신입 공채.. "코딩 실력만 본다"
- 카카오 "코딩 능력만으로 2018 신입 개발자 뽑는다"

기사의 제목을 기준으로 "블라인드 전형"에 주목하는 기사와 "코딩 테스트"에 주목하는 기사로 나뉘는 걸 발견했다. 튜브는 이들을 각각 묶어서 보여주면 카카오 공채 관련 기사를 찾아보는 사용자에게 유용할 듯싶었다.

유사한 기사를 묶는 기준을 정하기 위해서 논문과 자료를 조사하던 튜브는 "자카드 유사도"라는 방법을 찾아냈다.

자카드 유사도는 집합 간의 유사도를 검사하는 여러 방법 중의 하나로 알려져 있다. 두 집합 A, B 사이의 자카드 유사도 J(A, B)는 두 집합의 교집합 크기를 두 집합의 합집합 크기로 나눈 값으로 정의된다.

예를 들어 집합 A = {1, 2, 3}, 집합 B = {2, 3, 4}라고 할 때, 교집합 A ∩ B = {2, 3}, 합집합 A ∪ B = {1, 2, 3, 4}이 되므로, 집합 A, B 사이의 자카드 유사도 J(A, B) = 2/4 = 0.5가 된다. 집합 A와 집합 B가 모두 공집합일 경우에는 나눗셈이 정의되지 않으니 따로 J(A, B) = 1로 정의한다.

자카드 유사도는 원소의 중복을 허용하는 다중집합에 대해서 확장할 수 있다. 다중집합 A는 원소 "1"을 3개 가지고 있고, 다중집합 B는 원소 "1"을 5개 가지고 있다고 하자. 이 다중집합의 교집합 A ∩ B는 원소 "1"을 min(3, 5)인 3개, 합집합 A ∪ B는 원소 "1"을 max(3, 5)인 5개 가지게 된다. 다중집합 A = {1, 1, 2, 2, 3}, 다중집합 B = {1, 2, 2, 4, 5}라고 하면, 교집합 A ∩ B = {1, 2, 2}, 합집합 A ∪ B = {1, 1, 2, 2, 3, 4, 5}가 되므로, 자카드 유사도 J(A, B) = 3/7, 약 0.42가 된다.

이를 이용하여 문자열 사이의 유사도를 계산하는데 이용할 수 있다. 문자열 "FRANCE"와 "FRENCH"가 주어졌을 때, 이를 두 글자씩 끊어서 다중집합을 만들 수 있다. 각각 {FR, RA, AN, NC, CE}, {FR, RE, EN, NC, CH}가 되며, 교집합은 {FR, NC}, 합집합은 {FR, RA, AN, NC, CE, RE, EN, CH}가 되므로, 두 문자열 사이의 자카드 유사도 J("FRANCE", "FRENCH") = 2/8 = 0.25가 된다.

### 입력 형식
- 입력으로는 str1과 str2의 두 문자열이 들어온다. 각 문자열의 길이는 2 이상, 1,000 이하이다.
- 입력으로 들어온 문자열은 두 글자씩 끊어서 다중집합의 원소로 만든다. 이때 영문자로 된 글자 쌍만 유효하고, 기타 공백이나 숫자, 특수 문자가 들어있는 경우는 그 글자 쌍을 버린다. 예를 들어 "ab+"가 입력으로 들어오면, "ab"만 다중집합의 원소로 삼고, "b+"는 버린다.
- 다중집합 원소 사이를 비교할 때, 대문자와 소문자의 차이는 무시한다. "AB"와 "Ab", "ab"는 같은 원소로 취급한다.

### 출력 형식
입력으로 들어온 두 문자열의 자카드 유사도를 출력한다. 유사도 값은 0에서 1 사이의 실수이므로, 이를 다루기 쉽도록 65536을 곱한 후에 소수점 아래를 버리고 정수부만 출력한다.

### 예제 입출력

|str1|	str2|	answer|
|:--:|:--:|:--:|
|FRANCE|	french|	16384|
|handshake	|shake hands|	65536|
|aa1+aa2|	AAAA12	|43690|
|E=M*C^2	|e=m*c^2	|65536|

### 풀이

```javascript
 const solution = (str1, str2) => {
    // 리턴할때  (교집합 / 합집합)에 곱할 변수
    let answer = 65536;
    // 문자열에서 공백, 숫자, 특수문자를 제거할 정규식 변수
    const regExp = /[0-9\{\}\[\]\/?.,;:|\)*~`!^\-_+<>@\#$%&\\\=\(\'\" ]/g;
    // 문자열을 나눈 배열, 교집합, 합집합을 담을 객체
    let obj = {
      a: [], // str1
      b: [], // str2
      empty: [],
      sum: [],
    };

    // str1과 str2중 길이가 더 긴 갚을 변수에 저장
    let len = (str1.length < str2.length ? str2.length : str1.length) - 1;

    // len만큼 반복문 실행
    for (let a = 0; a < len; a++) {
      // 문자열 str1과 str2를 a부터 a + 2까지 잘라서 배열로 치환한다음 순회 ex) [str1 = "FR", str2 = "fr" ]
      [str1.slice(a, a + 2), str2.slice(a, a + 2)].map((v, i) => {
        // 정규식으로 v에서 공백, 숫자, 특수문자를 삭제후 길이가 2라면
        v.replace(regExp, '').length === 2 &&
          // i는 길이가 2인 배열이라서 Object.keys 함수를 이용해 obj.a이나 obj.b에 대문자로 치환해서 추가해줍니다
          // Object.keys(obj)[i]는 i = 0 => obj.a, i = 1 => obj.b를 가리킵니다.
          obj[Object.keys(obj)[i]].push(v.toUpperCase());
      });
    }

    // obj.a와 obj.b가 둘다 빈 값이거나 같으면 answer리턴
    if (JSON.stringify(obj.a) === JSON.stringify(obj.b)) return answer;

    // 반복 횟수를 줄이기 위해 obj.a와 obj.b중 짧은 배열을 순회
    obj.empty.push(
      ...(obj.a.length <= obj.b.length
        ? obj.a.map((x) => {
            if (obj.b.includes(x))
              // obj.a의 요소( x )가 obj.b에 같은 값이 있다면 obj.b에서 x의 첫 번째 인덱스를 찾아 obj.empty 안에 넣어줍니다.
              // 이렇게 되면 obj.a와 obj.b의 중복 값은 obj.empty에 추가됩니다.
              // splice 함수로 잘라낸 요소는 배열로 반환되기 때문에 join을 해주지 않으면 obj.empty는 이차원 배열이 됩니다.
              return obj.b.splice(obj.b.indexOf(x), 1).join('');
          })
        : obj.b.map((x) => {
            // obj.a와 obj.b의 위치만 바뀌고 위 코드와 같습니다.
            if (obj.a.includes(x))
              return obj.a.splice(obj.a.indexOf(x), 1).join('');
          })
      )
        // 조건문에 적합하지 않으면 obj.empty 안에 false 값이 들어가니 filter 함수로 제거
        .filter((v) => v)
    );

    // 합집합은 중복을제거한 obj.a와 obj.b를 합치면 됩니다,
    obj.sum.push(...obj.a, ...obj.b);
   
   
    // 위 과정을 거치고 나면 obj값은 이렇게 됩니다.

    // str1 = "FRANCE", str2 = "french"
    // obj = {
    //   a: [ 'FR', 'RA', 'AN', 'NC', 'CE' ],
    //   b: [ 'RE', 'EN', 'CH' ],
    //   empty: [ 'FR' , 'NC' ],
    //   sum: [
    //     'FR', 'RA', 'AN',
    //     'NC', 'CE', 'RE',
    //     'EN', 'CH'
    //   ]
    // }
    return Math.floor((obj.empty.length / obj.sum.length) * answer);
  };
```
