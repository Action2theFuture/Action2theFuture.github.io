---
layout: post
title: "MongoDB"
date: 2021-07-14
categories: TIL MongoDB node.js 비동기
---

# NoSQL 데이터베이스

- MongoDB는 동적 스키마형 데이터베이스이다
- 데이터는 Document형태로 하나씩 저장이 된다
- 기존의 관계형데이터베이스와 달리 관계적인 데이터를 추구하기 보다는 다른 종류의 데이터를 쉽고 빠르게 다룰 수 있다

Node.JS와 MongoDB와 연결하기 위해서는 Mongoose 모듈을 이용해야 한다

**ODB(Object Document Modeling) : Modeling Tool**

## Mongoose

#### app.js

```javascript
const mongoose = require("mongoose");

const MONGO_URL = `DB_HOST=mongodb://localhost:27017/`;

// mongodb://username:password@host:port/database?options

mongoose.connect(
  MONGO_URL,
  {
    dbName: "test",
    useNewUrlParser: true,
    useCreateIndex: true,
    useUnifiedTopology: true,
  },
  (error) => {
    if (error) {
      console.log("mongodb connection error", error);
    } else {
      console.log("mongodb connection success");
    }
  }
);

mongoose.connection.on("error", (error) => {
  console.error("mongodb connection error", error);
});

mongoose.connection.on("disconected", () => {
  console.error("mongodb disconnection, restart");
  connect();
});
```

> **Mongoose option**  
> https://mongoosejs.com/docs/connections.html

mongoose를 이용하여 MongoDB가 연결이 되었다

이젠 스키마를 만들어보자

#### ./models/schema.js

```javascript
const mongoose = require("mongoose");
const Schema = mongoose.Schema;

const User = new Schema({
  name: String,
  email: String,
  password: String,
  nickname: String,
});

mongoose.model("User", User);
```

#### ./models/index.js

```javascript
const User = requrie("./schema");

const models = {
  User,
};

module.exports = models;
```

## Statics / Methods

Node.JS로 스키마에 저장되거나 저장된 데이터를 조작을 해보자

```javascript
User.statics.create = function (name, email, password, phonenumber) {
  const user = new this({
    name,
    email,
    password: hash(password),
    nickname: nickname,
  });

  return user.save();
};

module.exports = mongoose.model("User", User);
```

Statics : 해당 모델에 접근
User라는 모델에 Static 함수로 접근하여 스키마를 다룬다

Methods : 데이터 인스턴스에 접근
Client의 요청에 의하여 데이터가 들어오면 원하는 데이터 객체를 다룰 수 있는 함수이다

### Schema 참조

다른 스키마 참조하여 참조된 스키마의 데이터형식을 정할 수 있다

```javascript
const mongoose = require("mongoose");
const Schema = mongoose.Schema;

const Review = new Schema({
  title: String,
  content: String,
  product: { type: mongoose.ObjectId, ref: "Product" },
  user: { type: mongoose.ObjectId, ref: "User" },
});
```

### findOneAndUpdate()

```javascript
.
.
.
try {
        await User.findOneAndUpdate(
            {
                _id: id,
            },
            {
                $set: {
                    profile: profile,
                },
            },
            {
                returnNewDocument: true,
            }
        );
        res.json({ message: "success" });
    } catch (err) {
        res.status(404).json({ message: `${err}` });
    }
.
.
.
try {
      const id = await tokenCheck(token);
      await User.findOneAndUpdate(
           {
               _id: id,
           },
           {
               $addToSet: {
                cartlist: await Product.findOne({ name: name })
               },
           },
           {
               returnNewDocument: true,
           }
        );
            const user = await User.findOne({ _id: id });
            return await Promise.all(
                user.cartlist.map(id => {
                    return Product.findOne({ _id: id });
                })
            );
  // Promise.all()을 이용하여 비동기를 병렬로 처리
        } catch (err) {
            return new ApolloError(err, "404");
        }
.
.
.
try {
      const id = await tokenCheck(token);
      const product = await Product.findOne({ name: name });
      await User.findOneAndUpdate(
          {
              _id: id,
          },
          {
              $pullAll: {cartlist: [product._id]},
          },
          {
              returnNewDocument: true,
          }
         );
            const user = await User.findOne({ _id: id });
            return await Promise.all(
                user.cartlist.map(id => {
                    return Product.findOne({ _id: id });
                })
            );
          } catch (err) {
            return new ApolloError(err, "404");
          }
```

- $addToset : 배열을 추가한다
  - $ each를 추가하여 기존 배열에 중복되지 않는 값을 추가한다
- $pullAll : 기존 배열에서 지정된 값의 모든 인스턴스를 제거한다

> MongoDB 공식문서
> https://docs.mongodb.com/manual/
