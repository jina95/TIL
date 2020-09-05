# ReactJS로 영화 웹 서비스 만들기 💻 

## 1️⃣
### 🖥 SETUP - 1
#### 1 - 0. Creating your first React App 
- react 프로젝트 생성

<pre><code>$ npx create-react-app movie_app(프로젝트이름)</code></pre>

- README.md 파일 수정 > yarn lock 파일 삭제 > package.json 에 파일 내용 수정

```javascript
"scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build"
  },
```

- 서버를 띄울때 npm start -> local / On Your Network ( 테스트하고싶을때, 핸드폰이나 다른환경 같은와이파이를 사용할때 접속 가능 )

#### 1 - 1. Creating a Github Repository
- 기존 프로젝트 생성 폴더 -> $ git init
- new repo 생성 -> 주소 복사
- 기존 프로젝트 생성 폴더 터미널 -> $ git remote add origin https://github.com/jina95/movieApp_react.git(주소)
- add & commit & push ( $ git push origin master)

> 이때 입력하라는 username 은 내 아이디(spzn02)가 아닌 이름(jina95)

- 이렇게 하면 기존 깃허브 데스크탑을 이용해서 폴더를 이동하지 않아도 가능하다!!

#### 1 - 2. How does React work? 
- react : 사용되는 모든 요소를 생성한다. js 로 만들고 html 로 밀어 넣는다
- 모든 어플리케이션을 react public / index.js -> <div id="root"></div> 안에 넣는다.

```javascript
// src/index.js 
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);

// publice/index.html
<div id="root"></div>

// 만약 이 둘중 하나의 이름만 바꾸게 된다면 에러가 뜬다. root를 찾아서 그 안에 app.js 에 내용을 넣어줌 

```

- react는 virtual Dom을 만들어 냄 (가상돔)

### 🖥 SX & PROPS - 2
#### 2 - 0. Creating your first React Component
- 컴포넌트란 ?  html을 반환하는 함수

```javascript
// src/index.js 
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```

- 컴포넌트를 사용하고자할때 컴포넌트의 형태 👆
- 이러한 자바스크립트와 html 사이의 조합을 jsx라고 한다. ( react에 특화된 개념)
- 컴포넌트를 생성 후

```javascript
// 리액트는 하나의 컴포넌트만 랜더링 할 수 있어서, 아래와 같은 경우는 ❌ / App 안에 넣어줘야 한다.
ReactDOM.render(
  <React.StrictMode>
    <App /><Potato />
  </React.StrictMode>,
  document.getElementById("root")
);
```

```javascript
// App 안에 이런식으로 넣어주면 작동 ⭕️
import React from 'react';
import Potato from "./Potato";

function App() {
  return (
    <div>
      <h1>Hello</h1>
      <Potato></Potato>
    </div>
  );
}

export default App;

```

- **리액트는 하나의 컴포넌트만 랜더링 할 수 있다**

#### 2 - 1. Reusable Components with JSX + Props

- 상위에서 -> 하위 컴포넌트로 정보를 전달하고 그 하위컴포넌트에서 어떻게 정보를 사용할까 ?

```javascript
<Food fav="Kimchi" />
    {/* jsx 방식 */}
```

- 위와 같은 방식으로 정보를 상위에서 하위로 보내줄 수 있다. 
- prop(fav) = property(kimchi) 
- react masic 에서 전달한 props를 가져오는 일을 할 수 있다.
- fav="Kimchi" 처럼 string 만 가능한 것이 아닌, blooean, array 도 가능 

```javascript
import React from 'react';

function Food(props) {
  console.log(props);
  //전달 객체가 많더라도 하나의 props 로 받아올 수 있다.
  // 하나의 오브젝트 형식으로 받아오는데 props.fav / props.papap 등으로 확인할 수 있다
  // 또한 아예 인자값으로 {fav} 를 이용하면 props.fav 를 사용하지 않고 바로 접근 가능 (es6) 
  
  return <h3>I love skarsgard</h3>;
}

function App() {
  return (
    <div>
      <h1>Hello</h1>
      <Food fav="Kimchi" papap={true} something={['1','2','3',true]} />
      {/* jsx 방식 */}
    </div>
  );
}

export default App;
```

#### 2 - 2. Dynamic Component Generation
- map 함수를 이용하여 반복시켜준다.

```javascript
import React from 'react';

function Food({name, picture}) {
  return <div>
    <h2>I like {name}</h2>
    <img src={picture}></img>
  </div>
}

const foodILike = [
  {
    name: "Kimchi",
    image:
      "http://aeriskitchen.com/wp-content/uploads/2008/09/kimchi_bokkeumbap_02-.jpg",
  },
 // .... 
];

function App() {
  return (
    <div>
      { foodILike.map(dish => (
        <Food name={dish.name} key={dish.name} picture={dish.image} />
      ))}
      
    </div>
  );
}

export default App;
```

- <Food> 에 props 로 foodILike의 name과 image 를 보내고 Food 에서는 받은 데이터를 {} 로 뿌려준다.

#### 2 - 4. Protection with PropTypes
- $ npm i prop-types //  prop-types 설치
- prop-types 를 이용해서 내가 전달받은 props가 원하는 props인지 확인해준다.

```javascript
import PropTypes from 'prop-types'

// 얻고 싶은 props에 대한 설명
Food.propTypes = {
  name: PropTypes.string.isRequired,
  picture: PropTypes.string.isRequired,
  rating: PropTypes.number.isRequired,
  // rating을 PropTypes.string.isRequired로 쓰면 콘솔 에러를 확인할 수 있다 => rating은 number이기 때문!
  // string 뿐만아니라, boolean, object 인지 있는지 없는지까지 확인할 수 있다.
  // rating: PropTypes.number 로 적는다면 number or undefined 라는 뜻 (number여야 하지만 필수는 아니라는 뜻) 
  // 근데 만약 위와같이 적고 rating에 string 을 넣는다면 에러가뜬다 (number를 예상했는데 string 을 제공했기 때문)
};
```

- prop-types 을 통해 type 만 체크할수도 있고, isRequired를 호출하는 방식으로 type과 require를 체크할 수 있다.
- 단 prop-types 은 사용할때 Food.sexyTypes 이라던지 이름을 바꾸면 react가 확인하지 않기때문에 무조건 Food.propTypes 형태로 사용해 줘야 한다.
- 참고사이트 : [PropTypes와 함께 하는 타입 확인](https://ko.reactjs.org/docs/typechecking-with-proptypes.html)

### 🖥 STATE - 3
#### 3 - 0. Class Components and State


