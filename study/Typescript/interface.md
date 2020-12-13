# Typescript

## 인터페이스

- `interface`는 컴파일 시점에서만 참조되므로 코드양에 영향을 미치지 않는다. 그리고 구현체가 없고 행위만 기록된다. 속성(데이터)만 담아둔다고 생각하면 된다.
- 정의한 인터페이스의 하나 이상의 속성 타입을 만족하지 못하면 타입 에러가 발생한다.

```tsx
interface Person {
  name: string;
  age: number;
}
const p1: Person = { name: "mike", age: "23" }; //에러발생
```

### 선택속성

- 없어도 되는 속성을 말한다. 물음표기호를 사용한다.
- 물음표기호를 사용하지 않고 undefined를 유니온타입으로 추가할수 잇으나 명시적으로 그 속성을 입력해 줘야 한다.

```tsx
interface Person {
  name: string;
  age?: number;
}
const p1: Person = { name: "mike" }; //정상작동

interface Person {
  name: string;
  age: number | undefined;
}
const p1: Person = { name: "mike", age: undefined }; //명시적으로 값을 입력해 줘야 한다.
```

### 읽기 전용 속성

- 객체에서 읽기 전용 속성은 값이 변하지 않는 속성을 말하며 readonly키워드를 사용한다.

```tsx
interface Person {
  readonly name: string;
  age: number;
}
const p1: Person = {
  name:'anna'; //변수를 정의 하는 시점에서는 값을 할당 할 수 있다.
}
p1.name = 'sunny'; //컴파일 에러
```

### 정의되지 않은 속성값에 대한 처리

- 리터럴로 값을 초기화 하는 경우에는 인터페이스에 정의되지 않은 속성값이 있다면 타입 에러가 발생힌다.
- 객체가 인터페이스에 정의되지 않은 속성값을 갖고 있어도 인터페이스의 조건을 충족한다면 할당이 가능하다.(덕타이핑or구조적타이핑)

```tsx
interface Person {
  name: string;
  age?: number;
}
const p1: Person = { name: 'mike', birth: 2000 }; //타입에러
const p2 = { name: 'mike', birth: 2000 }
const p3 Person = p2; //에러가 발생하지 않는다.
```

### 인터페이스로 정의 하는 인덱스 타입

- 속성의 이름을 구체적으로 정의하지 않고 값의 타입만 정의하는 것

```tsx
interface Person {
  name: string;
  age: number;
  [key: string]: string | number;
}
const p1: Person = { name: "mike", age: 21, birth: 2000 };
```

### 여러개의 인덱스를 정의하는 경우

- 자바스크립트에서는 속성 이름에 숫자를 사용하면 문자열로 변환된 후 사용된다. 따라서 타입스크립트는 숫자인 속성 이름의 값이 문자열인 속성 이름의 값으로 할당 가능한지 검사한다.

```tsx
//숫자타입인 A는 문자열타입의 B에 할당이 가능해야 한다.
interface YearPriceMap {
  [year: number]: A;
  [year: string]: B;
}

//위의 조건을 만족하는 예시
interface YearPriceMap {
  [year: number]: number;
  [year: string]: string | number;
}
```

### 인터페이스로 함수 타입 정의

- 함수타입에 나왔었지만 인터페이스로 함수 타입을 정의 할 수 있고, 속성 이름 없이 정의 한다.
- 함수의 속성값도 정의 할 수 있다.

```tsx
interface GetInfoText {
  (name: string, age: number): string;
  totalCall: number;
}
const getInfoText: GetInfoText = function (name, age) {
  getInfoText.totalCall += 1;
  const nameText = name.substr(0, 10);
  const ageText = age >= 35 ? "senior" : "junior";
  return `name: ${nameText}, age: ${ageText}, totalCall: ${getInfoText.totalCall}`;
};
getInfoText.totalCall = 0;
```

### 인터페이스로 클래스 구현하기

- 인터페이스는 클래스로 구현될 수도 있는데, 클래스 타입에서 같이 참고 하면 될것 같다.

### 인터페이스로 확장하기

```tsx
interface Person {
  name: string;
  age: number;
}
interface Korean extends Person {
  isLiveInSeoul: boolean;
}
===========================
//Korean 인터페이스의 모습
interface Korean {
  name: string;
  age: number;
  isLiveInSeoul: boolean;
}
```

확장받을 인터페이스를 ,로 이어서 써서 여러개를 확장할 수도 있다.(위의 코드에선 Person, Person1...이런식으로)

### 인터페이스 합치기

- 교차타입(intersection)을 통하여 여러 인터페이스를 하나로 합칠 수 있다. 타입에서의 교집합은 더 많은 타입제한이 걸리며 집합의 크기가 작아지는걸 뜻한다. 그러므로 교차되는 인터페이스의 모든 속성을 충족하는 더 작은 집합이 만들어 진다.

```tsx
interface Name {
  name: string;
}

interface Info {
  age: number;
  birth: number;
}

type WURI = Name & Info;

const wuri: WURI = {
  name: "wuri",
  age: 20,
  birth: 2020,
};
```
