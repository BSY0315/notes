# body-parser에 대하여

## 1. 개요

express 문서에 따르면 미들웨어 없이 **req.body** 에 접근하는 경우에는 기본으로 undefined 가 설정되어 있으므로 **bodyParser, multer**와 같은 미들웨어를 사용하여 요청 데이터 값에 접근해야 한다는 안내를 찾을 수 있다.
클라이언트 측에서 API post 와 put 메소드로 요청시 (get delete 는 불가하다.) body 를 포함하여 보낼 수 있는데 이 값을 서버 측에서 받는다고 그대로 사용할 수 있는 것이 아니고 서버 내에서 해석 가능한 형태로 변형해야 사용할 수 있게 되는 것이다.
이때 API 요청에서 받은 body 값을 파싱하는 역할을 수행하는 것이 bodyParser 라는 미들웨어이다.

> Body-Parser란?  
> **HTTP post put** 요청시 request body 에 들어오는 데이터값을 읽을 수 있는 구문으로 파싱함과 동시에 **req.body** 로 입력해주어 응답 과정에서 요청에 body 프로퍼티를 새로이 쓸 수 있게 해주는 미들웨어.

```js
npm install body-parser

import bodyParser from "body-parser";
```

---

## 2. Methods

```js
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));
```

- **`bodyParser.unlencoded() :`**  
  bodyParser 미들웨어의 여러 옵션 중에 하나로 false 값일 시 node.js에 기본으로 내장된 **queryString**, true 값일 시 따로 설치가 필요한 **npm qs** 라이브러리를 사용한다.

  queryString 과 qs 라이브러리 둘 다 url 쿼리 스트링을 파싱해주는 같은 맥락에 있으나 qs가 추가적인 보안이 가능한 말 그대로 extended 확장된 형태이다

---

## 3. 대체

express 4.16.0 버전에서는 bodyParser가 express에 포함되어 있다.

```js
app.use(exprss.json());
app.use(express.urlencoded({ extended: true }));
```

...와 같이 사용할 수 있다.
