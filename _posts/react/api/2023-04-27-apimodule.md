---
title: "[ React ] API 모듈화"
author: <author_id>
categories: [ React,  "REST API"]
tags: [ React, API,"REST API"]
math: true
toc: true
mermaid: true
image: /images/backgrounds/react.png
---

### API를 모듈화 하는 이유
>API 관련 코드를 모듈화 하는것은 API관리를 위한 행위로
>이렇게 나누는 이유는 프로젝트의 구조를 좀더 깔끔하게 만들고 코드의 유지보수와
>재사용성을 향상시키며 가독성을 높이는데 도움이 됩니다.

### Axios Install
>시작하기에 앞서 먼저 `React`에서 `api`를 요청할때 가장 많이 사용하는
>`Axios`를 설치합니다.
>
>"Axios를 사용하는 이유는 API 요청을 쉽게 관리할 수 있고 인기가 많아서 에러 발생 시 정보를 쉽게 찾을 수 있습니다. 또한 Promise 기반의 API를 제공하여 비동기 요청을 쉽게 처리할 수 있습니다.
>
>요청 및 응답 인터셉터를 사용하여 요청 전/후에 커스텀 로직을 적용하면 모듈화를 더욱 쉽게 할 수 있습니다."
>#### npm
>```shell
>npm install axios
>```
>
>#### yarn
>```shell
>yarn add axios
>```

### src/dataManager/apiConfig.js 생성
> 이 파일은 API 호출에 필요한 설정을 저장하고 관리하는 파일입니다. 여기에서는 기본 URL, 헤더, 인증 토큰 등과 같은 공통 요소를 설정할 수 있습니다. 
> 
>이렇게 하면 나중에 API 관련 설정을 변경해야 할 때 한 곳에서만 수정하면 됩니다.
> 
> 
> 디렉토리 이름을 `dataManager`로 하지않고 `api`나 `services`등으로
> 하셔도 무관합니다.
> 


```javascript
import Axios from 'axios'
import {isEmpty} from '../utils/utility'

// API 요청 메소드
export const HttpMethod = {
  GET: 'get',
  POST: 'post',
  PUT: 'put',
  PATCH: 'patch',
  DELETE: "delete",
}


export default class ApiConfig {
  // 사용자가 입력한 매개변수를 기반으로 실제 HTTP 요청을 보내는 함수이며
  // 매개변수를 구조분해 할당으로 data, query, path, method, url을 받습니다
  static request({data, query, path, method, url}) {
    try {
      // 조건문을 통해 메소드와 URL이 비어있는지 확인후 둘중 하나라도 값이 없다면 조건문 실행
      if (isEmpty(method) || isEmpty(url)) {
        // 만약 비어 있다면, 경고 메시지를 표시하고 함수를 종료
        return alert('HTTP Method 와 URL 을 확인해주세요.')
      }
      
      // 조건문을 통해 path에 값이 있는지 확인후 값이 있어야만 실행
      if (path) {
        // path의 key값과 value값을분리해 url의 경로 매개변수(Path Parameter)를
        // path의 value값으로 변경해줍니다.
        
        // ex) url = "users/:id", path = { id: 24} 반복문 종료후 => url = "users/24"
        for (const [key, value] of Object.entries(path)) {
          url = url.replace(`:${key}`, value)
        }
      }

      // 조건문을 통해 query에 값이 있는지 확인후 값이 있어야만 실행
      if (!isEmpty(query)) {
        // query를 순회 하면서 key값과 value값 중간에 " = "을 합쳐 쿼리 문자열을 생성
        // 이렇게 합쳐진 쿼리 문자열 앞에 " ? "를 붙여 url 뒤부분에 추가
        
        // ex) query = { age: "11", gender: "male" }
        // ex) url = "users" map함수 종료후 => url = "users?age=11&gender=male"
        url += '?' + Object.keys(query)
            .map(key => key + '=' + query[key])
            .join('&')
      }

      // 클라이언트와 서버간에 메타데이터를 교환할때 사용될 객체
      const headers = {
        // 클라이언트가 서버로부터 받는 MIME 타입을 지정합니다.
        accept: 'application/json',
        // 클라이언트가 서버에 보내는 데이터의 MIME 타입을 지정합니다.
        'Content-Type': 'application/json',
        // 사용자 인증을 위한 커스텀 토큰 헤더이며 브라우저에 저장된 'jwt'라는 토큰 값을
        // 가져와 서버에서 사용자 인증 및 권한 검사를 하는데 데 사용됩니다.
        'X-Access-Token': window.sessionStorage.getItem('jwt'),
      }

      // 조건문을 통해 메소드에 따른 API요청
      switch (method) {
        // method가 "get"일경우 
        case HttpMethod.GET:
          // GET 메소드를 이용해 데이터를 서버에 요청 
          return Axios.get(url, {headers: headers})
        // method가 "post"일경우
        case HttpMethod.POST:
          // 특정 데이터를 보내 데이터 생성.
          return Axios.post(url, data, {headers: headers})
        // method가 "patch"일경우
        case HttpMethod.PATCH:
          // 특정 데이터를 보내 데이터 일부분 수정.
          return Axios.patch(url, data, {headers: headers})
        // method가 "put"일경우
        case HttpMethod.PUT:
          // 특정 데이터를 보내 데이터 대체.
          return Axios.put(url, data, {headers: headers})
        // method가 "delete"일경우
        case HttpMethod.DELETE:
          // 특정 데이터를 보내 데이터 삭제.
          return Axios.delete(url, data, {headers: headers})
        default:
          break
      }
    } catch (error) {
      // 잘못된 요청일경우 에러를 출력합니다
      alert(error.message)
    }
  }
}

```

### src/dataManager/apiMapper.js 생성
> 이 파일은 API 엔드포인트를 저장하고 관리하기 위한 파일이며. 
> 이를 통해 API를 호출할 때 API 엔드포인트를 참조하고 업데이트할 수 있으며,
> 코드의 가독성과 유지 보수성이 향상됩니다.

```javascript
// 환경 변수에서 API Key나 주소를 가져옵니다
const API = process.env.REACT_APP_API

// API 엔드포인트를 정의합니다
export const EndPoint = {
  GET_USERS: `${API}/users`,
}

// HTTP의 각 메서드에 따른 API 엔드포인트를 관리합니다.
const ApiMapper = {
  get: {
    [EndPoint.GET_USERS]: {},
  },
  post: {},
  patch: {},
  put: {},
  delete: {},
}

export default ApiMapper

```

