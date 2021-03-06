# 0513 execution context & closure

소스 코드 타입 분류

- 전역 코드
- 함수 코드
- eval 코드
- 모듈 코드


<br>

if, for 문 등이 없는 이유는 실행 컨텍스트를 생성하지 않기 때문

<br>

구분하는 이유는 소스 코드의 타입에 따라 실행 컨텍스트를 생성하는 과정과 관리 내용이 다르기 때문

<br>

모든 소스 코드는 실행에 앞서 평가 과정을 거치며 코드 실행을 준비한다.

자바스크립트 엔진은 모든 코드를 평가와 실행으로 나누어 처리.

-> 소스 코드의 평가 과정이 끝나면 (선언문을 제외한) 소스 코드가 '순차적'으로 실행 = 런타임 시작

**코드가 실행되려면 아래와 같이 스코프, 식별자, 코드 실행 순서 등의 관리가 필요하다.**

**실행 컨텍스트(execution context)는 소스 코드를 실행하기 위해 필요한 환경을 제공하고 코드의 실행 결과를 실제로 관리하는 영역이다.**

<br>

**실행 컨텍스트는 식별자(변수, 함수, 클래스 등의 이름)를 등록하고 관리하는 스코프와 코드 실행 순서 관리를 구현한 내부 매커니즘으로 모든 코드는 실행 컨텍스트를 통해 실행되고 관리된다.**

<br>

스 코드가 평가되면 실행 컨텍스트가 생성되고 실행 컨텍스트 스택의 최상위에 쌓인다. **실행 컨텍스트 스택의 최상위에 존재하는 실행 컨텍스트는 언제나 현재 실행 중인 코드의 실행 컨텍스트이다.** 따라서 실행 컨텍스트 스택의 최상위에 존재하는 실행 컨텍스트를 **실행 중인 실행 컨텍스트(running execution context)**라 부른다.



```javascript
let x = 1;
var x = 10;
//error 서로 등록되는 환경이 달라서 어떤 x를 찾아야 할지 모르기 때문에
```

<br>
전역 객체가 없어지지 않는 이유 : widnow라는 이름이 존재하며, 애플리케이션과 생애 주기를 같이한다.

함수 코드가 실행되고(호출되고) 함수 객체를 평가할 때 this 바인딩

```javascript
let x = 1;
if(true){
	console.log(x);
}// 블록문은 실행 컨텍스트를 생성시키는 게 아니라 block lexical environment를 생성시킨다
// 모든 코드 블록이 실행 컨텍스트를 만드는 것은 아니다.
```

클로저가 어렵다? -> 실행 컨텍스트에 대한 이해가 부족한 것이다.

-> 함수형 프로그래밍 언어에 사용되는 중요한 특성

>클로저란 함수와 그 함수가 선언된 렉시 컬 환경과의 조합이다

함수가 선언된 렉시 컬 환경 = 함수와 함수의 상위 스코프 이야기

함수의 정의된 위치, 스코프

<br>

함수 객체의 내부 슬롯 [[environment]] 왜?

-> 자바스크립트 모든 함수는 클로저인가? -> 일반적으로 클로저라고 할 수 있으나 통상적으로 클로저라 하지는 않는다.

클로저의 조건

1. 외부함수 보다 중첩 함수가 더 오래 생존
2. 1의 조건을 만족하는 중첩 함수가 외부의 식별자를 참조

중첩 함수가 갖고 있는 상위 스코프를 클로저라고 한다(목적은 상태를 안전하게 유지하기)

<br>

함수가 태어나자마자 자신의 상위 스코프를 기억하고 있으며 =([[Environment]]) 고정되어 있고 (정적 스코프) Function.Environment 어디서 호출되는가는 의미 없다.



