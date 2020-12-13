# Typescript

## 함수타입

- 함수 매개변수 타입과 함수 실행 후 어떤 타입으로 반환되는지 타입 어노테이션을 해줘야 한다.

```tsx
// 매개변수가 모두 number type이라 반환타입을 정의해주지 않아도 number type임을 추론함
function add(x: number, y: number): number {
  return x + y;
}
// 화살표 함수의 어노테이션
const minus = (x: number, y: number): number => x - y;
// 함수표현식 어노테이션. 왼쪽에 이미 정의해놨으므로 오른쪽 매개변수 타입과 반환을 적지 않아도 된다.
const sum: (x: number, y: number) => number = function (x, y) {
  return x + y;
};
```

- 선택 매개변수(옵셔널 매개변수)
  반드시 입력하지 않아도 되는 매개변수이다. 매개변수 이름 오른족에 물음표를 입력하면된다.

```tsx
function sumMaxThree(x: number, y: number, z?: number): number {
  return x + y + (z ? z : 0);
}
```

선택 매개변수 오른쪽에 필수 매개변수가 오면 컴파일 에러가 발생한다. 그럴땐 유니온타입을 이용해서 undefined도 입혁해주도록 한다. 단, undefined를 항상 인자값으로 넘겨줘야하고 가독성이 좋지 않게된다.

```tsx
//오른쪽 매개변수가 필수매개변수일 경우 에러가 발생한다.
function userInfo(name: string, favorit?: string, age: number): string {
  //...
}

function userInfo(
  name: string,
  favorit: string | undefined,
  age: number
): string {
  //...
}
unerInfo("ann", undefined, 20); //undefined를 매개변수로 넘겨줘야하고 가독성이 떨어진다.
```

- 매개변수에 디폴트 값을 주면 그 값의 타입으로 정의 된다.

```tsx
// 매개변수 기본값 정의로 string type이 추론된다, 반환값 역시 string type으로 추론된다.
function pizza(topping = "cheese"): string {
  return `${topping}pizza`;
}
//기본값이 있는 매개변수는 선택 매개변수다.
const menu1: (topping?: string) => string = pizza;
```

- this타입

```tsx
//this는 항상 매개변수자리중 첫번째에 정의하고, name은 두번재 매개변수가 아니라 첫번째 매개변수가 된다.
function getInfo(this: string, name: string, age: number): string {
  const info = this.split(",");
  //..
}
```

- 원시 타입에 메서드 추가하기

```tsx
//인터페이스를 이용해 이미 존재하는 문자열 타입에 getInfo메서드를 추가하고
//문자열의 프로토타입에 작성한 함수를 등록한다.
interface String {
  getInfo(this: string, name: string, age: number): string;
}
String.prototype.getInfo = getInfo;
```

- 함수 시그니처와 오버라이딩

  문자열 자체를 타입 어노테이션으로 명시 할 수있다.

  바디 없이 함수의 인자와 값의 타입을 정의 → **함수 시그니처**

  함수 시그니처를 동일한 이름으로 여러개 정의 → **함수 오버라이딩 시그니처** (\**구현체*를 작성해 줘야한다.)

```tsx
interface FreshBasket {}
interface OtherBasket {}

//시그니처 목록
function basket(list: "당근"): FreshBasket;
function basket(list: "인형"): OtherBasket;

//구현체
function basket(list: "당근" | "인형") {
  // union type
  if (list === "당근") {
  } else if (lis === "인형") {
  } else {
    throw new Error("unsupported type");
  }
}
```

- 명명된 매개변수 사용하기

```tsx
function getInfoText({
  name,
  age = 15,
  language,
}: {
  name: string;
  age?: number;
  language?: string;
}): string {
  const nameText = name.substr(0, 10);
  const ageText = age >= 35 ? "senior" : "junior";
  return `name: ${nameText}, age: ${ageText}, language: ${language}`;
}

//위의 명명된 매개변수 타입을 재사용하기
//인터페이스로 명명된 매개변수 타입을 정의하면 다른 코드에도 재사용 할 수 있다.
interface Param {
  name: string;
  age?: number;
  language?: string;
}
function getInfoText({ name, age = 15, language }: Param): string {
  // ...
}
```
