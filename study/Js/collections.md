#Javascript 공부

# Collections(Map, Set, WeakMap, WeakSet)

오늘은 이전에 공부했던 Map, Set, WeakMap, WeakSet 객체들을 정리하는 시간을 가져보려한다. 해당 내용은 추후에 추가나 수정이 될수 있다. 



### Collection?

일단 이 객체들을 공부하다 보니 컬렉션이라는 말이 나온다. 컬렉션이라서 <code>length</code>프로퍼티는 0이고 개수는 <code>size</code>프로퍼티를 써야하고... 도데체 이게 무슨말이야? 역시 모를땐 다시 구글링이다!  찾아보니 **'데이터의 추가 및 추적, 수정 과 삭제를 할 수 있는 키-값 형태의 저장소', '자바스크립트의 데이터 구조'** 이정도로 정의를 할 수 있겠더라. 



###  왜 생겨났을까?

이러한 객체들이 생겨난 이유가 궁금해졌다. 키-값의 형태는 이미 <code>Object</code>도 있는데, 왜 생겨났을까?  

* <code>Object</code>는 키-값 형태로 되어있는 데이터지만 ES6전에는 <code>key</code>안에 <code>String</code>타입만 사용할 수 있다.
*  ES6이후엔 <code>symbol</code>도 사용 가능해 졌지만 **객체 자체는 반복을 위한 데이터가 아니다보니 방법을 이용하여 반복 시킬뿐 실제론 속도가 느리다** 한다. 
* 원소의 개수를 바로 알수 없다는 등의 불편함이 있었는데 콜렉션 객체로 인하여 **빠른 속도로 반복 작업을 시킬 수 있고**(내부적으로 해시 테이블을 활용하기 때문이라고 한다), **키-값 안에 각각 원하는 데이터 타입을 넣을 수 있게 되었다**. (원시타입은 물론 객체 타입도 사용할 수 있다.)



### Map

Map객체는 Map 생성자 함수로 생성한다. 인수를 지정하지 않으면 데이터가 없는 빈 Map객체가 생성된다. 인수로는 요소를 두개 이상 포함하는 [키,값]을 그 값으로 가지는 이터러블한 객체이다.

<code>Map</code>객체는 다음과 같은 <code>Map.prototype</code>의 프로퍼티와 메서드를 상속받는다.

- <code>clear()</code> : Map객체 안에 있는 모든 데이터를 삭제한다.
- <code>delete(key)</code> : Map객체에서 key가 가리키는 데이터를 삭제한다.
- <code>entries()</code> : Map객체가 가진 데이터(키-값) 값을 저장한 이터레이터를 데이터를 삽입한 순서대로 반환한다.
- <code>forEach(callback)</code> : Map객체의 모든 데이터를 대상으로 callback 함수를 실행한다. 이때 실행 순서는 데이터 삽입된 순서이고, 콜백함수의 인수는 currentValue, currentKey, currentMap 순으로 인수를 받는다.
- <code>get(key)</code> : Map객체에서 key가 가리키는 데이터를 반환한다.
- <code>has(key)</code> : Map객체에서 key가 가리키는 데이터가 있는지 논리값을 반환한다.
- <code>keys()</code> : Map객체에서 데이터 키를 값으로 가지는 이터레이터를 반환한다.
- <code>set(key, value)</code> : Map객체에 키가 key이고 값이 value인 데이터를 추가한다.
- <code>values()</code> : Map객체에서 데이터 값을 값으로 가지는 이터레이터를 반환한다.

```javascript
//첫번째 예제
const map = new Map([[0,'영'],[1,'일'],[2,'이']])
console.log(map) // Map(3) {0 => "영", 1 => "일", 2 => "이"}

map.forEach((v,k)=> {
    console.log(k+':'+v) // 0:영 1:일 2:이
}
const mapKey = map.keys()
for(let k of mapKey) console.log('keys',k) // keys 0 keys 1 keys 2

const mapValue = map.values()
for(let v of mapValue) console.log('values',v) // values 영 values 일 values 이

const mapEntrie= map.entries()
for(let e of mapEntrie) console.log('entries', e) //entries (2) [0, "영"] entries (2) [0, "일"] entries (2) [0, "이"]
```

첫번째 예제를 보면 알겠지만 배열로 키-값을 넣어도 배열처럼 인덱스를 지정해서 특정 키-값을 가져오거나 할수없다. 필요시엔 <code>forEach()</code>나 <code>for...of</code>를 이용하여 가져와야한다. 하지만 이번에 토이프로젝트를 하며 Map객체를 사용해 봤는데 다루기가 객체보다 편했다. 앞으로도 사용하고 싶은 의사가 UP중이다!

그리고 Map객체는 이터러블한 객체를 인수로 넘길 수 있으므로 제너레이터도 사용할 수 있다.



```javascript
//두번째 예제
function* makeData() {
	yield ['삼일절', '1919/3/1'];
	yield ['광복절', '1945/8/15'];
}
const datas = makeData();
const data = new Map(datas);
console.log(data) // Map(2) {"삼일절" => "1919/3/1", "광복절" => "1945/8/15"}
```





###  Set

Set객체는 중복되지 않는 유일한 데이터를 수집하여 활용하기 위한 객체이다. Set객체는 데이터 값의 단순 집합으로 간주하고 외부에서 키를 사용하여 데이터 값을 추가/삭제/검색할 수 있다. 값의 데이터 타입은 제한이 없고 인수를 넘기지 않으면 빈 Set객체가 생성된다.

```javascript
//첫번째 예제
const set = new Set();
console.log(set); // Set(0) {}
```

그리고 Map에서는 데이터를 추가할때 <code>set(key, value)</code>를 썼지만, Set에서는 <code>add(value)</code>프로퍼티를 이용하여 추가한다. 아래에 Set.prototype의 프로퍼티와 메소드를 상속받아 사용하는데 Set객체가 데이터 값만을 다루는데 굳이 값:값 형태로 나오게 key나 entries 메서드를 쓰는 이유는 Map객체와 형식을 통일 시키기 위해서다.





### WeakMap, WeakSet

Map객체와 Set객체는 **강력한 참조**를 가진다. 그래서 가비지컬렉터()가 수거할 수 없어서. 사용하지 않게되어도 메모리를 차지하며 메모리 누수(메모리릭)이 발생한다. 이를 보완하기 위해 WeakMap과 WeakSet이 나왔는데 이들의 키값은 **약한참조**를 가져서 더이상 사용하지 않을때나 참조가 끊어지는 순간 가비지 컬렉터가 쓸어담아 가게된다. 메모리누수를 보완하고 이와 같은 특징으로 인한 활용사례도 참고 링크에 나와 있으니 보면 좋을 것 같다. 그리고 WeakMap객체와 WeakSet객체는 Map객체와 Set객체처럼 열거할 수 없고, 사용할 수 있는 기능이 제한적이다.



### 언제 사용하면 좋을까?

그렇다면 모든 키-값 형태는 다 컬렉션을 사용해야 할까? 여러 케이스를 다루며 사용해 보지 않아서 이부분은 참고 링크에 나와있는 내용을 보는게 더 좋을것 같다



책에 나온 예제는 키값을 DOM객체를 연결해서 두더지잡기 게임만들기 였는데, 책의 예제를 적는건 큰 의미가 없을것 같고 나중에 다시 필요한 상황이 왔을때 참고해 보며 좋은 예제가 있다면 추후 추가하도록 하겠다.





##### 참고 링크

- <https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment>

* <https://beomy.tistory.com/18>
