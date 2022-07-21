## 기본형 데이터와 참조형 데이터
참고) https://hwb0218.tistory.com/41

### 💡 데이터의 두 가지 타입
원시 자료형(primitive type)과 참조 자료형(reference type)이 있다.
* 원시 자료형이 할당될 때에는 변수에 값(value) 자체가 담긴다.
* 참조 자료형이 할당될 때는 보관함의 주소(reference)가 담긴다.

### 💡 원시 자료형 (Primitive data type) = 원시타입, 기본형 데이터
* 기본형 데이터가 할당된 변수는 자기 자신만의 고유한 값을 가진다.
▶ 기본형 데이터는 변경 불가능한 값. 한 번 생성된 기본형 데이터는 변경할 수 없다(불변성)
▶ 기본형 데이터를 할당한 변수는 재할당 이외에는 변수값을 변경할 수 없다.
▶ 객체가 아니면서 method를 가지지 않는 6가지의 기본형 데이터 타입이 있다.
string, number, boolean, undefined, symbol, (null은 원시 타입과 거의 같게 사용 되지만 엄밀히 따지면 객체이다. 빈 참조를 나타내는 데 자주 사용된다.)

number : 3.141592
string : ‘3.141592’
boolean : true & false
undefined : 변수가 정의되지 않았거나 값이 없다.
null : 의도적으로 비어있음을 표현하기 위해 null 이라는 것이 들어있다.
symbol(ES6부터 추가됨, 객체 속성을 만드는 데이터 타입)
### 💡 참조 자료형 (Reference data type) = 참조타입
▶ 자바스크립트에선 원시 자료형이 아닌 모든 것은 참조 자료형.
▶ 참조 자료형은 기존에 고정된 크기의 보관함이 아니다.
▶ 참조 자료형을 변수에 할당할 때는 변수에 값이 아닌 주소를 저장한다.
▶ 동적으로 크기가 변하는 데이터를 보관하기 위해 변수가 아닌 다른 곳에 데이터를 저장하고 변수에는 그 주소만 할당한다.
▶ 참조형은 원시형 데이터의 집합. 배열([])과 객체({}), 함수(function(){})가 대표적

배열 Array : [0,1,2,3,4]
객체 Object {name : “John”, age : 16}
함수 function
정규표현식 RegExp
2) JavaScript 형 변환
자바스크립트는 타입이 매우 유연한 언어이다. 때문에 자바스크립트 엔진이 필요에 따라 암시적변환을 혹은 개발자의 의도에 따라 명시적변환을 실행한다.

### 💡 암시적 형 변환(Implicit type conversion)
자바스크립트 엔진이 필요에 따라 자동으로 데이터 타입을 변환시키는 것이다.

1) 산술연산자
더하기(+) 연산자는 숫자형보다 문자형이 우선시되기 때문에, 숫자형이 문자형을 만나면 문자형으로 변환하여 연산된다.

```
number + number // number
number + string // string
string + string // string
string + boolean // string
number + boolean // number
50 + 50; //100
100 + “점”; //”100점”
“100” + “점”; //”100점”
“10” + false; //”100"
99 + true; //100
```

다른 연산자(-,*,/,%)는 숫자형이 문자형보다 우선시되기 때문에 더하기와 같은 문자형으로의 변환이 일어나지 않는다.
```
//다른 연산자(-,,/,%)
string number // number
string string // number
number number // number
string boolean //number
number boolean //number
“2” false; //0
2 true; //2
```

2) 동치비교
아래 예제는 엄격하지 않은 동치(==)비교이며, 아래의 결과값은 좌우항 변환할 경우 모두 '0==0이기 때문에' 'true'이다.

```
null == undefined // true 0 == 0
“0” == 0 // true 0 == 0
0 == false // true 0 == 0
“0” == false // true 0 == 0
```

여기서 유의해야할 점은 위의 비교는 엄격하지 않은 동치 비교일 경우이기 때문에, 두 값을 비교할때 데이터타입을 변환하지 않는 엄격한 동치(===)비교와 혼동되지 않도록 한다.

### 💡 명시적 형 변환(Explicit Type Conversion)
명시적 변환이란 개발자가 의도를 가지고 데이터 타입을 변환시키는 것이다.

타입을 변경하는 기본적인 방법은 Object(), Number(), toString(), Boolean() 와 같은 함수를 이용하는데 new 연산자가 없다면 사용한 함수는 타입을 변환하는 함수로써 사용된다.

```
var trans = 100; //Number
Object(trans); //100
console.log(typeof trans); //Number
toString(trans); //”100"
console.log(typeof trans); //String
Boolean(trans); //true
console.log(typeof trans); //Bolean
```

