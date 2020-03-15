# Redux 기본컨셉

#리덕스 기본 컨셉 정리 #배우며 헷갈리던 것들 정리 #내가 느낀대로 정리

### 1. Store는 한 개만 사용한다

- 사용 할때는 redux에서 createStore를 소환(import)해서 사용한다.

```javascript
/*소환 주문*/
import { createStore } from "redux";
```

- Store를 프로젝트내에 한개만 만드는걸 원칙으로 한다.

### 2. Store는 reducer만 상태를 변경 한다

- 위처럼 소환한 createStore를 할당할 때 인자값으로 reducer를 넣어줘야한다.
- reducer만 상태(state)값을 변경할 수 있는다.
- reducer는 state와 action을 인자로 갖는 함수이다.

```javascript
//state가 바로 store의 상태값이다
const reducer = (state, action) => {
  /*내용*/
};
```

### 3. dispatch라는 마법봉을 휘둘러야 한다

- 유일하게 store의 상태값을 수정(return)할 수 있는 reducer를 사용하기 위해선 dispatch라는 마법봉을 휘둘러야 한다.
- dispatch는 그냥 휘두르면 안되고 reducer의 두번째 인자인 action을 넣어 휘둘러야 reducer를 사용할 수 있다.
- action은 반드시 object여야 하며 필수값으로 type이라는 프로퍼티를 갖는다.

```javascript
// { type: 'ADD' }라는 액션을 담아 dispatch마법봉을 휘두르는 중
store.dispatch({ type: "ADD" });
```

- reducer는 dispatch가 보내준 action의 type의 값을 받아 일치하는 type의 내용을 return한다.

```javascript
/*switch문으로 사용해도 된다*/
const reducer = (state = 0, action) => {
  if (action.type === "ADD") {
    return state + 1;
  } else {
    return state;
  }
};
```

### 4. getStore()와 subscribe()의 차이는?

- getStore()는 읽기 전용으로 호출하는 시점의 데이터(store)값을 가져온다.
- subscribe()는 데이터(store)값이 변하면 그 값을 반영해준다. 인자는 콜백함수를 받는다.
- 둘의 차이는 데이터가 정적이냐(getStore) 동적이냐(subscribe)의 차이이다. (마치 DOM API의 querySelector와 getElement~ 의 차이)

### 5. 그 밖에 주의할점

- Store값은 언제나 불변적으로 관리해야한다.
- action type에 문자열로 넣으면 오타가 나도 에러발생시 찾기가 힘들다. 변수에 문자열을 담아 변수를 프로퍼티 값으로 넣어주면 오타시 에러로 확인할 수 있다.

```javascript
  const ADD = 'ADD';
  ...
  store.dispatch({ type: ADD });
  //변수명으로 넣기 때문에 오탈자가 발생 하면 is not defined.. 하고 에러가 발생한다
```
