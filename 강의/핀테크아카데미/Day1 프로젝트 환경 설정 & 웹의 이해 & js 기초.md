# Day1. 프로젝트 환경 설정 & 웹의 이해 & js 기초 & 리액트 초기설정

### 개발환경

- 서버 : NodeJS → cmd node 입력 후 설치되어있는지 확인
- 프론트 : React → npm install create-react-app -g 로 리액트 설치

    React vs React native : 웹에 특화되어있고 모바일에 특화되어있다. 

- IDE : Visual Studio Code

    js 실행 : node .\first_example.js

- 형상관리 : Git, Sourcetree

### 웹 어플리케이션

- 서버 : 사용자 요청에 대한 응답
- 클라이언트 : 사용자가 사용하는 프로그램
- 네트워크 : 클라이언트의 요청 전달
- HTTP 통신 규약을 지켜야 함

### Javascript(ES6)

> **let vs const**

`**let`** 은 변수 재선언, 재할당이 가능하고 `**const**`는 변수 재선언, 재할당 모두 불가능하다.  

> **배열**

```jsx
let cars = ["sonata", "bmw", "porter", 100];
console.log(cars[0], cars[1], cars[2], cars[3]);
cars.push("hello");
console.log(cars);
```

데이터 타입이 달라도 배열의 요소가 될 수 있다. 

> **반복문**

```jsx
// 반복문 1
for(let i=0; i<cars.length; i++) {
    let car = cars[i];
    console.log(car);
}

// 반복문 2
for(car of cars) {
    console.log(car);
}

// 배열의 map 메서드 사용
cars.map((car) => {
    console.log(car);
});
```

> **기타 표현법**

```jsx
const printCar = (name, ph, sn, date) => {
    console.log(name, ph, sn, date);
};

const printCar = (car) => {
    // let name = car.name;
    const {name, ph, sn, date} = car;
    console.log(name, ph, sn, date);
};

printCar(car);
```

```jsx
const printCar = (car) => {
    // let name = car.name;
    const {name, ph, sn, date} = car;
    const description = "자동차의 정보는" + name + " 입니다. 자동차의 마력은 : " + ph + " 입니다.";
    const templetDescription = `자동차의 이름은 : ${name} 입니다. 자동차의 마력은 ${ph} 입니다`; 
    console.log(name, ph, sn, date);
    console.log(templetDescription);
};
printCar(car);
```

### 리액트 시작

`**npx create-react-app 폴더이름**` : 프로젝트 폴더를 생성하고자 하는 폴더에서 다음과 같은 명령어를 입력하면 npm 패키지를 일회성으로 사용할 수 있게 해준다. `package.json` 이 있는 곳에 프로젝트가 존재해야한다.

`**npm start**` : [http://localhost:3000/](http://localhost:3000/) 가 접속됨을 확인할 수 있다.