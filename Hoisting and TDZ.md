## Q. 호이스팅과 TDZ는 무엇일까 ?

### 스코프, 호이스팅, TDZ
##### 스코프
식별자 접근 규칙에 따른 유효범위로, 선언 시점에 따라 전역/지역 변수가 나뉜다
 * Global Scope : 전역에 선언되어 있어 어디서든 변수에 접근 가능
 * Local Scope : 해당 지역에서만 접근 가능

Var : function -scope
즉, var는 함수() {} 내에서 유효하다, for 문 끝난 다음에 i를 호출하면 값이 출력된다. 
ex) for(var j=0; j<10; j++) {
  		console.log('j', j)}
	console.log('after loop j is ', j) // after loop j is 10

ex) function counter () {
	for(var i=0; i<10; i++) {console.log('i', i)}}
counter()
console.log('after loop i is', i) // ReferenceError: i is not defined

Let & Const : block - scope 
let은 변수에 재할당 가능/ const는 변수 재선언 및 재할당 불가능

함수 호이스팅도 가능한데, 함수만 끌어올리고 변수 값은 그대로
ex) sayhello();  //hello
	function sayhello() {console.log(‘hello’);}
위 예시대로 작동시키면 sayhello라는 함수를 선언하기 전에 함수코드를 실행시켰지만, hello가 출력된다. 
이유는 js에서 함수 선언을 호이스팅하여 global 객체에 등록시키기 때문이다. 

** Local Scope은 Global Scope 보다 높은 우선순위

##### 호이스팅 
* 실행되기 전에 함수 안에 필요한 변수값을 모두 모아서 유효 범위 최상단에 선언
* var변수 선언과 함수 선언문에서만 호이스팅이 일어난다. 
* Let/const 변수 선언과 함수 표현식에서는 호이스팅이 발생g하지만 .. 할당되기 전까지 변수는 TDZ에 들어가있어 ReferenceError를 출력한다. 

##### TDZ (Temporal Dead Zone) 
Function{ 변수 선언 -> 변수 초기화 -> 변수 값 할당 } 
변수가 선언되고, 초기화가 이루어지기 전까지의 구간
* TDZ 에 영향을 받는 것 - let, const, class, class의 construction() 내부의 super(), 함수 매개변수
* TDZ에 영향 받지 않는 것 - var, function (함수 선언식), import 


### 함수 선언문과 함수 표현식에서 호이스팅 방식의 차이
함수 선언문은 function 함수명() {구현 로직}
함수 표현식은 var test1 = 1 function() {return ‘익명/기명 함수표현식’ } 

### 여러분이 많이 작성해온 let, const, var, function 이 어떤 원리로 실행되는지 알 수 있어요.

### 실행 컨텍스트와 콜 스택
##### 실행 콘텍스트 (Record/outer)
코드를 실행하는데 필요한 환경을 제공하는 객체

##### 콜 스택:
콘텍스트들이 담겨있는 곳으로, 최근에 추가된 실행 콘텍스트만 활성화 됨

### 스코프 체인, 변수 은닉화
### 스코프 체인 
변수를 참조할 때 js는 스코프 체인을 통해 변수를 참조.
변수가 해당 지역에 없다면, 상위 스코프로 올라가면서 변수를 참조한다. 
[스코프체인](file:///Users/minsun/Desktop/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%A9%E1%84%91%E1%85%B3%E1%84%8E%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AB.png)

### 변수 은닉화
