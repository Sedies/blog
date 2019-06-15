#Javascript 공부

# 디스트럭쳐링(destructuring assignment)

저번에 호이스팅에 대해 알아보고 난후, 그 후 다른 개념들도 공부겸 정리해보는게 좋을 것 같아 최근에 공부했던 디스트럭쳐링 문법에 대해 적어보자 한다.



### 디스트럭쳐링이란?

다른 말로는 비구조화 할당, 구조 분해라고도 부른다.

예전에 영어로된 문서를 통으로 번역 시켰더니 파괴로 번역되어  '왜 객체를 파괴하지..' 하면서 혼란이 더 가중된 적이 있는데, 영어를 우리나라 말로 바꾸면 의미가 온전치 못하게 전달되는게 많은것 같다. 여기서는 ~~내 맘대로 섞어서~~ 사용하고있다.

ES2015(ES6)에서 새로나온 문법으로 객체나 배열의 요소를 변수에 추출하는 문법인데, 말로만 설명하면 어려우니 예제들을 살펴 보자.



### 기본 문법

```javascript
//첫번째 예제

const fruitsColor = {
    apple: 'red',
    banana: 'yellow',
    grape: 'purple'
}

const {apple, banana, pineapple} = fruitsColor;
console.log(apple) //red
console.log(banana) //yellow
console.log(pineapple) //undefined
```



첫번째 예제는 기본 문법으로 fruitsColor의 객체 요소를 분해해서 할당해 주고 있다. 객체 요소이므로 분해해서 가져올 요소이름에 {}를 감싸준다. 배열이라면 []로 감싸주면 된다(두번째 예제 참고). 좌변은 값을 넣을 변수, 우변은 값을 할당할 변수가 된다. 존재하지 않는 요소이름을 선언하면 가져올 값이 없으므로 undefined를 반환한다.



```javascript
//두번째 예제

const alphabet = ['a','b','c','d'];

const [a,b, ...c] = alphabet;
console.log(a) //a
console.log(b) //b
console.log(c) //['c', 'd']
```

두번째 예제는 배열을 구조분해하였다. EC6 rest문법(나머지문법)을 사용하여 할당할 수 있으며, 배열요소를 할당할때는  인덱스 0번 부터 차례로 할당이 된다.



###  중첩과 새로운 변수명 할당

```javascript
const animal= {
   	dog :{
        name: '댕댕이',
        color: 'white',
        sounds: '왈왈!'
    },
    cat :{
        name: '냥이',
        color: ['brown','block','white'],
        sounds: '야~옹'
    }
}

const {dog:{name:dogName}, cat:{name:catName}, cat:{color:[reddish]}} = animal;
console.log(dogName); //댕댕이
console.log(catName); //냥이
console.log(reddish); //brown
```

중첩된 객체 및 배열도 분해해서 할당할 수 있고, 새로운 변수명으로 할당할 수있다.



### 값의 교환(swap)

값을 교환할때 temp같은 임시로 옮겨놓을 변수를 따로 만들지 않고도 간편하게 할 수 있다.

```javascript
//임시 변수를 이용한 값의 교환
function swap(one, two) {
    var temp = one;
    var one = two;
    var two = temp;
    console.log(one);
    console.log(two);
}
swap(1,2) // one:2, two:1


//구조분해를 이용한 값의 교환
let one = 1;
let two = 2;
[one, two] = [two, one];
console.log(one); //2
console.log(two); //1
```



### 매개변수

매개변수에서도 디스트럭쳐링을 사용할 수 있다.  

```javascript
function fruit({color}){
	console.log(`그 과일은 ${color}입니다.`)
}

const apple = {color:'빨간색'}
fruit(apple) //그 과일은 빨간색입니다.

const favorit = {
    apple:{
        color:'빨간색'
    },
    banana:{
        color:'노란색'
    },
    grape:{
        color:'보라색'
    }
}
fruit(favorit.banana) //그 과일은 노란색입니다.
fruit(favorit['grape']) //그 과일은 보라색입니다.

//디스트럭쳐링해서 간편하게 쓸수 있다.
const {apple, banana, grape} = favorit;
fruit(banana) //그 과일은 노란색입니다.
fruit(grape) //그 과일은 보라색입니다.
```



### 기본값 설정

ES6문법인 파라미터에 기본값 설정하는것이 가능하다.

```javascript
function apple({season='사계절', color='빨간색', brix=12}) {
    console.log(`사과는 ${season}에 재배시 대부분 ${color}이며 ${brix}당도를 가지고 있다.`)
}
apple({season:'봄', color:'초록색'}) //사과는 봄에 재배시 대부분 초록색이며 12당도를 가지고 있다.
```



### 퀴즈

```javascript
//1번 퀴즈
const alphabet = ['a','b','c','d'];
const [a,,d] = alpahbet;
console.log(a) //?
console.log(d) //?

//2번 퀴즈
function quiz({
    breakfast="milk",
    lunch="noodle",
    dinner="meat"
}={}) {
    console.log(`오늘 아침은 ${breakfast="rice"}를 먹고 점심은 어제처럼 ${lunch}, 저녁은 ${dinner}를 먹을 거에요`)
}
quiz() //?
```





##### 참고 링크

- <https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment>

* <https://beomy.tistory.com/18>
