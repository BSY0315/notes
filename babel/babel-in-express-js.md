# Express에서 ES6 문법 사용을 위한 babel 적용

## 1. Babel이란?

> Babel은 ECMAScript 최신 문법으로 작성된 코드들을 구버전의 브라우저에서도 실행할 수 있게끔 변환해주는 트랜스파일러이다. 특히 개발하는 서비스가 구버전의 IE를 지원해야하는 경우 Babel을 이용한 호환성 확장은 필수적이다. 또한 Babel은 최신 문법 변환 외에도 다양하게 사용될 수 있는데, 리액트의 JSX 문법 또한 Babel이 createElement 함수를 사용한 리액트 코드로 변환시켜 준다.

## 2. 설치

```
npm i @babel/cli @babel/core @babel/node @babel/preset-env babel-loader @babel/polyfill -D
```

- **@babel/core** : 바벨을 사용하기위해 필수적으로 설치해야한다.

- **@babel/cli** : command line을 통해 코드를 transpile 할 수 있게 만들어준다.  
  `npx babel index.js`

- **@babel/node** : ES6로 작성된 노드 코드를 실행하는 기능을 갖고있다. (프로덕션 에서 사용시, 그때그때 마다 앱을 컴파일 하게되고 이는 성능 저하를 불러오기때문에, 개발 및 테스트 과정에서만 사용해야 한다.)  
  `npx babel --presets @babel/env index.js | node` 와 같다고 할 수 있다.

- **@babel/preset-env** : 프리셋을 통해 간편하게 바벨의 트랜스 파일링 설정을 해줄 수 있는데, env는 가장 범용적으로 사용되는 프리셋이다.  
  프리셋 설정을 해주어야만 어떻게 변화될지 결정할 수 있다.  
  `npx babel --presets @babel/env index.js`

- **babel-loader** : webpack이 .js 파일들에 대해 babel을 실행하도록 만들어준다.

- **@babel/polyfill** : babel은 기본적으로 es6로 작성한 코드를 es5 환경에서 동작할 수 있도록 변환을 해주지만 애초부터 es5에 존재하지 않는 es6의 메서드나 생성자들까지 지원하지는 않기 때문에 이를 해결하기 위한 패키지이다.

## 3. 실행

바벨 커맨드를 실행할 때마다 매번 프리셋 옵션을 붙이기 번거롭다면 바벨 설정파일인 **.babelrc**을 프로잭트 최상위 디렉토리에 만들자.
혹은 **package.json**에 추가하는여도 된다.

- .babelrc

```json
{
  "presets": ["@babel/env"]
}
```

- package.json

```json
  "devDependencies": {
    "@babel/cli": "^7.10.4",
    "@babel/core": "^7.10.4",
    "@babel/node": "^7.10.4",
    "@babel/preset-env": "^7.10.4"
  },
+  "babel": {
+    "presets": ["@babel/env"]
+  },

```

> +Tip. **nodemon**과 조합하여 사용하자

```json
"scripts": {
    "start" : "nodemon index.js --exec babel-node"
}
```
