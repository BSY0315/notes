# express-session에 대하여

## 1. 개요

> Express-Session란?  
> express-session 은 Express 프레임워크에서 세션을 관리하기 위해 필요한 미들웨어.

```js
npm install express-session

import session from "express-session";
```

> ### 설정

```js
app.use(
  session({
    secret: "@#@$MYSIGN#@$#$",
    resave: false,
    saveUninitialized: true,
  })
);
```

- secret – 쿠키를 임의로 변조하는것을 방지하기 위한 값 입니다. 이 값을 통하여 세션을 암호화 하여 저장합니다.
- resave – 세션을 언제나 저장할 지 (변경되지 않아도) 정하는 값입니다.  
  express-session documentation에서는 이 값을 false 로 하는것을 권장하고 필요에 따라 true로 설정합니다.
- saveUninitialized – 세션이 저장되기 전에 uninitialized 상태로 미리 만들어서 저장합니다.

---

## 2. 세션 변수 설정

```js
app.get("/login", function (req, res) {
  sess = req.session;
  sess.username = "velopert";
});
```

따로 키를 추가해줄 필요 없이 sess.[키 이름] = 값 으로 세션 변수를 설정 할 수 있습니다.

---

## 3. 세션 제거

```js
req.session.destroy(function (err) {
  // cannot access session here
});
```

`destroy() 메소드의 콜백함수에서는 세션에 접근 할 수 없다.`

---

## 4. 주의사항

**app.use 는 차례차례 체인 형식으로 진행이 된다.**  
따라서, **app.use(app.router)** 앞줄에 **app.use(session)**이 있어야 req.session이 undefined로 뜨지 않는다.
