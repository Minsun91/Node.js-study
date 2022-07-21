## Q. 호이스팅과 TDZ는 무엇일까 ?

### 스코프, 호이스팅, TDZ
##### 스코프
식별자 접근 규칙에 따른 유효범위로, 선언 시점에 따라 전역/지역 변수로 나뉜다. 

 * Global Scope : 전역에 선언되어 있어 어디서든 변수에 접근 가능
 * Local Scope : 해당 지역에서만 접근 가능
** Local Scope은 Global Scope 보다 높은 우선순위


자바스크립트에서 모든 코드 블록(if, for, while, try/catch 등)이 지역 스코프를 만들며, 이러한 특성을 블록 레벨 스코프라 한다. 
하지만 var 키워드로 선언된 변수는 오로지 함수의 코드 블록만을 지역 스코프로 인정한다. 이를 함수 스코프라 한다.

* Var : function -scope
즉, var는 함수(){} 내에서 유효하다, for 문 끝난 다음에 i를 호출하면 값이 출력된다. 
```
for(var j=0; j<10; j++) {
  		console.log('j', j)}
	console.log('after loop j is ', j) // after loop j is 10
```

```
function counter () {
	for(var i=0; i<10; i++) {console.log('i', i)}}
counter()
console.log('after loop i is', i) // ReferenceError: i is not defined
```

* Let & Const : block - scope 
let은 변수에 재할당 가능/ const는 변수 재선언 및 재할당 불가능

##### 호이스팅 
* 함수가 실행되기 전에 함수 안의 변수값을 모두 모아서 유효 범위 최상단에 선언
* var변수 선언과 함수 선언문에서만 호이스팅이 일어난다. 
* Let/const 변수 선언과 함수 표현식에서는 호이스팅이 발생하지만, 할당되기 전까지 변수는 TDZ에 들어가있어 ReferenceError를 출력한다. 

##### TDZ (Temporal Dead Zone) 
Function{ 변수 선언 -> 변수 초기화 -> 변수 값 할당 } 
변수가 선언되고, 초기화가 이루어지기 전까지의 구간
* TDZ 에 영향을 받는 것 - let, const, class, class의 construction() 내부의 super(), 함수 매개변수
* TDZ에 영향 받지 않는 것 - var, function (함수 선언식), import 


### 함수 선언문과 함수 표현식에서 호이스팅 방식의 차이

함수 선언문은 function 함수명() {구현 로직} 으로 표현하고, 
함수 표현식은 var test1 = 1 function() {return ‘익명/기명 함수표현식’ } 표현할 수 있다. 

```javascript
function getName() {
    console.log('name');
} // 함수 선언문 -> 호이스팅 대상

var name = function() {
   console.log('name');
};// 함수 표현식 -> 호이스팅 X
```

* 함수 선언문에서는 아래 두 예제에서 에러 없이 값이 호출된다. 

```javascript
count();

function count() {
    console.log('count는 2이다.');
}
```
```javascript
function count() {
    console.log('count는 2이다.');
}
count();
```

* 함수 표현문에서는 에러/정상/에러가 발생한다. 

1)
```javascript
count();

var count = function() {
    console.log('count는 1이다.');
} //error : count is not function
```

2)
```
var count = function() {
    console.log('count는 1이다.');
}

count();
```

3)
```
count();

let count = function() {
    console.log('count는 1이다.');
} //Referrence Error
```

1) var 는 호이스팅의 영향을 받으므로 위로 끌어올려진다.
그래서 var count; 가 가장 먼저 실행되지만 변수에 아무 값도 담지 않았으므로 undefined 상태이다.
그 후로 count()가 호출되면 위에 선언한 count가 호출되므로 변수를 호출하는 격이된다.
그러므로 not function 이라는 에러 메시지가 나타난다.

2) var count가 호이스팅으로 인해 위로 끌어올려지지만, count() 호출 전 count에 함수를 담으므로
count()를 호출하였을 때 정상 작동한다. 

3) let 은 호이스팅의 영향을 받지 않기 때문에, 예시에 작성한 코드 순서대로 실행된다.
그러므로 count()라는 함수가 정의되지 않았는데 호출하였기 때문에 에러가 발생한다.


### let, const, var, function의 작동 원리
![image]("https://stephaniejoymills.com/dark-table-5ec7c8c60d7f366b7812e214d58a3c3d.svg")

### 실행 컨텍스트와 콜 스택
##### 실행 콘텍스트 (Record/outer)
코드를 실행하는데 필요한 환경을 제공하는 객체

##### 콜 스택
콜 스택은 프로그램을 실행할 때 현재 실행 중인 함수가 가장 위에 쌓이고 그 함수의 실행이 끝나면 사라지는 스택 자료구조
프로그램이 시작되면 콜 스택에 함수들이 쌓이고, 가장 최근에 호출되어 쌓인 순서대로 함수들이 종료되면서 스택이 모두 비어지면 프로그램이 끝난다. 

### 스코프 체인, 변수 은닉화
### 스코프 체인 
변수를 참조할 때 js는 스코프 체인을 통해 변수를 참조.
변수가 해당 지역에 없다면, 상위 스코프로 올라가면서 변수를 참조한다. 

![image]("https://github.com/Minsun91/Node.js-study/issues/1#issue-1312274026")

### 변수 은닉화
외부에서 임의로 해당 속성의 값을 변경하지 못하도록 하는 것
변수명 앞에 underscore(_ )를 포함하면 그 변수는 Private variable이 되지만 접근 가능하기 때문에 클로저를 사용한다. 
 _클로저는 외부 변수를 기억하고 이 외부 변수에 접근할 수 있는 함수를 의미하며, 외부 함수와 연결되어 있기 때문에 값이 동적으로 바뀌어도 반영된다_

```
var click = (function () {
  // 클릭한 횟수를 기억
  var count = 0;
  return function () {
    ++count;
    return count;
  };
})();

// 버튼을 누를 때 마다 누른 횟수 출력
function print() {
  console.log(click());
}
```

print 함수 안에 있는 click 함수는 이름이 없는 클로저를 반환하고 호출한다. (변수 은닉)
클로저는 click 함수의 count변수 값을 계속 기억하고 있으므로 버튼을 누른 횟수를 출력이 가능하다. 

