#Javascript 공부

## 호이스팅(Hoisting)

자바스크립트 공부를 시작한지 어언 3개월째, 호이스팅이란 개념은 공부시작하던 때에 책에서 나와서 알고 있다고 생각했으나 실행문맥을 공부하다가 다시 호이스팅 까지 내용이 이어졌을때 지금까지 알고 있던 개념이 뭔가 잘못된것 같다란 생각이 들며 혼란이 오기 시작했다.

그래서 다시 한번 되짚어 볼겸 열심히 각종 블로그와 글들을 보다가 MDN을 봐도 시원하지 않아서 명세까지 뒤지게 되었다.

영어 알못이라 번역기로 돌렸다가 ~~let이 하자로 번역 되고 body가 몸으로 번역되는 대참사를 보고~~ 조용히 영문으로 다시 돌려서 한줄한줄 장인의 한땀처럼 번역기를 조금씩 돌려가며 보았다.

일단 호이스팅이라는것은 **변수(var, let, const), 함수(function, function *)를 선언**하면 해당 스코프에 최상단에서 선언한것처럼 작동 시키는 것을 말하는데, 아래의 예제를 보자.



```javascript
//첫번째 예제

console.log(tomato); //undefined
var tomato = 5;

console.log(banana); //Uncaught ReferenceError: Cannot access 'banana' before initialization
let banana = 8;
```



앗 뭐지? var로 선언한건 undefined가 뜨고 *let으로 선언한건 레퍼런스에러*가 뜬다.

그렇다면 let은 호이스팅이 안되는걸까? 다른 예제를 살펴보자.



```javascript
//두번째 예제

function apple() {
    console.log(cherry);
};
let cherry = 1;
apple(); //1
```

위의 코드를 실행하면 1이 찍히는걸 볼 수 있는데, let도 호이스팅이 된다는거다.



#### 그렇다면 첫번째 예제의 에러는 왜 그런걸까?

이건 자바스크립트의 변수생성이 어떻게 이루어지는지를 먼저 알아야 하는데, 변수는 아래 3가지 단계를 거쳐 생성이 된다.



> 1. 선언 단계 (Declaration phase) : 변수를 실행문맥의 변수 객체에 등록, 이 변수 객체는 스코프가 참조하는 대상이됨.
> 2. 초기화 단계 (Initialization phase) : 변수객체에 등록된변수를 위한 공간을 메모리에 확보. undefined로 초기화.
> 3. 할당 단계 (Assignment phase) : undefined로 초기화된 변수에 실제 값을 할당.



그리고 명세에 따르면 let과 const의 선언에 대한 내용은 아래와 같다.

![letAndConstDeclaration](.\img\letAndConstDeclaration.png)

번역기로 열심히 돌려가며 이해해본 바로는, 실행문맥의 렉시컬환경이 실행될때 let과 const는 선언이 되지만 값이 초기화 되는것은 아니다. **초기화는 선언문을 직접 만나는 시점에 이루어 지는데** 우리가 호이스팅을 배울때 변수의 선언이 끌어올려진다고 배우지만, **실제로 선언문이 끌어 올려지는것이 아니라, 마치 스코프의 최상단에 선언되는 것처럼 먼저 변수객체에 등록이 되는것**이다. 그리고 스코프 최상단부터 선언문을 만나기 전까지 '일시적인 사각지대(Temporal Dead Zone, TDZ)'가 발생하게 되는데 첫번째 예제의 에러가 바로 TDZ가 발생된 케이스다.

그래서 두번째 예제에서 아래처럼 순서를 바꾸면 레퍼런스에러가 나게된다.

```javascript
//두번째 예제 함수 실행순서 변경

function apple() {
    console.log(cherry);
};
apple(); //Uncaught ReferenceError: Cannot access 'cherry' before initialization
let cherry = 1;
```

let cherry라는 변수객체에 등록이 되었지만, 초기화 및 할당은 실제 선언코드를 만나기전까지 이루어 지지 않아서 TDZ에 빠진 상태이다. 그래서 초기화 전엔 cherry를 엑세스 할수 없다는 레퍼런스에러 문구가 뜨는것이다.
간혹 변수에 값이 할당되면 호이스팅이 되지 않는다고 생각하는 분들도 있는데, 할당값은 호이스팅 되지 않고, 선언만 호이스팅이 된다. 이부분 또한 착각하지 않도록 주의 해야한다.

그리고 여기서 또다른 궁금 증이 생겼다. 

#### 그럼 왜 var는 undefined로 뜰까?

그래서 명세를 또 찾아보았다.

![varDeclaration](.\img\varDeclaration.png)

위에 적힌 명세를 해석하면 var은 *선언과 동시에 초기화가* 이루어지며 undefined가 할당된다는 것을 알수 있다. 그래서 똑같이 호이스팅 되지만 var과 let은 다르게 나오는 것이다!

사실 호이스팅에 관한 글들은 많지만, 변수의 생성과정에 대한 이해가 없으니 많은 설명들을 보아도 제대로 이해가 되지 않았는데 역시 깊게 알려면 사전지식이 많이 필요한것 같다. 

자바스크립트는 어렵지만 재밌다!



##### 참고 링크

* <http://www.ecma-international.org/ecma-262/6.0/index.html>
* <https://poiemaweb.com/es6-block-scope>
* <http://2ality.com/2015/10/why-tdz.html>

