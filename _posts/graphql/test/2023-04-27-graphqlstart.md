---
title: "[ React + GraphQL + ApolloServer ] 시작해보기"
author: <author_id>
categories: [ GraphQL,  Study]
tags: [ GraphQL, React,ApolloServer]
math: true
toc: true
mermaid: true
image: /images/backgrounds/graphql.png
---

## Project 에 서버용 디렉토리 추가
1. ### my-project/graphql-server(GraphQL 디렉토리)
2.  ### 티미널로 폴더이동 `cd my-project/graphql-server`
3. ### `graphql-server`디렉토리에 `package.json`추가
    ```
    npm init -y
    ```
4. ### `graphql-server/package.json`스크립트 변경
  ```javascript
  {
    "Before change": "Before change",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },

    "After change": "Before change",
    "scripts": {
      "dev": "nodemon index.jsx"
    }
  }
  ```


## GraphQL 설치(npm, yarn)
```shell
npm install graphql

yarn add graphql
```
## Apollo 라이브러리 설치(npm, yarn)
```shell
npm install apollo-server

yarn add apollo-server
```
## GraphQL + Apollo 한번에 설치(npm, yarn)
```shell
npm install apollo-server graphql

yarn add apollo-server graphql
```

## Apollo 초기설정
+ ### my-project/graphql-server/index.js(생성)
  ```javascript
  const { ApolloServer, gql } = require('apollo-server');
  
  // The GraphQL schema
  const typeDefs = gql`
    type Query {
      "A simple type for getting started!"
      hello: String
    }
  `;
  
  // A map of functions which return data for the schema.
  const resolvers = {
    Query: {
      hello: () => 'world',
    },
  };
  
  const server = new ApolloServer({
    typeDefs,
    resolvers,
  });
  
  server.listen().then(({ url }) => {
    console.log(`🚀 Server ready at ${url}`);
  });
  ```

1. ### 서버 열기
```shell
npm run dev
```
![](https://velog.velcdn.com/images/dltmdwls15/post/db7a82de-d469-42a7-92cb-ac4b5ce7f116/image.png)

2. ### http://localhost:4000/ 접속
![](https://velog.velcdn.com/images/dltmdwls15/post/b0f31058-b5a7-4c52-8461-61f2c9c77a90/image.png)
3. ### Query your server 클릭
![](https://velog.velcdn.com/images/dltmdwls15/post/2090ee3e-63dc-47fa-97ce-dafe68aee8d2/image.png)
4. ### ExampleQuery 클릭 (응답 확인)
![](https://velog.velcdn.com/images/dltmdwls15/post/e206784c-be3a-4969-9a0c-194b6fd1dd9c/image.png)



## typeDef는 무엇인가?
+ ### typeDef
  ```javascript
  const typeDefs = gql`
    type Query {
      hello: String
    }
  `;
  ```
GraphQL에서 사용하는 스키마의 대한 정의를 하는 곳이며 클라이언트에서 GraphQL로
서버에 어떠한 요청을 할 때 어떤 식으로 요청을 하는지에 대한 스키마도 정할 수 있습니다
간단하게 생각하면 GraphQL의 스키마를 정하는곳이다 라고 생각할 수 있습니다.

## resolver는 무엇인가?
+ ### resolver
  ```javascript
  const resolvers = {
    Query: {
      hello: () => 'Hello World',
    },
  };
  ```
  클라이언트에서 GraphQL 로 서버에 어떠한 요청을 할 때 해당 요청의 응답을 작성하는
  곳 입니다. 클라이언트에서 GraphQL로 `typeDef`가 정의한 요청에 알맞게 요청한다면
  `resolvers`는 `"data": { "hello" : "Hello World" } `라는 응답을 하게 됩니다.
  그리고 `typeDef`와 `resolvers`는 한쌍을 이루게 되어 있습니다.
  `typeDef`와 `resolvers`작성한다음 `ApolloServer`에 넣으면 서버가 완성이 됩니다.

  ```javascript
  const server = new ApolloServer({
    typeDefs,
    resolvers,
  });
  ```

## 배운것 정리
+ ### typeDef(s)
  + #### GraphQL의 Schema(스키마)를 정의 하는곳.
    + Object
    + Query
    + Mutation
    + input
  + #### gql 과 template literal 로 작성한다.
    + template literal
      ```javascript
      // React.js 의 styled-components 처럼 
      // 백틱안에 값을 정의하는 방법
      const typeDefs = gql`
        type Query {
          hello: String
      }
      `;
      ```
+ ### resolver(s)
  + #### Schema(스키마)에 해당하는 구현을 하는 곳
  + #### 요청을 받아 데이터를 조회, 수정, 삭제를 하는 곳
