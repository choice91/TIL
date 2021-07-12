## useState()
- 함수형 컴포넌트에서 state를 만들 때에는 useState를 호출한다.
- state의 인자로는 state의 초기값이 들어온다.
- 2개의 값으로 이루어진 배열로 리턴하는데 그 중 첫번째 값은 상태값, 두번째 값은 그 상태값을 바꿀 수 있는 함수가 온다.
- 따라서 함수형 컴포넌트에서도 useState를 이용해서 state를 관리할 수 있다.

ex)
```
import { useState } from "react"

const textState = useState(초기값);
const text = textState[0];
const setText = textState[1];
```
useState는 2개의 값으로 이루어진 배열로 리턴한다. console.log()를 해보면 2개의 값을 가진 배열을 리턴하는 것을 볼 수 있다.   
![image](https://user-images.githubusercontent.com/48742487/125316518-25366c80-e373-11eb-99d5-0eb416d46630.png)


```
const [text, setText] = React.useState(초기값)
```
혹은
```
import { useState} from "react"

const [text, setText] = useState(초기값)
```
