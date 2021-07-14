## 리덕스
> A Predictable State Container for JS Apps <br />
> 자바스크립트 앱을 위한 예측 가능한 상태 컨테이너 <br />
> 출처 : [Redux 공식문서](https://ko.redux.js.org/)

- 리덕스는 자바스크립트 App에서 **상태(state)를 효율적으로 관리**할 수 있게 도와주는 도구이다.
- React나 다른 뷰 라이브러리와 함께 사용할 수 있다.
- state(상태)는 객체`{ }`이다.
- state는 `dispatcher`, `reducer`를 통해서만 데이터를 수정할 수 있고 또한 데이터를 가져갈 때도 `getState()`를 통해서만 가져갈 수 있다.
- 이렇게 함으로써 데이터를 외부에서 직접 제어할 수 없게 하고 그로 인해 의도하지 않게 state값이 바뀌는 문제를 사전에 차단할 수 있다.
- 또한 데이터를 만들 때, 원본을 직접 바꾸는 것이 아니라 원본을 복제하고 복제한 데이터를 수정해서 새로운 원본을 만드는 방식을 사용한다. 
그러면 각각의 상태 변화가 서로에게 영향을 전혀 주지 않는 독립된 형태를 유지할 수 있다. 

### 설치
```
yarn add redux

yarn add react-redux
```
<br />

## State (상태)
- 리덕스에서 저장하고 있는 상태값
- 딕셔너리 형태 `{key: value}`로 보관한다.
- <br />

## Action (액션)
- reducer와 소통하는 방법으로 Object여야하며 그 key는 항상 type이다.
```
{ type: "CHANGE_STATE", data: {...} }
```
<br />

## Action Creator (액션 생성 함수)
- Action Creator는 액션을 만드는 함수이다.
- 파라미터를 받아와서 액션 객체 형태로 만들어준다.
- 액션을 return해준다.
```
const changeState = (new_data) => {
  return {
    type: "CHANGE_STATE",
    data: new_data,
  }
}
```
<br />

## Reducer (리듀서)
- 순수함수
- 리덕스에 저장된 상태를 변경하는 함수
- 리듀서는 이전 상태와 액션을 파라미터로 받는다.
> 액션 생성 함수 호출 -> 액션 생성 -> 리듀서가 현재 상태와 액션 객체를 받음 -> 새로운 데이터 생성 -> 리턴
```
const initialState = {
  name: "Kim"
}

function reducer (state = initialState, action) {
  switch(action.type) {
    case: CHANGE_STATE:
      return { name: "PARK" };
    default:
      return false;
  }
}
```
<br />

## Store (스토어)
- 한 개의 프로젝트는 하나의 스토어만을 가질 수 있다.
- state(상태)를 저장하는 곳이다.
<br />

## Dispatch (디스패치)
- reducer에게 action을 보내는 방법이다.
- action을 발생시키는 역할을 한다.
- `dispatch(action);`의 형태로 액션 객체를 파라미터로 넣어 호출한다.
<br />

## Subscribe (구독)
- 스토어 내장 함수 중 하나
- store 안에 있는 변화를 감지한다.
- subscribe 함수 안에 Listener 함수를 파라미터로 넣어주면, 이 함수가 액션이 디스패치되어 상태가 업데이트 될 때마다 호출된다.
- `store.subscribe(func);` -> store 안에 변화를 감지하면 func 실행
```
const listener = () => {
  console.log("Update!");
};

const unsubscribe = store.subscribe(listener);

unsubscribe(); // 구독을 해제할 때 호출
```
