# Intermediate - JS
> 출처 [자바스크립트 중급 강좌](https://youtu.be/4_WLS9Lj6n4)을 보고 정리한 내용.
________

## 목차

- [변수](#변수)
- [생성자 함수](#생성자-함수)
- [객체 메소드(object methods), 계산된 프로퍼티(Computed property)](#객체-메소드-계산된-프로퍼티)
- [심볼(Symbol)](#심볼(Symbol))
- [숫자, 수학 method (Number, Math)](#숫자-수학)
- 문자열 메소드 (String methods)
- 배열 메소드 1(Array methods)
- 배열 메소드 2(sort, reduce)
- 구조 분해 할당 (Destructuring assignment)
- 나머지 매개변수, 전개 구문(Rest parameters, Spread s)
- 클로저(Closure)
- setTimeout / setInterval
- call, apply, bind
- 상속, 프로토타입(Prototype)
- 클래스(class)
- 프로미스(Promise)
- async, await
- Generator
<br/>
<br/>
_____

## 변수

- **let**
```javascript
let name = 'Mike';
console.log(name); //Mike

let name = 'Jane';
console.log(name); // error!
```

- **const**
```javascript
let name;
name = 'Mike';

let age;
age = 30;

const gender;
gender = 'male'; //error! 선언하면서 할당을 안했기 때문
```

- **var**
<br>한번 선언된 변수를 다시 선언할 수 있다
```javascript
var name = 'Mike';
console.log(name); //Mike

var name = 'Jane';
console.log(name); //Jane
```
<br>선언하기 전에 사용할 수 있음
```javascript
console.log(name); //undefined
var name = 'Mike';

//위를 
//var name; (호이스팅(hoisting))
//console.log(name); //undefined :선언은 호이스팅이 되지만 할당은 호이스팅이 안되기 때문
//name = 'Mike'; //할당
//로 동작하기 때문
```

- **호이스팅(hoisting)**
<br>let, const, var 모두 호이스팅 됨
<br>스코프 내부 어디서든 변수 선언은 최상위에 선언된 것 처럼 행동
<br>error를 내는 이유는 TDZ(Temporal Dead Zone)때문
    - TDZ영역에 변수들은 사용할 수 없음
    - let, const는 TDZ의 영향을 받음
    - 할당을 하기 전엔 사용할 수 없음

- **변수의 생성과정**
<br>1. 선언 단계
<br>2. 초기화 단계 (초기화 : undefined를 할당 해주는 단계)
<br>3. 할당 단계
```
var는 선언과 초기화가 동시에 되서 할당 전에 호출하면 에러가 뜨지 않고 undefined

let 은 선언단계와 초기화 단계분리되어 진행됨
호이스팅 되면서 선언단계가 이루어지지만, 초기화 단계는 실제 코드에 도달했을때 진행되기 때문에 레퍼런스 에러가 발생

let 과 var는 선언만 해두고 나중에 할당하는 것을 허용하지만,
const 선언과 할당이 동시에 되어야함
```

- **스코프**
<br/>var : 함수 스코프(function-scoped)
  - 함수 스코프 : 함수 내에서 선언된 변수 만 그 지역변수가 됨

  <br/>let, const : 블록 스코프(block-scoped)
  - 블록 스코프 : 모든 코드 블록에서 선언된 변수는 코드 블록 내에서만 유효하며, 외부에서는 접근할 수 없다는 의미.
  - 즉, 코드 블록 내부에서 선언한 변수는 지역변수
  - 코드블록은 함수, if문, for문, while문, try/catck문 등을 의미
```javascript
const age = 30;

if(age > 19) {
  var txt = '성인';
}
console.log(txt); //성인

//if문 안에서 var로 선언한 변수는 if문 밖에서도 사용 가능
//하지만 let, const는 중괄호 내부에서만 사용 가능(블록스코프)

function add(num1, num2) {
  var result = num1 + num2;
}
add(2,3);
console.log(result); //error!
//var도 함수 내부에서 선언되면 함수를 함수 밖에서 사용할 수 없음
//유일하게 벗어날 수 없는 스코프가 함수라고 생각하기
```
_____

## 생성자 함수

```javascript
//생성자 함수는 첫글자는 대문자로
function User(name, age) {
  this.name = name;
  this.age = age;
}
let user1 = new User('Mike', 30); //User{name:'Mike', age:30}
let user2 = new User('Jane', 22); //User{name:'Jane', age:22}
let user3 = new User('Tom', 17); //User{name:'Tom', age:17}
```
```javascript
//메소드 추가
function User(name, age) {
  this.name = name;
  this.age = age;
  this.sayName = function(){
    console.log(this.name);
  }
}
let user5 = new User('Han', 40);
user5.sayName(); //'Han'
```
<br>예제
```javascript
// 생성자 함수 : 상품 객체를 생성
function Item(title, price){
  // this = {};
  this.title = title;
  this.price = price;
  this.showPrice = function() {
    console.log(`가격은 ${price}원 입니다.`);
  }
  // return this;
}
const item1 = new Item('인형', 3000); //new 안붙이면 undefined
const item2 = new Item('가방', 4000);
const item3 = new Item('지갑', 5000);

console.log(item1, item2, item3);
//Item{title:'인형', price:3000, showPrice: 함수}
//Item{title:'가방', price:4000, showPrice: 함수}
//Item{title:'지갑', price:5000, showPrice: 함수}

item3.showPrice(); //가격은 5000원 입니다.
```
____

## 객체 메소드, 계산된 프로퍼티

- **계산된 프로퍼티(Computed property)**
```javascript
let a = 'age';
const user = {
  name : 'Mike',
  [a] : 30 //age : 30
}
```
<br>예제
```javascript
function makeObj(key, val){
  return {
    [key] : val
  }
}

const obj = makeObj("성별", "male");

console.log(obj); //{성별: "male"}
//어떤게 키가 될지 모르는 객체를 만들때 유용
```
<br/>

- 객체 메소드(object method)
  - **Object.assign()**
  <br>Object.assign(): 객체 복제
  ```javascript
  const user = {
    name : 'yoon',
    age : 30
  }
  const newUser = Object.assign({}, user);
  //{}빈 객체는 초기값. 두번째 매개 변수부터 들어온 객체들이 초기값에 병합 됨
  newUser.name = 'Tom';
  console.log(user.name); //'yoon' 이름을 바꿔도 변함 없음
  newUser != user

  //만약
  Object.assign({name:'Tom'}, user);
  //을 하면 name:'yoon', age:30 으로 덮어 쓰게 됨
  ```

  <br/>예제
  ```javascript
  const user = {
    name: 'yoon'
  };
  const user2 = Object.assign({}, user);
  user2.name = 'jane';

  console.log(user); //{name: 'yoon'}
  console.log(user2); //{name: 'jane'}
  ```

  - **Object.keys()**
  <br>Object.keys(): 키 배열 반환
  ```javascript
  const user = {
    name : 'yoon',
    age : 30,
    gender : 'female'
  }

  Object.keys(user); //["name","age","gender"]
  ```

  <br/>예제
  ```javascript
  const user = {
    name: 'yoon',
    age: 30
  };
  const result = Object.keys(user);

  console.log(result); //['name', 'age']
  ```

  - **Object.values()**
  <br>Object.values(): 값 배열 반환
  ```javascript
  const user = {
    name : 'yoon',
    age : 30,
    gender : 'female'
  }

  Object.values(user); //["yoon",30,"female"]
  ```
  <br/>예제
  ```javascript
  const user = {
    name: 'yoon',
    age: 30
  };
  const result = Object.values(user);

  console.log(result); //['yoon', 30]
  ```

  - **Object.entries()**
  <br>Object.entries(): 키/값 배열 반환
  ```javascript
  const user = {
    name : 'yoon',
    age : 30,
    gender : 'female'
  }

  Object.entries(user); //[["name","yoon"],["age",30],["gender","female"]]
  ```
  <br/>예제
  ```javascript
  const user = {
    name: 'yoon',
    age: 30
  };
  const result = Object.entries(user);

  console.log(result); //(2) [Array(2), Array(2)]
  ```

  - **Object.fromEntries()**
  <br>Object.fromEntries(): 키/값 배열을 객체로
  ```javascript
  const arr = [
    //["키", "값"]
    ["name","yoon"],
    ["age",30],
    ["gender","female"]
  ];

  Object.fromEntries(arr); // {name : 'yoon', age : 30, gender : 'female'}
  ```

  <br/>예제
  ```javascript
  let arr = [
    ['mon', '월'],
    ['tue', '화']
  ]
  const result = Object.fromEntries(arr);

  console.log(result); //{mon: '월', tue: '화'}
  ```

_____

## 심볼(Symbol)

- **property key: 문자형**
<br>1. 유일한 식별자를 만들 때 사용
```javascript
const a = Symbol(); //new를 붙이지 않음!
const b = Symbol();

console.log(a) //Symbol()
console.log(b) //Symbol()
//생긴건 똑같지만
//a === b; false
//a == b; false
```
<br>2. 유일성 보장
```javascript
const id = Symbole('id'); //설명을 붙여주면 디버깅하기 편함
const id2 = Symbole('id');

//id, id2 모두 생긴건 똑같ㅈ미ㅏㄴ
//id === id2 false
//id == id2 false
```

- **property key: 심볼형**
```javascript
const id = Symbol('id');
const user = {
  name : 'Mike',
  age: 30,
  [id]: 'myid'
}

//user -> {name:'Mike', age: 30, symbol(id): 'myid'}
user[id] //'myid'


//Object.keys(user); ["Mike", "age"]
//Object.values(user); ["Mike", 30]
//Object.entries(user); [Array(2), Array(2)] 등
//키가 심볼형인 프로퍼티는 건너 뜀
```

- **Symbol.for() : 전역 심볼**
    - 하나의 심볼만 보장받을 수 있음
    - 없으면 만들고, 있으면 가져오기 때문
    - Symbol 함수는 매번 다른 Symbol 값을 생성하지만, 
    - Symbol.for 메소드는 하나를 생선한 뒤 키를 통해 같은 Symbol을 공유
    ```javascript
    const id1 = Symbole.for('id');
    const id2 = Symbole.for('id');

    id1 === id2; //true
    Symbol.keyFor(id1) //"id"
    //전역 심볼이 아닌 심볼은 keyfor을 사용할 수 없음
    const id = Symbol('id 입니다.');
    id.description; //"id 입니다." 대신 description으로 알 수 있음
    ```
_____

## 숫자, 수학

- **toString()**
<br> 10진수 -> 2진수/16진수
```javascript
let num = 10;
num.toString(); //'10'
num.toString(2); //2진수로 변환 '1010'

let num2 = 255;
num2.toString(16); //16진수로 변환 'ff'
```

- **Math**
```javascript
//대표적인 프로퍼티 예
Math.PI; //3.141592653589793 (원주율)
```

- **Math.ceil()**
<br>올림
```javascript
let num1 = 5.1;
let num2 = 5.7;

Math.ceil(num1); //6
Math.ceil(num2); //6
```

- **Math.floor() : 내림**
```javascript
let num1 = 5.1;
let num2 = 5.7;

Math.floor(num1); //5
Math.floor(num2); //5
```

- **Math.round() : 반올림**
```javascript
let num1 = 5.1;
let num2 = 5.2;

Math.round(num1) //5
Math.round(num2) //6
```
- **소수점 자릿수**
```javascript
//요구사항 : 소수점 둘째자리까지 표현(셋째 자리에서 반올림)
let userRate = 30.1234;

1. userRate * 100 //'3012.34' (100을 곱하고)
2. Math.round(userRate * 100) //'3012' (반올림을 해준 뒤)
3. Math.round(userRate * 100)/100 //'30.12' (다시 100을 나눠 줌)

그러면 요구사항은 30.12
```
<br>OR

- **소숫점 자릿수 : toFixed()**
<br>숫자를 인수로 받아 그 숫자만큼 소수점 이하 갯수에 반영
<br>주의: 문자열로 반환. 그래서 반환받은 이후, Number을 이용해 숫자로 변환 후 작업
```javascript
//요구사항 : 소수점 둘째자리까지 표현(셋째 자리에서 반올림)
let userRate = 30.1234;

userRate.toFixed(2); //'30.12'
//숫자변환
Number(userRate.toFixed(2)); //30.12

만약
userRate.toFixed(0); //0일 경우 정수만 남음 '30'
userRate.toFixed(6);
//기존 소수 갯수보다 클 경우 0으로 채워줌 '30.1234..'
```

- **isNaN()**
<br>NaN인지 판단해줌
```javascript
let x = Number('X'); //NaN

//NaN은 자기자신과도 똑같지 않다고 판단
x == NaN //false
x === NaN //false
NaN == NaN //false

//그래서 isNaN만 판단가능
isNaN(x) //true
isNaN(3) //false
```
- **parselnt()**
<br>소수점 이하는 무시하고 정수만 반환
<br>문자열을 숫자로 바꿔 줌
<br>Number와 다른 점은 문자가 혼용되어 있어도 동작 함
<br>읽을 수 있는 부분까지 읽고 문자를 만나면 숫자를 반환함
<br>두번째 인수를 받아서 진수를 지정할 수 있음
```javascript
let margin = '10px';

parseInt(margin); //10
Number(margin); //NaN

//숫자로 시작하지 않을 경우
let redColor = 'f3';
parseInt(redColor); //NaN

//진수 지정
let redColor = 'f3';
parseInt(redColor, 16); //243 (16을 전달해 16진수로 바꿈)
```

- **parseFloat()**
<br>parseInt와 동일하게 동작하지만, 부동소수점 반환
```javascript
let padding = '18.5%';

parseInt(padding); //18
parseFloat(padding); //18.5
```

- **Math.random()**
<br>0~1 사이 무작위 숫자 생성
```javascript
//만약 1~100 사이 임의의 숫자를 뽑고 싶다면? 식을 만들어 사용
Math.floor(Math.random()*100)+1

1. Math.random()으로 숫자 생성 //0.6789이라면
2. 거기에 100을 곱하면 뽑고싶은 총 갯수가 100개가 됨 //67.89
3. Math.floor을 이용해서 소숫점 버림 //67
4. 마지막으로 1을 더하는데 이유는 랜덤 숫자가 0.몇으로 나올수도 있기 때문에 최솟값 1을 더해줌 //68
```

- **Math.max() / Math.min()**
<br>max는 가로안에 인수들 중 최댓값 구할 수 있음
<br>min은 가로안에 인수들 중 최솟값 구할 수 있음
```javascript
Math.max(1,4,-1,5,10,9,5.54); //10

Math.min(1,4,-1,5,10,9,5.54); //-1
```

- **Math.abs()**
<br>절대값을 구해줌
<br>abs는 absolute의 약자
```javascript
Math.abs(-1) //1
```

- **Math.pow(n,m)**
<br>n의 m승 값(거듭 제곱 값)을 보여줌
```javascript
Math.pow(2, 10); //1024 (2의 10승)
```

- **Math.sqrt()**
<br>제곱근을 구해줌
<br>Square root의 약자
```javascript
Math.sqrt(16); //4
```
