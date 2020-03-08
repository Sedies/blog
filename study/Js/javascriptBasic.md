# Javascript Basic

#자바스크립트 기초 복습 내용 기록, #내가 중요하다 싶은 내용 기록, #내가 나중에 다시 보려고 기록

## 연산자

### 우선순위

- 맨 마지막은 ,(쉼표)연산자.
- 할당 연산자(=)는 모든 연산 순위에서 3번째로 느리다.
- +연산자는 단항연산자가 먼저 실행되고 그 후에 덧셈이 이루어진다.

### +/- 연산자

- +단항 연산자는 문자열을 숫자형으로 형변환 시킨다.
- +연산자는 피연산자에 문자열이 있으면 숫자형을 모두 문자형으로 변환하여 연산한다.
- -연산자는 피연산자에 문자열이 있을시 숫자형으로 변환한다.

### 비교연산자 (<, >, <=, >= , ==, !=, === , !==)

- 비교연산자는 피연산자의 형이 서로 다르면 숫자형으로 바꾼다.
- 단, <code>null</code>은 0, <code>undefined</code>는 NaN이 된다.
- ==(동등)연산자는 피연산자가 <code>undefined</code>나 <code>null</code>일때 형번환 하지 않는다.
- 단, <code>undefined</code>와 <code>null</code>을 비교할 때만 참, 그 외엔 거짓을 반환한다. (<code>undefined</code>는 숫자로 바꾸면 NaN, NaN은 <code>false</code>만 반환하고 <code>null</code> 또는 <code>undefined</code>와의 비교에서만 같다고 하므로)
- 문자열 비교 -> 유니코드순으로 비교(사전순 x)

### 비트연사자 (~, <<, >>, >>>)

- 비트연산자도 ~~를 문자형에 붙이면 +단항 연산자처럼 숫자형으로 변환시킨다.
- 단, 비트연산자는 32비트로 연산하므로 숫자크기 2^32-1 까지만 연산 가능하다.(21억 4700만)
- 오버플로우는 버리고, 대신 속도는 더 빠르다.

### 논리연산자

- OR(||) : 불리언으로 형변환하여 평가하며 <code>true</code>를 만나면 연산을 멈추고 원래 값을 반환. 하나라도 <code>true</code>면 <code>true</code>를 반환하며 모두 <code>false</code>이면 마지막 값을 반환.
- AND(&&) : 불리언으로 형변환하여 평가하며 <code>false</code>를 만나면 연산을 멈추고 원래값 반환, 하나라도 <code>false</code>면 <code>false</code>를 반환하며 모두 <code>true</code>이면 마지막 값을 반환.
- 우선순위는 AND(&&)가 OR(||)보다 높다.

## 조건문과 반복문

### 반복문

- 반목분이 한번 실행되는 것을 ineration이라고 한다.
- for(let i=0; i<10; i++) {} 에서 i를 인라인 변수 선언이라고 한다.

### 조건문

- 삼항연산자의 ? 오른쪽엔 <code>break</code>, <code>continue</code>가 올 수 없다.
- 레이블은 <code>break</code>이나 <code>continue</code>지시자 위에 있어야한다.
- <code>break</code>, <code>continue</code>는 반복문 안에서만 사용 가능하다.
- switch문은 일치 비교로 조건을 확인한다.
- case문에는 어떤 표현식이든 올 수 있다.
- default는 필수가 아니다.
- case문에 <code>break</code>이 없다면 다음 case문들도 다 실행 한다.
- case문은 묶을 수 있다.

```javascript
 case A:
 case B:
  /*실행 내용*/
  brack;
```

## 함수

### 함수

- 함수는 building blocks, action의 모음이라고도 한다.
- 반환값이 없거나, 값을 반환치 않을때 <code>undefined</code>를 반환한다.

### 함수명 패턴

- show~: 무언가 보여줌
- get~: 값을 반환함
- calc~: 무언갈 계산함
- create~: 무언갈 생산함
- check~: 무언갈 확인 후 불린값을 반환함
- is~: 무언가의 상태를 나타낼때, 불린값을 반환함
- self discribing code가 좋다.
