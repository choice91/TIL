## Redux Toolkit
### 설치
```
yarn add @reduxjs/toolki
```
<br />

### Redux Toolkit이란?
기존 Redux 이용시 필요한 코드를 많이 줄여주고 비동기 통신에 필요한 thunk 미들웨어 라이브러리를 내장하고 있다는 장점이 있다.
<br />

### CreateAction
createAction 함수는 action 타입 문자열로 인자를 받고, 해당 타입을 사용하는 액션 생성자함수를 return한다.<br />
action의 값은 payload 안에 있다. action.payload로 값을 알 수 있다.
```
// Before
const INCREMENT = "counter/increment";

function increment(amount) {
  return {
	  type: INCREMENT,
		payload: amount
  }
}

const action = increment(3);
```
위의 코드를 createAction을 사용하면 아래처럼 짧게 쓸 수 있다.
```
// After
import { createAction } from "@reduxjs/toolkit";

const increment = createAction('counter/increment');

let action = increment();

action = increment(3);
```
<br />

예제<br />
```
import { createStore } from "redux";
import { createAction } from "@reduxjs/toolkit";

const addToDo = createAction("ADD");
const deleteToDo = createAction("DELETE");

// Reducer
const reducer = (state = [], action) => {
  switch (action.type) {
    case addToDo.type:
      console.log(action);
      return [{ text: action.payload, id: Date.now() }, ...state];
    case deleteToDo.type:
      return state.filter((toDo) => toDo.id !== action.payload);
    default:
      return state;
  }
};

const store = createStore(reducer);

export const actionCreator = {
  addToDo,
  deleteToDo,
};

export default store;
```
<br />

### CreateReducer
기존 reducer 함수를 대체한다.<br />
기존 reducer 함수는 switch문으로 action.type을 확인하고 처리를 해줬는데 createReducer함수는 lookup 테이블을 사용하여 reducer를 작성할 수 있다.<br />
객체의 각 키는 redux action type 문자열이며 값은 reducer 함수이다.<br />
또한 reducer 함수에서 새로운 state 객체를 리턴할 필요 없이 state 값을 직접 변경하는 방식으로 코드를 작성하면 된다.
```
const initialState = { value: 0 }

function counterReducer(state = initialState, action) {
  switch (action.type) {
    case 'increment':
      return { ...state, value: state.value + 1 }
    case 'decrement':
      return { ...state, value: state.value - 1 }
    case 'incrementByAmount':
      return { ...state, value: state.value + action.payload }
    default:
      return state
  }
}
```