1) A Type → Number Type
다른 자료형을 숫자타입으로 변형하는 방법은 아래와 같다.

Number()
Number()는 정수형과 실수형의 숫자로 변환한다. 보통 문자형을 숫자형으로 변경할때 사용한다. 숫자로 변환되지 않는 경우에는 NaN(Not a Number)을 반환한다.

Number(“12345”); //12345
Number(“2”*2); //4

펄시한 값(falsy values : null, false,"빈문자열")에 대해서는 0으로 표현.
트루시한 값(truthy values)에 대해서는 1로 표현.
array의 경우는 Number()함수에서 사용하는 0을 반환.

const falsy1 = null;
Number(falsy1); // 0;

const falsy2 = '';
Number(falsy2); // 0;

const falsy3 = false;
Number(falsy3); // 0;

const truthy1 = [];
Number(truthy1); // 0;

const truthy2 = true;
Number(truthy2); // 1;

const truthy3 = {};
Number({}); // NaN;

parseInt()
parseInt()는 정수형의 숫자로 변환한다. 만약 문자열이 '숫자0'으로 시작하면 8진수로 인식하고, '0x, OX'로 시작한다면 해당 문자열을 16진수 숫자로 인식한다. 또한 앞부분 빈 공백을 두고 나오는 문자는 모두 무시되어 NaN을 반환한다.

```
parseInt(“27”) //27
parseInt(0033); //27
parseInt(0x1b); //27
parseInt(“ 2”); //2
parseInt(“ 2ㅎ”); //2
parseInt(“ ㅎ2”); //NaN
```

parseFloat()
parseFloat()는 부동 소수점의 숫자로 변환한다. parseInt()와는 달리 parseFloat()는 항상 10진수를 사용하며 parseFloat() 또한 앞부분 빈 공백을 두고 나오는 문자는 모두 무시되어 NaN을 반환한다.

```
parseFloat(“!123”); //NaN
parseFloat(“123.123456”); //123.123456
parseInt(“123.123456”); //123
parseFloat(“ 123.123456”); //123.123456
parseFloat(“ a123.123456”); //NaN
```

단항연산자(unary-operators)로 숫자형 타입 변경

+'1000'; // 1000
+'-1000'; // -1000
+'Infinity'; // Infinity
-'1000'; // -1000
+true; // 1
+[]; /// 0
+false; // 0
+null; // 0
+'';// 0

위 예제를 보면 단일 연산자를 이용한 숫자형 변환은 Number와 동일한 동작을 하는 것을 볼 수 있다. 자바스크립트 함수를 사용하지 않고 타입변환을 할 수 있는 쉽고 효율적인 방법.

2) A Type → String Type
다른 자료형을 문자타입으로 변형하는 방법은 아래와 같다.

String()

String(123); //”123"
String(123.456); //”123.456"

toString()
주어진 값을 문자열로 변환 후 반환. toString()는 인자로 기수를 선택할 수 있다. 인자를 전달하지 않으면 10진수로 변환한다.

```
var trans = 100;
trans.toString(); //”100"
trans.toString(2); //”1100100"
trans.toString(8); //”144"
var boolT = true;
var boolF = false;
boolT.toString(); //”true”
boolF.toString(); //”false”
```

toFixed()
toFixed()의 인자를 넣으면 인자값만큼 반올림하여 소수점을 표현하며 소수점을 넘치는 값이 인자로 들어오며 '0'으로 길이를 맞춘 문자열을 반환한다.

```
var trans = 123.456789;
var roundOff = 99.987654;
trans.toFixed(); //”123"
trans.toFixed(0); //”123"
trans.toFixed(2); //”123.46"
trans.toFixed(8); //”123.45678900"
roundOff.toFixed(2); //”99.99"
roundOff.toFixed(0); //”100"
```

3) A Type → Boolean Type
자바스크립트에서는 Boolean타입으로 변경은 Boolean 또는 부정연산자(!)를 사용하여 Boolean값을 만들어낸다. 부정연산자는 의미그대로 !을 사용하면 Boolean() 반대의 값을 리턴한다.

다른 자료형을 불린타입으로 변형하는 방법은 아래와 같다.

Boolean()

```
Boolean(100); //true
Boolean(“1”); //true
Boolean(true); //true
Boolean(Object); //true
Boolean([]); //true
Boolean(0); //false
Boolean(NaN); //false
Boolean(null); //false
Boolean(undefined); //false
Boolean( ); //false
const numb1 = 0;
Boolean(numb1); // false
!!numb1; // false
!numb1; // true
```

