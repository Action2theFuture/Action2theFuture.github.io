---
layout: post
title: "GraphQL"
date: 2021-07-14
categories: TIL RESTfulAPI apollo-server-express GraphQL node.js
---

# GraphQL

![](https://images.velog.io/images/action2thefuture/post/bf39e89c-7aa4-46f2-a7ba-e40613b9210d/graphql.png)

페이스북이 개발한 데이터 질의어이다
주로 사용하던 RestfulAPI와 달리 클라이언트가 원하는 데이터 구조를 정할 수 있고 서버에서는 동일한 구조로 응답을 한다
엔드포인트는 하나로 정해져있다
이러한 장점으로 인해 불필요한 데이터를 줄여 서버낭비를 방지할 수 있고 원하는 데이터를 받으면서 로딩시간을 줄여서 비교적 빠르게 페이지를 나타낼 수 있다

서버 단에 의존적이지 않는 클라이언트 부분과 상호작용을 하여서 좀 더 유연한 데이터 구조를 만들 수 있다

웹과 앱을 동시에 개발해야하는 환경에서 각 클라이언트마다 새로 API를 만들 필요없이 하나의 엔드포인트로 그 환경에 맞춰 데이터를 제공할 수 있다

GraphQL는 json으로 응답이 된다

GraphQL의 대표적인 클라이언트인 Apollo가 있다

## GraphQL Architecture Diagram

![](https://images.velog.io/images/action2thefuture/post/8b1c134e-08dd-4d06-adef-b629ce6386f6/graphql.png)

## PlayGround

![](https://images.velog.io/images/action2thefuture/post/9d939065-973f-48f1-9379-a40559d5a739/playground.png)

## GraphQL Server

apollo-server-express를 통하여 GraphQL Server를 구동하였다
server.applyMiddleware로 express 서버에 api를 추가하였다

```javascript
const express          = require("express");
const { ApolloServer } = require("apollo-server-express");

const typeDefs  = require("./models/schema");
const resolvers = require("./resolvers");

const app = express();

const port = process.env.PORT || 5000;
const host = process.env.HOST || "0.0.0.0";

app.use(express.urlencoded({ extended: false }));
app.use(express.json());

const server = new ApolloServer({
    typeDefs,
  // 모델의 스키마
    resolvers,
  // 리졸브
    context: ({ req }) => {
        const token = req.headers.authorization;
            return { token };
        }
    },
  // 요청의 전처리를 context로 받는다
});

server.applyMiddleware({ app, path: "/graphql" });
app.listen({ port, host }),
    async () => {
        try {
            await console.log(
                `GraphQL is running on port ${port}${server.graphqlPath}`
            );
        } catch (err) {
            await console.log(err);
        }
    };
```

### models/schema.js

schema.js 응답받은 데이터들을 결정한다

```javascript
const { gql } = require("apollo-server-express");

module.exports = gql`
  type User {
    id: ID!
    name: String
    email: String
    password: String
    phonenumber: String
  }
  type Query {
    showUser: User!
  }
  type Mutation {
    signUp(
      name: String!
      email: String!
      password: String!
      phonenumber: String!
    ): User!
  }
`;
```

### Query

context로 요청의 헤더값을 전달받을 수 있다

```javascript
const { ApolloError } = require("apollo-server-errors");

const User = require("../models/user");
const { tokenCheck } = require("../util");

module.exports = {
  showUser: async (_, __, { token }) => {
    // context로 들어온 token값
    if (!token) return new ApolloError("not login", "404");
    try {
      const id = await tokenCheck(token);
      return await User.findOne({
        _id: id,
      });
    } catch (err) {
      return new ApolloError(err, "404");
    }
  },
};
```

#### ApolloError

Apollo의 에러를 커스터마이징이 가능하도록 해준다
첫번째 인자값은 에러 내용, 두번째 에러 코드, 세번째 인자는 추가 옵션을 줄 수 있다

### Mutation

```javascript
const { ApolloError } = require("apollo-server-errors");
const User = require("../models/user");

module.exports = {
  signUp: async (_, args) => {
    const { name, email, password, phonenumber } = args;
    let user = null;
    try {
      user = await User.create(name, email, password, phonenumber);
      return user;
    } catch (err) {
      return new ApolloError(err, "404");
    }
  },
};
```

### resolvers/index.js

```javascript
const Query = require("./query");
const Mutation = require("./mutation");

module.exports = {
  Query,
  Mutation,
};
```
