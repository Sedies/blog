# JS 기본 오류 7가지

참고링크 보고 한글로 간단 내용정리

### 1. 범위오류 Range Error

### 2. 참조오류 Reference Error

- 존재하지 않는 변수나 항목을 참조하려하거나
- 참조가 깨졌을 때
- 환경 레코드에서 찾을 수 없을때

### 3. 문법오류 Syntax Error

-구문 분석중 JS엔진에서 일어남

- 토큰화, 파싱, 인터프리팅 과정 중 토근화와 파싱 단계에서 구문 규칙이 어긋나면 스테이지 실패로 Error발생

### 4. 타입오류 Type Error

- 실패원인을 나타내는 적절한 기본 오류 유형이 없을때
- 예) 잘못된 테이터 유형일때

### 5. URI오류 URI Error

- 전역 URI 처리 기능 중 하나가 해당 정의와 호환되지 않는 방식으로 사용되었을때 //(?)
- URI를 인코딩하거나 디코딩 할때 문제가 있는 경우 발생

### 6. 평가오류 Eval Error

-전역 eval() 함수를 사용할 때 오류를 식별하는데 사용

### 7. 내부오류 Internal Error

-처리할 데이터가 너무 많고 스택이 임계 한계를 초과하였을때 JS엔진 내부에서 발생

- 예) 너무 많은 재귀, 너무 많은 스위치 케이스 등

<br>
<br>
<br>
##### 참고링크
- [7 Types of Native Errors in JavaScript You Should Know](https://blog.bitsrc.io/types-of-native-errors-in-javascript-you-must-know-b8238d40e492)
