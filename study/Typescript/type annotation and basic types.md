# Typescript

## Type annotation

:변수나 상수를 선언할 때 그 타입을 명시적으로 선언해 줌으로써 어떤 타입의 값이 저장될 것인지를 컴파일러에 직접 알려주는 문법

변수옆에 세미콜론(:)을 두고 그 오른쪽에 타입을 지정함
따로 타입을 지정하지 않으면 ①변수를 할당할때 타입이 결정되는데 ②이때 할당이 없으면 any타입이 된다.

```jsx
let score = 100; // number type이 된다.①
score = "100"; // string을 할당하면 에러 발생
```

```jsx
let score; // any type이 된다.②
score = 50;
score = "65"; //에러가 발생하지 않는다.
```

const는 상수이므로 타입 어노테이션이 없어도 할당하는 값을 보면 타입이 뭔지 알수 있다.

```jsx
const score = 90; // 상수 score가 number type임을 알 수 있다.
```

## 기본타입

> - primitive type : <code>number</code>, <code>string</code>, <code>boolean</code>, <code>null</code>, <code>undefined</code>, <code>symbol</code>
> - reference type : <code>object</code>

- ES6기준의 자바스크립트 데이터타입을 모두 제공해준다.
- string type은 `"",'',```모두 사용할 수있다.
- object type은 객체만 반환되는데 `let objValue: object = new String('A');` 이경우는 new연산자를 통해 객체가 반환되므로 오류가 발생하지 않는다.
- undefined와 null은 서로 바꿔 할당할 수 있으며, 이 둘은 하위타입이다.
- 하위타입은 상위타입 변수에 할당할 수있다.
- 모든 타입의 상위타입은 any type이다.
- 그 밖에 배열에 타입을 지정할 때는 `let List: string[];` 이렇게 배열원소의 타입을 적고 배열이라는 대괄호를 붙여준다.
- 변수 객체를 선언시점에서 어떠한 속성들이 정해지는지 별도의 타입지정없이 바로 지정해줄수 있는데 이러한 타입을 인라인 타입이라고한다.

```jsx
let user: { name: string, score: number };
user = { name: "jay", score: 50 };
```

하지만 같은 타입을 매번 선언할때마다 같이 적어주는건 번거롭고 생산적이지 못하다.

- interface는 컴파일 시점에서만 참조되므로 코드양에 영향을 미치지 않는다. 그리고 구현체가 없고 행위만 기록된다. 속성(데이터)만 담아둔다고 생각하면 된다.

```jsx
interface TV {
  turnOff(): void; // 반환값이 없다
  trunOn(): boolean; // ← 메서드의 바디({})가 없다(구현체가 없다)
  color?: string; //interface의 속성중 옵셔널한 속성은 ?를 뒤에 붙여주면 된다
}
```

```typescript
const size: number = 123; //number타입
const isBig: boolean = size >= 100; //boolean타입
const msg: string = isBig ? "크다" : "작다"; //string타입
const value1: number | string = "abc"; //union타입
const value2: number[] = [1, 2, 3]; //array타입
const value3: Array<number> = [1, 2, 3]; //generic타입
const data: [string, number] = [msg, size]; //tuple타입
let v1: 10 | 20 | 30; //숫자 리터럴 타입
let v2: "사과" | "바나나"; //문자 리터럴 타입
let value: any; //any타입

function f1(): void {
  //void타입
  console.log("hello world");
}
function f2(): never {
  //never타입
  throw new Error("error");
}
function f3(): never {
  //never타입
  while (true) {}
}

let v3: object = {
  //object타입
  name: "abc",
};

let v4: (1 | 2 | 3) & (2 | 3 | 4); //교차타입(&)과 유니온(|)타입

type Width = number | string; //type키워드로 별칭 주기
let width: Width;
width = 100;
width = "100px";
```

## void 타입

아무것도 반환하지 않고 종료되는 함수의 반환 타입이다

## never 타입

예외가 발생해서 비정상적으로 종료되거나 무한 루프때문에 종료되지 않는 함수의 반환 타입이다.

## oject 타입

객체의 속성에 대한 정보를 포합해서 타입을 정의하기 위해서는 인터페이스(interface)를 사용해야 한다.

<br>
<br>
<br>
- 출처: 실전리액트프로그래밍, 패스트캠퍼스 프론트강좌