## 3) 불변 객체를 만드는 방법
### 💡 불변 객체 (Immutable Object)
객체 내부 프로퍼티를 변경할 때마다 새로운 객체를 만들어 재할당하기로 정하거나
자동으로 새로운 객체를 만드는 도구를 활용하여 (ex. immutable.js, immer.js 등의 라이브러리) ➡불변성 확보

### 💡 불변 객체가 필요한 경우
객체에 변화를 가해도 원본이 그대로 남아있어야 하는 경우
ex) 정보가 바뀌었으면 알림 전송하는 경우, 바뀌기 전의 정보와 바뀐 후의 정보를 보여줘야하는 경우 등

```
var user = {
name: "namju",
gender: "male",
};
var changeName = function (user, newName) {
var newUser = user;
newUser.name = newName;
return newUser;
};
var user2 = changeName(user, "yun");
// 아래의 if문은 무시되어 지나침
if (user !== user2) {
console.log("유저 정보가 변경되었습니다.");
}
console.log(user.name, user2.name); // yun yun
console.log(user === user2); // true
```

💡 불변 객체 만들기
새 객체를 하드코딩

```
var user = {
name: "namju",
gender: "male",
};
var changeName = function (user, newName) {
return {
name: newName,
gender: user.gender,
};
};
var user2 = changeName(user, "yun");
if (user !== user2) {
console.log("유저 정보가 변경되었습니다."); // 유저 정보가 변경되었습니다.
}
console.log(user.name, user2.name); // namju yun
console.log(user === user2); // false
```

➡ 객체에 프로퍼티가 많을수록 하드코딩해야하는 수고가 너무 늘어남
프로퍼티 개수에 상관 없이 모든 프로퍼티를 복사하는 함수를 만드는 것이 좋음

## 4) 얕은 복사와 깊은 복사
### 💡 얕은 복사
바로 아래 단계의 값들만 복사하는 방법
: for in 반복문으로 새 객체에 원래 객체의 프로퍼티들을 복사하는 함수

```
var copyObject = function (target) {
var result = {};
for (var prop in target) {
result[prop] = target[prop];
}
return result;
};
```

이 함수를 이용해 새로운 객체를 만들어 프로퍼티를 변경할 수 있음

```
var user = {
name: "namju",
gender: "male",
};
var user2 = copyObject(user);
user2.name = "yun";
if (user !== user2) {
console.log("유저 정보가 변경되었습니다."); // 유저 정보가 변경되었습니다.
}
console.log(user.name, user2.name); // namju yun
console.log(user === user2); // false
```

이 방법의 단점

프로토타입 체이닝 상의 모든 프로퍼티를 복사
getter / setter는 복사하지 않음
얕은 복사만 수행함
➡ 협업하는 모든 개발자들에게 무조건 copyObject 함수를 사용하기로 합의시키는 것이 어려움!
프로토타입 체이닝
모든 객체(함수 포함)에는 프로토타입 객체가 포함되어 있음
그렇기 때문에 얕은 복사를 한 객체는 부모(원본) 객체의 프로토타입에도 접근할 수 있음 (스코프 체이닝처럼 계속 상위로 가서 탐색을 하는 식)

### 💡 깊은 복사
내부의 모든 값들을 하나하나 찾아서 전부 복사하는 방법

얕은 복사만으로는 중첩된 객체를 제대로 복사할 수 없음 (바로 아래 단계의 값들만 새로운 데이터 주소로 복사시키는 것)

한 단계 더 nesting 된 info 객체의 프로퍼티들에는 기존의 데이터를 그대로 참조하고 있는 것! ➡이런 nested 된 모든 프로퍼티들에 대한 복사를 재귀적으로 수행해야 깊은 복사가 됨

```
var user = {
name: "namju",
info: {
hobby: "bike",
location: "seoul",
happy: true,
},
};
var user2 = copyObject(user);
user.name = "yun namju";
user.info.hobby = "read";
user.info.location = "busan";
console.log(user.name === user2.name); // false
console.log(user.info.hobby === user2.info.hobby); // true : 두 객체가 모두 변경됨
console.log(user.info.location === user2.info.location); // true : 두 객체가 모두 변경됨
```

객체의 깊은 복사를 수행하는 함수

```
var copyObjectDeep = function (target) {
var result = {};
if (typeof target === "object" && target !== null) {
for (var prop in target) {
result[prop] = copyObjectDeep(target[prop]); // 재귀적 호출
}
} else {
result = target;
}
return result;
};
```

➕ hasOwnProperty 메서드를 통해 프로토타입 체이닝을 통해 상속된 프로퍼티는 복사하지 않도록 할 수 있음
➕ ES6, ES2017의 경우 Object.getOwnPropertyDescriptor, Object.getOwnPropertyDescriptors를 통해 getter/setter를 복사할 수 있음
