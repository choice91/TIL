## useEffect()
> Effect Hook을 사용하면 함수 컴포넌트에서 side effect를 수행할 수 있습니다.   
> side effect라는 것은 데이터 가져오기, 구독(subscription) 설정하기, 수동으로 리액트 컴포넌트의 DOM을 수정하는 것까지의 모든 것을 말한다.   
> 출처 : [공식문서](https://ko.reactjs.org/docs/hooks-effect.html)

useEffect()를 사용해서 클래스형 컴포넌트의 life cycle을 구현할 수 있다. 

- useEffect()의 첫번째 인자값으로는 함수가 들어와야한다.
- 웹페이지가 처음 렌더가 끝났을 때 실행이 되고, 렌더가 또 실행될 때마다 실행된다.

생활코딩 강의를 보고 정리해봤다.

---
### 1. componentDidMount와 componentDidUpdate
```
import React, { useState, useEffect } from "react";
import "./App.css";

function App() {
  return (
    <div className="container">
      <h1>Hello World</h1>
      <FuncComp initNumber={2}></FuncComp>
    </div>
  );
}

let funcId = 0;
function FuncComp(props) {
  const [number, setNumber] = useState(props.initNumber);
  const [date, setDate] = useState(new Date().toString());

  useEffect(function () {
    console.log("func => useEffect " + ++funcId);
    document.title = number + " : " + date;
  });

  console.log("func => render " + ++funcId);

  return (
    <div className="container">
      <h2>function style component</h2>
      <p>Number : {number}</p>
      <p>Date : {date}</p>
      <button
        onClick={() => {
          setNumber(Math.random());
        }}
      >
        random
      </button>
      <button
        onClick={() => {
          setDate(new Date().toString());
        }}
      >
        date
      </button>
    </div>
  );
}

export default App;
```
![1](https://user-images.githubusercontent.com/48742487/125395047-97e03000-e3e5-11eb-998b-661f367d078a.png)
- 처음 렌더링이 될 때 render가 먼저 출력되고나서 useEffect가 호출되는 것을 console.log()로 출력하면서 확인할 수 있다.   
- render 후 componentDidMount가 실행되는 클래스형 컴포넌트와 유사하다. 
<br />

![2](https://user-images.githubusercontent.com/48742487/125396937-35d4fa00-e3e8-11eb-9ea2-d776f86b9fa3.png)
- 위의 코드에서 버튼을 눌러 number와 date에 변화를 줄 때마다 render가 된 후 useEffect가 호출된다.
- componentDidUpdate와 비슷한 역할
---
### 2. useEffect는 여러 개를 사용할 수도 있다. 
---
### 3. componentWillUnmount
```
import React, { useState, useEffect } from "react";
import "./App.css";

function App() {
  return (
    <div className="container">
      <h1>Hello World</h1>
      <FuncComp initNumber={2}></FuncComp>
    </div>
  );
}

let funcId = 0;
function FuncComp(props) {
  const [number, setNumber] = useState(props.initNumber);
  const [date, setDate] = useState(new Date().toString());

  useEffect(function () {
    console.log("func => useEffect " + ++funcId);
    document.title = number + " : " + date;
    return function () {
      console.log("func => useEffect return " + ++funcId);
    };
  });

  console.log("func => render " + ++funcId);

  return (
    <div className="container">
      <h2>function style component</h2>
      <p>Number : {number}</p>
      <p>Date : {date}</p>
      <button
        onClick={() => {
          setNumber(Math.random());
        }}
      >
        random
      </button>
      <button
        onClick={() => {
          setDate(new Date().toString());
        }}
      >
        date
      </button>
    </div>
  );
}

export default App;
```
![3](https://user-images.githubusercontent.com/48742487/125397548-0bd00780-e3e9-11eb-8d56-ef31e2e0a262.png)   
- 두번째값까지는 처음 렌더링됬을 때, 세번째값부터는 button을 눌러서 date와 number에 변화를 줬을 때 어떤 순서대로 실행되는지를 보여준다.
- useEffect가 실행이 되고나서 다시 똑같은 useEffect가 실행될 때 그 전에 return에 있는 함수를 실행시켜준다.
- 즉, 일종의 정리정돈의 작업을 처리할 수 있게 해준다. Cleanup이라고도 함
- return을 품고 있는 함수가 다시 실행될 때 return을 실행시켜준다.
---
### 4. Skipping Effect
- useEffect의 두번째 인자값을 넣어주면 두번째 인자값이 변경되었을 때만 useEffect를 실행하게 할 수 있다.
```
import React, { useState, useEffect } from "react";
import "./App.css";

function App() {
  return (
    <div className="container">
      <h1>Hello World</h1>
      <FuncComp initNumber={2}></FuncComp>
    </div>
  );
}

let funcId = 0;
function FuncComp(props) {
  const [number, setNumber] = useState(props.initNumber);
  const [date, setDate] = useState(new Date().toString());

  useEffect(
    function () {
      console.log("func => useEffect number " + ++funcId);
      document.title = number;
      return function () {
        console.log("func => useEffect number return " + ++funcId);
      };
    },
    [number]
  );

  useEffect(
    function () {
      console.log("func => useEffect date " + ++funcId);
      document.title = date;
      return function () {
        console.log("func => useEffect date return " + ++funcId);
      };
    },
    [date]
  );

  console.log("func => render " + ++funcId);

  return (
    <div className="container">
      <h2>function style component</h2>
      <p>Number : {number}</p>
      <p>Date : {date}</p>
      <button
        onClick={() => {
          setNumber(Math.random());
        }}
      >
        random
      </button>
      <button
        onClick={() => {
          setDate(new Date().toString());
        }}
      >
        date
      </button>
    </div>
  );
}

export default App;
```
처음 렌더링 되었을 때   
![4](https://user-images.githubusercontent.com/48742487/125398970-efcd6580-e3ea-11eb-87f7-22e7764cd92b.png)   

소스코드에서 첫 번째 useEffect()는 number가 변했을 때만 실행된다.   
![5](https://user-images.githubusercontent.com/48742487/125399008-f8be3700-e3ea-11eb-8621-b499ca34a14b.png)   

두번째 useEffect는 data가 변했을 때만 실행한다.   
![6](https://user-images.githubusercontent.com/48742487/125399028-fc51be00-e3ea-11eb-8222-1d25d2a3f094.png)   

---
5. useEffect의 두번째 인자값으로 빈배열 전달하기
- 기본적으로 useEffect()를 사용하면 componentDidMount, componentDidUpdate와 똑같은 효과를 내는데 두번째 인자값으로 빈배열을 넘겨주면 처음 1회만 실행되고 더 이상 실행되지 않는다.
```
useEffect(function () {
	console.log("func => useEffect (componentDidMount) " + ++funcId);
	document.title = number;
	// 부모 컴포넌트에서 자식 컴포넌트를 Unmount시킬 때 return이 실행됨
	return function () {
		console.log("func => useEffect (componentWillUnmount) return " + ++funcId);
	};
}, []);
```
렌더링 되었을 때   
![7](https://user-images.githubusercontent.com/48742487/125401007-9155b680-e3ed-11eb-8938-c4b09e410b8d.png)   

부모 컴포넌트에서 자식 컴포넌트를 Unmount시킬 때 return된다.
![8](https://user-images.githubusercontent.com/48742487/125401026-96b30100-e3ed-11eb-9059-c4b0a8e54e64.png)   
