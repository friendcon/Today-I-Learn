# Day2. React

### JSX

- app.js 구조

```jsx
function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          안녕하세요 <code>src/App.js</code> 를 불러왔습니다
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          리액트 배우기
        </a>
      </header>
    </div>
  );
}

export default App;
```

### React Component 와 Props

- **Component** : `**웹의 구성요소에대한 정의**`를 내릴 수 있다. 컴포넌트의 가장 큰 특징은 재사용이 가능하다는 점이다.
- **Props** : 프로퍼티를 통해 컴포넌트에 데이터를 전달한다

```jsx
const elements = <h1>Hello World!</h1>;
const Welcome = ({ userName }) => {
	return (
		<>
			<p>Hello {userName}</p>
		</>
	);
};

function App() {
	return (
		<div className="App">
			<Welcome userName={"홍길동"}></Welcome>
			<Welcome userName={"박길동"}></Welcome>
		</div>
	);
}
```

### 함수형 컴포넌트 vs 클래스형 컴포넌트

- **함수형 컴포넌트**

```jsx
function App() {
	const name = 'react';
	return (
		<>
			<p>Hello {name}</p>
		</>
	)
}
```

- **클래스형 컴포넌트**

```jsx
Class App extends Component {
	render() {
		const name = 'react';
		return <div className="react">{name}</div>
	}
}
```

### VScode snippet

React 자동완성 라이브러리

### React State

데이터를 저장하는 역할을 한다. 데이터가 변경되면 화면을 새로 그려준다.

데이터를 변경하기 위해서는 `**setState`** 함수를 사용해야한다.

```jsx
import react, {useState} from "react";

function App() {
	const [userName, setUserName] = useState("초기값");
	const changeUserName = (e) => {
		const { value, name } = e.target;
		setUserName(value);
		console.log(userName);
	};
	return (
		<div className="App">
			<input onChange={changeUserName}></input>
		</div>
	);
}
```

### React Event

onChange, onClick 과 같은 다양한 이벤트들이 선언되어있다.

### React 배열 컨트롤

```jsx
const ListComponent = () => {
    const [users, setUsers] = useState([
        {name: "홍길동", age:12, height:180},
        {name: "동", age:18, height:180},
        {name: "홍", age:16, height:180}
    ])
    return (
        <div>
						// 방법1
            { <p>{users[0].name} {users[0].age} {users[0].height}</p>
            <p>{users[1].name} {users[1].age} {users[1].height}</p>
            <p>{users[2].name} {users[2].age} {users[2].height}</p> }
						// 방법2
            {users.map((user) => {
                return (<p>{user.name} {user.age} {user.height}</p>)
            })}
        </div>
    )
}

export default ListComponent
```

### NPM

Node Packaged Manager. Nodejs에서 사용할 수 있는 모듈들을 패키지화하여 모아둔 저장소 역할을 하며 설치/관리를 수행하는 CLI 제공

### 라우팅

리액트는 `**SPA(Single Page Application)**` 방식으로써 여러개의 페이지를 사용하며, 새로운 페이지를 로드하는 기존의 방식과는 달리(ex 회원가입.html → 로그인.html) 필요한 데이터만 불러서 렌더링한다. 기존의 방식은 페이지를 완전히 다시 로드하는 반면 SPA 방식을 이용하면 재로드 없이 한페이지 안에서 이루어진다.

 `**React-Router**` 은 페이지를 새로 불러오지 않는 상황에서 각각의 선택에 따라 선택된 데이터를 하나의 페이지에서 렌더링 해주는 라이브러리다. 

### AXIOS

브라우저, Node.js를 위한 Promise API를 활용하는 `**HTTP 비동기 통신 라이브러리`** 

### CORS(Cross-Origin Resource Sharing)

브라우저간의 데이터를 주고받는 과정에서 도메인 이름이 서로 다른 사이트간에 api 요청을 할 때 공유설정을 해주지 않으면 CORS 에러가 발생한다.