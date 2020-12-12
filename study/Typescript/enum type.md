# Typescript

## 열거(enum)타입

열거형 타입의 각 원소는 값으로 사용될 수 있고, 타입으로도 사용될 수 있다.
아무것도 할당하지 않으면 자동으로 첫번째 순서부터 0으로 할당되고 1씩 증가한 값이 할당된다.

```typescript
enum Fruit {
    Apple,
    Banana,
    Orange,
}
===========================
var Fruit;
(function (Fruit) {
    Fruit[Fruit["Apple"] = 0] = "Apple";
    Fruit[Fruit["Banana"] = 1] = "Banana";
    Fruit[Fruit["Orange"] = 2] = "Orange";
})(Fruit || (Fruit = {}));
```

열거형 타입은 컴파일 후에도 관련된 코드가 남으며, 객체로 존재하게된다.
객체이므로 일반적인 객체처럼 다룰수 있고, 각 원소의 이름과 값이 양방향 매핑이 되어있기 때문에 값을 이용해서 이름을 가져올수도있다.

```typescript
enum Fruit {
  Apple,
  Banana = 4,
  Orange,
}
console.log(Fruit.Banana); // 5
console.log(Fruit["Banana"]); //5
consnole.log(Fruit[4]); //Banana
```

열거형 타입의 원소에 문자열을 할당하게되면 컴파일 결과가 달라진다.
문자열을 할당하는경우에는 단방향으로 매핑된다. 서로다른 원소의 이름 또는 값이 같을 경우 충돌이 발생되기 때문이라고 한다.

```typescript
enum Language {
    Korean = 'ko',
    English = 'en',
    Japanese = 'jp',
}
===========================
var Language;
(function (Language) {
    Language["Korean"] = "ko";
    Language["English"] = "en";
    Language["Japanese"] = "jp";
})(Language || (Language = {}));
```

### 열거형 타입을 위한 유틸리티함수

```typescript
function getEnumLength(enumObject:any) {
    const keys = Object.keys(enumObject);
    return keys.reduce((acc,key) => (typeof enumObject[key] === 'string'? acc +1 : acc),0,);
}

function isValidEnumValue(enumObject:any, value:number|string) {
    if(typeof value === 'number') {
        return !!enumObject[value];
    }else{
        return(
            Object.keys(enumObject).filter(key=>isNaN(Number(key))).some(key=>enumObject[key]===value)
        )
    }
}

enum Fruit {
    Apple,
    Banana,
    Orange,
}

enum Language {
    Korean = 'ko',
    English = 'en',
    Japanese = 'jp',
}

const l = console.log;

l(getEnumLength(Fruit), getEnumLength(Language));
l('1 in Fruit: ', isValidEnumValue(Fruit, 1));
l('5 in Fruit: ', isValidEnumValue(Fruit, 5));
l('Banana in Fruit: ', isValidEnumValue(Fruit, 'Banana'));
l('ko in Language: ', isValidEnumValue(Language,'ko'));
l('Korean in Language: ', isValidEnumValue(Language,'Korean'));

================
[LOG]: 3,  3
[LOG]: "1 in Fruit: ",  true
[LOG]: "5 in Fruit: ",  false
[LOG]: "Banana in Fruit: ",  false
[LOG]: "ko in Language: ",  true
[LOG]: "Korean in Language: ",  false

```

### 상수형 열거형 타입

열거형 타입은 컴파일 후에도 남아있어 번들 파일의 크기가 커질수 있다. 열거형 타입의 객체에 접근하지 않는다면 굳이 컴파일 후에 객체로 남겨 놓을 필요는 없다.
상수 열거형 타입을 사용하면 컴파일 결과에 객체를 남겨 놓지 않을 수 있다.
하지만 열거형 타입을 상수로 정의하면 열거형 타입의객체를 사용할 수 없으므로 모든 경우에 쓸 수 있는것은 아니다.
<br>
<br>
<br>

- 출처: 실전리액트프로그래밍
