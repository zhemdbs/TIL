# Intermediate - JS
> 출처 [자바스크립트 중급 강좌](https://youtu.be/4_WLS9Lj6n4)을 보고 정리한 내용.
________

## 목차

- [변수](#변수)
- [생성자 함수](#생성자-함수)
- [객체 메소드(object methods), 계산된 프로퍼티(Computed property)](#객체-메소드-계산된-프로퍼티)
- [심볼(Symbol)](#심볼(Symbol))
- [숫자, 수학 method (Number, Math)](#숫자-수학)
- [문자열 메소드 (String methods)](#String)
- [배열 메소드 1(Array methods)](#Array1-(배열))
- [배열 메소드 2(sort, reduce)](#Array2-(배열))
- [구조 분해 할당 (Destructuring assignment)](#구조-분해-할당(Destructuring-assignment))
- [나머지 매개변수, 전개 구문(Rest parameters, Spread syntax)](#나머지-매개변수-전개구문(Rest-prameters-Spread-syntax))
- [클로저(Closure)](#클로저(Closure))
- [setTimeout / setInterval](#setTimeout-/-setInterval)
- call, apply, bind
- prototype
- 클래스(class)
- 프로미스(Promise)
- async, await
- Generator
<br/>
_______
<br/>

# ***변수*** 

- ## let
```javascript
let name = 'Mike';
console.log(name); //Mike

let name = 'Jane';
console.log(name); // error!
```

- ## const
```javascript
let name;
name = 'Mike';

let age;
age = 30;

const gender;
gender = 'male'; //error! 선언하면서 할당을 안했기 때문
```

- ## var
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
|var|let|const|
|:---------------:|:---------:|:---------:|
|변수 재선언O|변수 재선언X|변수 재선언X|
|변수 재할당O|변수 재할당O|변수 재할당X|
|block scope 무시함|block scope안에서 선언되면 <br/>block scope 안에서만 존재|block scope안에서 선언되면 <br/>block scope 안에서만 존재|

- ## 호이스팅(hoisting)
  - let, const, var 모두 호이스팅 됨
  - 어디에 선언되었는지와 상관없이 항상 선언을 제일 위로 끌어올려 주는 것
<br>- 글로벌 스코프에서 선언되었다면, 스크립트의 제일 위로
<br>- 함수 스코프에서 선언되었다면, 함수 내에서 제일 위로 끌어올려짐
  - error를 내는 이유는 TDZ(Temporal Dead Zone)때문
<br>- TDZ영역에 변수들은 사용할 수 없음
<br>- let, const는 TDZ의 영향을 받음
<br>- 할당을 하기 전엔 사용할 수 없음
```javascript
//함수 호이스팅은 함수 선언식의 경우에만 적용
//함수 표현식에는 적용(x)

//함수 선언식
function funcDeclaration() {
  return 'A function declaration';
}

//함수 표현식
const funcExpression = function() {
  return 'A function expression';
}
```
<br/>

- ## Scope(스코프)
'밖에서는 안을 볼 수 없지만 안에서는 밖을 볼 수 있다'라는 문장 하나로 설명이 가능
<br>- 부모 함수는 자식 함수 안의 변수에 접근할 수 없지만, 자식 함수는 밖의 변수에 접근이 가능


<br/>

- ## 변수의 생성과정
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

- ## 스코프
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
<br/>

# ***생성자 함수*** 

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
<br/>

# ***객체 메소드, 계산된 프로퍼티***

- ## 계산된 프로퍼티(Computed property)
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

- ## 객체 메소드(object method)
  - ## Object.assign() : 객체 복제
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

  - ## Object.keys() : 키 배열 반환
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

  - ## Object.values() : 값 배열 반환
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

  - ## Object.entries() : 키/값 배열 반환
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

  - ## Object.fromEntries() : 키/값 배열을 객체로
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
<br/>

# ***심볼(Symbol)***

- ## property key: 문자형
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

- ## property key: 심볼형
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

- ## Symbol.for() : 전역 심볼
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
<br/>

# ***숫자, 수학***

- ## toString()
10진수 -> 2진수/16진수
```javascript
let num = 10;
num.toString(); //'10'
num.toString(2); //2진수로 변환 '1010'

let num2 = 255;
num2.toString(16); //16진수로 변환 'ff'
```

- ## Math
```javascript
//대표적인 프로퍼티 예
Math.PI; //3.141592653589793 (원주율)
```

- ## Math.ceil() : 올림
```javascript
let num1 = 5.1;
let num2 = 5.7;

Math.ceil(num1); //6
Math.ceil(num2); //6
```

- ## Math.floor() : 내림
```javascript
let num1 = 5.1;
let num2 = 5.7;

Math.floor(num1); //5
Math.floor(num2); //5
```

- ## Math.round() : 반올림
```javascript
let num1 = 5.1;
let num2 = 5.2;

Math.round(num1) //5
Math.round(num2) //6
```
- ## 소수점 자릿수
```javascript
//요구사항 : 소수점 둘째자리까지 표현(셋째 자리에서 반올림)
let userRate = 30.1234;

1. userRate * 100 //'3012.34' (100을 곱하고)
2. Math.round(userRate * 100) //'3012' (반올림을 해준 뒤)
3. Math.round(userRate * 100)/100 //'30.12' (다시 100을 나눠 줌)

그러면 요구사항은 30.12
```
<br>OR

- ## 소숫점 자릿수 : toFixed()
<br>숫자를 인수로 받아 그 숫자만큼 소수점 이하 갯수에 반영
<br>주의: 문자열로 반환.
<br>그래서 반환받은 이후, Number을 이용해 숫자로 변환 후 작업
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

- ## isNaN()
NaN인지 판단해줌
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

- ## parselnt()
소수점 이하는 무시하고 정수만 반환
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

- ## parseFloat()
<br>parseInt와 동일하게 동작하지만, 부동소수점 반환
```javascript
let padding = '18.5%';

parseInt(padding); //18
parseFloat(padding); //18.5
```

- ## Math.random()
0~1 사이 무작위 숫자 생성
```javascript
//만약 1~100 사이 임의의 숫자를 뽑고 싶다면? 식을 만들어 사용
Math.floor(Math.random()*100)+1

1. Math.random()으로 숫자 생성 //0.6789이라면
2. 거기에 100을 곱하면 뽑고싶은 총 갯수가 100개가 됨 //67.89
3. Math.floor을 이용해서 소숫점 버림 //67
4. 마지막으로 1을 더하는데 이유는 랜덤 숫자가 0.몇으로 나올수도 있기 때문에 최솟값 1을 더해줌 //68
```

- ## Math.max() / Math.min()
max는 가로안에 인수들 중 최댓값 구할 수 있음
<br/>min은 가로안에 인수들 중 최솟값 구할 수 있음
```javascript
Math.max(1,4,-1,5,10,9,5.54); //10

Math.min(1,4,-1,5,10,9,5.54); //-1
```

- ## Math.abs()
절대값을 구해줌
<br>abs는 absolute의 약자
```javascript
Math.abs(-1) //1
```

- ## Math.pow(n,m)
n의 m승 값(거듭 제곱 값)을 보여줌
```javascript
Math.pow(2, 10); //1024 (2의 10승)
```

- ## Math.sqrt()
제곱근을 구해줌
<br>Square root의 약자
```javascript
Math.sqrt(16); //4
```
_____
<br/>

# ***String***

- ## length
```javascript
//문자열 길이
let desc = '안녕하세요';
desc.length //6

//특정 위치에 접근
let desc = '안녕하세요';
desc[2] //'하'
```

- ## toUpperCase() / toLowerCase()
```javascript
let desc = "Hi guys. Nice to meet you.";

//대문자
desc.toUpperCase();
"HI GUYS. NICE TO MEET YOU."

//소문자
desc.toLowerCase();
"hi guys. nice to meet you"
```

- ## str.indexOf(text)
```javascript
let desc = "Hi guys. Nice to meet you.";

//문자를 인수로 받아 몇번째 위치 하는지 알려줌
desc.indexOf('to'); //14
desc.indexOf('man'); //찾는 문자가 없으면 -1을 반환

//포함된 문자가 여러개라도 첫번째 위치만 반환


//if문을 쓸때
if(desc.indexOf('Hi')) {
  console.log('Hi가 포함된 문장');
}//라고 쓰면 메세지를 볼 수 없음 
//Hi로 시작한 문장이라 indexOF Hi는 0이기 때문

//사용하려면
if(desc.indexOf('Hi') > -1){
  console.log('Hi가 포함된 문장');
}//로 써야함
```

- ## str.slice(n,m)
slice는 n부터 m까지의 문자열을 반환
<br>n : 시작점
<br>m : 없으면 문자열 끝까지, 양수면 그 숫자까지(포함X), 음수면 끝에서부터 센다
```javascript
let desc = "abcdefg";

desc.slice(2) //"cdefg"
desc.slice(0,5) //"abcde"
desc.slice(2,-2) //"cde"
```

- ## str.substring(n,m)
n과 m사이 문자열 반환(n부터 m이 아니라 n과 m사이)
<br>n과 m을 바꿔도 동작함
<br>음수는 0으로 인식
```javascript
let desc = "abcdefg";

desc.substring(2,5); //"cde"
desc.substring(5,2); //"cde"
```

- ## str.substr(n,m) 
n부터 시작
<br>m개를 가져옴
```javascript
let desc = "abcdefg";

desc.substr(2,4); //"cdef"
desc.substr(-4,2); //"de"
```

- ## str.trim() : 앞 뒤 공백 제거
```javascript
let desc = " coding        ";

desc.trim(); //"coding"
```

- ## str.repeat(n) : n번 반복
```javascript
let hello = "hello!";

hello.repeat(3); //"hello!hello!hello!"
```

예시
```javascript
//숫자제외, 글자만
let list = [
  "01, 들어가며",
  "02, JS의 역사",
  "03, 자료형",
  "04, 함수",
  "05, 배열",
];

let newList = [];

for(let i = 0; i < list.length; i++){
  newList.push(
    list[i].slice(4)
  );
}

console.log(newList); 
//(5) ["들어가며", "JS의 역사", "자료형", "함수", "배열"]
```
```javascript
//금지어 : 콜라

function hasCola(str){
  if(str.indecOf('콜라') > -1){
    console.log('금지어 있음');
  } else {
    console.log('통과');
  }
}

hasCola('와 사이다가 짱이야'); //통과
hasCola('아냐 콜라가 짱이야'); //금지어
hasCola('콜라'); //금지어
```

___
<br/>

# ***Array1 (배열 )***

- ## push() : 뒤에 삽입
- ## pop() : 뒤에 삭제
- ## unshift() : 앞에 삽입
- ## shift() : 앞에 삭제

- ## arr.splice(n,m) : 특정 요소 지움
n번째 요소부터 m개 지워라
```javascript
let arr = [1,2,3,4,5];
arr.splice(1,2);

console.log(arr); //[1,4,5]
```

- ## arr.splice(n,m,x) : 특정 요소 지우고 추가
```javascript
let arr = [1, 2, 3, 4, 5];
arr.splice(1, 3, 100, 200);
//1부터 3개를 지우고, 100, 200을 추가

console.log(arr); //[1, 5, 100, 200]

//0이 있다면
let arr = ["나는", "철수", "입니다"];
arr.splice(1, 0, "대한민국", "소방관");
// ["나는", "대한민국", "소방관", "철수", "입니다"]
```

- ## arr.splice() : 삭제된 요소 반환
```javascript
let arr = [1,2,3,4,5];
let result = arr.splice(1,2);

console.log(arr); //[1,4,5]
console.log(result); //[2,3]
```

- ## arr.slice(n,m)
n부터 m까지 반환
<br>m은 포함하지 않음, 안쓰면 배열 끝까지
```javascript
let arr = [1,2,3,4,5];
arr.slice(1,4); //[2,3,4]

let arr2 = arr.slice();
//빈 가로면 그대로 배열이 복사
console.log(arr2); //[1,2,3,4,5]
```

- ## arr.concat(arr2,arr3 ..)
합쳐서 새배열 반환
```javascript
let arr = [1,2];

arr.concat([3,4]); //[1,2,3,4]
arr.concat([3,4], [5,6]); //[1,2,3,4,5,6]
arr.concat([3,4],5,6); //[1,2,3,4,5,6]
```

- ## arr.forEach(fn)
배열 반복
<br>함수를 인수로 받음
<br>그 함수는 세개의 매게변수가 있는데
<br>item : 해당요소 / index : 인덱스 / arr : 해당배열 자체
<br>보통 item과 index만 사용
```javascript
let users = ['Mike', 'Tom', 'Jane'];

user.forEach((item, index, arr) => {
  // ..
});

//예시
let users = ['Mike', 'Tom', 'Jane'];

user.forEach((name, index) => {
  console.log(name); //Mike, Tom, Jane
});
```

- ## arr.indexOf / arr.lastIndexOF
인수가 두개인 경우는 두번째는 시작 위치 반환
<br>끝에서 부터 탐색하고 싶으면 lastIndexOf
```javascript
let arr = [1,2,3,4,5,1,2,3];

arr.indexOf(3); //2
arr.indexOf(3,3); //7 
arr.lastIndexOf(3); //7
```

- ## arr.includes()
포함하는지 확인
```javascript
let arr = [1,2,3];

arr.includes(2); //true
arr.includes(8); //false
```

- ## arr.find(fn) / arr.findIndex(fn)
복잡한 연산이 가능하도록 함수 연결 할 수 있음
<br>첫번째 true값만 반환하고 끝남
<br>만약 없으면 undefined를 반환
```javascript
let arr = [1, 2, 3, 4, 5];

const result = arr.find((item) => {
  return item % 2 === 0; //짝수를 찾아라
});

console.log(result); //2
-------------------------

let userList = [
  {name:"mike", age:30},
  {name:"jane", age:27},
  {name:"tom", age:10},
];

const result = userList.find((user) => {
  if(user.age < 19>){
    return true;
  }
  return false;
});

console.log(result); //{name:"tom", age:10}
---------------------------------------------

const result = userList.findIndex((user) => {
  if(user.age < 19>){
    return true;
  }
  return false;
});

console.log(result); //2
```

- ## arr.filter(fn)
만족하는 모든 요소를 배열로 반환
```javascript
let arr = [1, 2, 3, 4, 5];

const result = arr.filter((item) => {
  return item % 2 === 0; //짝수를 찾아라
});

console.log(result); //(3) [2,4,6]
```

- ## arr.reverse()
역순으로 재정렬
```javascript
let arr = [1,2,3,4,5];

arr.reverse(); //[5,4,3,2,1]
```

- ## arr.map(fn)
함수를 받아 특정 기능을 시행하고 새로운 배열을 반환
```javascript
let userList = [
  {name:"mike", age:30},
  {name:"jane", age:27},
  {name:"tom", age:10},
];

let newUserList = userList.map((user, index) => {
  return Object.assign({}, user, {
    id: index + 1,
    isAdult: user.age > 19,
  });
});

console.log(newUserList);
// 0: {name:"mike", age:30, id:1, isAdult: true}
// 1: {name:"jane", age:27, id:2, isAdult: true}
// 2: {name:"tom", age:10, id:3, isAdult: flase}
```

- ## arr.join()
배열을 합쳐서 문자열로 만듬
```javascript
let arr = ["안녕", "나는", "철수야"];

let result = arr.join("-");
console.log(result); //안녕-나는-철수야
```

- ## arr.split()
문자열 나눠서 배열로 만듬
```javascript
const users = "mike,jane,tom";

const result = users.split(",");

console.log(result); //["mike", "jane", "tom"]
```

- ## Array.isArray()
배열인지 아닌지 확인
```javascript
let user = {
  name: 'mike',
  age: 30
};

let userList = ['mike','tom', 'jane'];

console.log(Array.isArray(user)); //false
console.log(Array.isArray(userList)); //true
```

___
<br/>

# ***Array2 (배열 )***
<br/>

- ## arr.sort()
배열 재정렬
<br>배열 자체가 변경되니 주의
<br>인수로 정렬 로직을 담은 함수를 받음
```javascript
let arr = [1, 5, 4, 2, 3];

arr.sort();
console.log(arr); //[1, 2, 3, 4, 5]
-----------------------------

let arr = [27, 8, 5, 13];

arr.sort();
console.log(arr); //[13, 27, 5, 8]
//정렬 요소를 문자열로 취급해서 13의 1이 먼저 27의 2가 먼저 나옴
//제대로 하기 위해

let arr = [27, 8, 5, 13];

function fn(a,b) {
  return a - b;
}
arr.sort(fn);

console.log(arr);  //[5, 8, 13, 27]
```

- ## arr.reduce()
인수로 함수를 받음
<br>(누적 계산값, 현재값) => {return 계산값};
```javascript
//배열의 모든 수 합치기
let arr = [1, 2, 3, 4, 5];

//for, for of, forEach

let result = 0;
arr.forEach(num => {
  result += num;
});
console.log(result); //15

//이 작업을 reduce로 할 수 있음

//(누적 계산값, 현재값) => {return 계산값}
const result = arr.reduce((prev, cur) => {
  return prev + cur;
}, 0) //초기값:0

console.log(result); //15
```
<br>예시
```javascript
let userList = [
  {name:"mike", age: 30},
  {name:"tom", age: 10},
  {name:"jane", age: 27},
  {name:"sue", age: 26},
  {name:"harry", age: 42},
  {name:"steve", age: 60},
];

let result = userList.reduce((prev, cur) => {
  if (cur.age > 19) {
    prev.push(cur.name);
  }
  return prev;
}, []);

console.log(result); //["mike", "tom", "jane", "sue", "harry", "steve"]

//초기값이 빈배열,
//만약 19살보다 나이가 크다면 push해주고 리턴, 19살보다 작다면 실행x

//이름이 3글자인 사람 찾기
let result = userList.reduce((prev, cur) => {
  if (cur.name,length === 3) {
    prev.push(cur.name);
  }
  return prev;
}, []);

console.log(result); //["tom", "sue"]
```

___
<br/>

# ***구조 분해 할당( Destructuring assignment )***
<br/>

- ## Destructuring assignment
구조 분해 할당 구문은 배열이나 객체의 속성을 분해해서 그 값을 변수에 담을 수 있게 하는 표현식
```javascript
let [x, y] = [1, 2];

console.log(x); //1
console.log(y); //2
```
```javascript
let users = ['mike', 'tom', 'jane'];
let [user1, user2, user3] = users;

//let user1 = users[0];
//let user2 = users[1];
//let user3 = users[2];

console.log(user1); //'mike'
console.log(user2); //'tom'
console.log(user3); //'jane'
```

- ## 배열 구조 분해 : 기본값
```javascript
let [a,b,c] = [1,2];
//c는 undefined

let [a=3, b=4, c=5] = [1,2]; //기본값을 설정해서 error방지
console.log(a); //1
console.log(b); //2
console.log(c); //5
```

- ## 배열 구조 분해 : 일부 반환값 무시
```javascript
let [user1, ,user2] = ['mike', 'tom', 'jane', 'tony'];

console.log(user1); //'mike'
console.log(user2); //'jane'
```

- ## 배열 구조 분해 : 바꿔치기
```javascript
let a = 1;
let b = 2;
//b에 a값을 넣고 a에 b값을 넣고싶을때
[a, b] = [b, a];
```

- ## 객체 구조 분해
```javascript
let user = {name: 'mike', age: 30};
let {name, age} = user; //순서 신경쓰지 않아도 됨

console.log(name); //'mike'
console.log(age); //30
```

- ## 객체 구조 분해 : 새로운 변수 이름으로 할당
```javascript
let user = {name: 'mike', age: 30};
let {name: userName, age: userAge} = user;

console.log(userName); //'mike'
console.log(userAge); //30
```

- ## 객체 구조 분해 : 기본값
```javascript
let user = {name: 'mike', age: 30};
let {name, age, gender} = user;
//gender은 아무것도 없기 때문에 undefined
//그래서 기본값을 줌

let {name, age, gender = 'male'} = user;
```

___
<br/>

# ***나머지 매개변수, 전개구문( Rest prameters, Spread syntax )***
<br/>

- ## 인수 전달
... (점 3개로 전달)
```javascript
function showName(name){ //개수 제한 없음
  console.log(name);
}
showName('mike'); //'mike'
showName(); //undefined
```

<br>함수에 인수를 얻는 방법은 두가지
1. arguments로 접근
2. 나머지 매개 변수

- ## arguments
  - 함수로 넘어 온 모든 인수에 접근
  - 함수내에서 이용 가능한 지역 변수
  - length / index
  - Array 형태의 객체
  - 배열의 내장 메서드 없음 (forEach, map 사용X)
```javascript
function showName(name){
  console.log(arguments.length);
  console.log(arguments[0]);
  console.log(arguments[1]);
}

showName('mike', 'tom');
//2
//'mike'
//'tom'
```

- ## 나머지 매개변수(Rest parameters)
정해지지 않은 개수의 인수를 배열로 나타낼 수 있음
<br>항상 마지막에 있어야 함
```javascript
///(...배열이름)
function showName(...names) {
  console.log(names);
}

showName(); //[], undefined가 아님
showName('mike'); //['mike']
showName('mike', 'tom'); //['mike', 'tom']
```

예시
```javascript
//전달 받은 모든 수를 더해야함

function add(...numbers) {
  let result = 0; //초기값 0
  numbers.forEach(num => (result += num));
  console.log(result);
}

add(1, 2, 3); //6
add(1, 2, 3, 4, 5, 6, 7, 8, 9, 10); //55
```
```javascript
//user 객체를 만들어 주는 생성자 함수를 만듬

function User(name, age, ...skills){
  this.name = name;
  this.age = age;
  this.skills = skills;
}

const user1 = new User('mike', 30 ,'html', 'css');
const user2 = new User('tom', 20 ,'JS', 'React');
const user3 = new User('jane', 10 ,'English');

console.log(user1); //User{name:'mike', age:30, skills:Array(2)}
console.log(user2); //User{name:'tom', age:20, skills:Array(2)}
console.log(user3); //User{name:'jane', age:10, skills:Array(1)}
```

- ## 전개구문(Spread syntac) : 배열
```javascript
let arr1 = [1,2,3];
let arr2 = [4,5,6];

let result = [...arr1, ...arr2];
//...arr1은 1,2,3을 풀어서 쓴것
//...arr2은 4,5,6을 풀어서 쓴것
let result2 = [0, ...arr1, ...arr2, 7, 8, 9];
//중간에 풀어서 쓴것도 가능

console.log(result); //[1, 2, 3, 4, 5, 6]
console.log(result2); //[0,1,2,3,4,5,6,7,8,9]
```

- ## 전개구문(Spread syntac) : 객체
```javascript
let user = {name:'mike'}
let mike = {...user, age:30}

console.log(mike) //{name:'mike', age:30}
```

- ## 전개구문(Spread syntac) : 복제
```javascript
let arr = [1, 2, 3];
let arr2 = [...arr]; //[1, 2, 3]

let user = {name:'mike', age:30};
let user2 = {...user};

user2.name = 'tom';

console.log(user.name); //'mike'
console.log(user2.name); //'tom' 별개로 복제
```
예시
```javascript
//user에 info를 넣고 fe,lang을 skills로 넣어라

let user = {name: 'yoon'};
let info = {age:30};
let fe = {'JS', 'React'};
let lang = {'korean', 'english'};

user = {
  ...user,
  ...info,
  skills:[...fe, ...lang]
};

console.log(user);
// {name:'yoon', age:30, skills:Array(4)}
```

___
<br/>

# ***클로저(Closure)***
<br/>

- ## 클로저
중첩된 함수에서 자식의 함수가 부모 함수에 정의된 변수에 접근이 가능한 것들을 클로저라함

- ## 어휘적 환경(Lexical Environment)
함수와 렉시컬 환경의 조합
<br>함수가 생성될 당시의 외부 변수를 기억
<br>생성 이후에도 계속 접근 가능
```javascript
function makeAdder(x){
  return function(y){
    return x + y;
  }
}

const add3 = makeAdder(3);
console.log(add3(2)); //5
//add3함수가 생성된 이후에도 상위함수인 makeAdder의 x에 접근이 가능

const add10 = makeAdder(10);
console.log(add10(5)); //15
console.log(add3(1)); //4
//add10과 add3은 서로 다른 환경이므로 makeAdder(10)이 호출되지만 add3(1)에는 아무 변화가 없음
```

___
<br/>

# ***setTimeout / setInterval***
<br/>

- ## setTimeout
일정 시간이 지난 후 함수를 실행
```javascript
function fn(){
  console.log(3)
}

setTimeout(fn, 3000); //3초후 log를 찍어줌
```
setTimeout은 2개의 매개변수를 가짐
<br>- fn은 일정시간이 지난 뒤 실행하는 함수
<br>- 3000는 시간(3s)
```javascript
//위의 코드는 아래처럼 쓸 수 있음
setTimeout(function() {
  console.log(3)
}, 3000);

//함수를 전달하지 않고 직접 코드를 작성해도 동일 작동

//인수가 필요하다면 시간 뒤에 작성
//예시
function showName(name) {
  console.log(name);
}
setTimeout(showName, 3000, 'yoon');
//yoon는 name의 첫번째 인수로 전달 됨
```

- ## clearTimeout
예정 된 작업을 없앰
```javascript
function showName(name) {
  console.log(name);
}
const tId = setTimeout(showName, 3000, 'yoon');

clearTimeout(tId); //3초가 지나기전에 실행되기 때문에 아무일도 일어나지 않음
```

- ## setInterval
일정 시간 간격으로 함수를 반복
```javascript
function showName(name){
  console.log(name);
}

const tId = setInterval(show, 300, 'yoon');
//계속 반복 실행
//3초마다 'yoon'이 찍힘
//중간에 중단하려면 clearInterval(tId)를 사용
```
예시
```javascript
//setInterval, clearInterval
//user가 접속하면 접속한지 얼마나 지났는지 알려줌

let num = 0;

function showTime() {
  console.log(`안녕하세요. 접속하신지 ${num++}초가 지났습니다.`);
}

setInterver(showTime, 1000);//1초에 한번씩 보여줌
//안녕하세요. 접속하신지 0초가 지났습니다.
//안녕하세요. 접속하신지 1초가 지났습니다.
//안녕하세요. 접속하신지 2초가 지났습니다. ++
---------------------------------------------

//3초까지만 보여주고 싶다면
let num = 0;

function showTime() {
  console.log(`안녕하세요. 접속하신지 ${num++}초가 지났습니다.`);
  if (num > 3) {
    clearInterval(tId);
  }
}

const tId = setInterver(showTime, 1000);
//안녕하세요. 접속하신지 0초가 지났습니다.
//안녕하세요. 접속하신지 1초가 지났습니다.
//안녕하세요. 접속하신지 2초가 지났습니다.
//안녕하세요. 접속하신지 3초가 지났습니다.
```
___
<br/>

# ***call, apply, bind***
<br/>

- ## ***call, apply, bind***
함수 호출 방식과 관계없이 this를 지정할 수 있음

- ## call
모든 함수에서 사용할 수 있으며, this를 특정값으로 지정할 수 있음
```javascript
const mike = {
  name: 'mike'
};
const tom = {
  name: 'tom'
};

function showThisName(){
  console.log(this.name);
  //this는 window를 가르킴
}

showThisName(); //window.name이 빈문자열이라 아무것도 안나타남
showThisName.call(mike); //mike
//함수를 호출하면서 call사용, this를 사용할 객체mike를 넘기면 해당 함수가 주어진 객체의 메소드처럼 사용
showThisName.call(tom); //tom
```
```javascript
const mike = {
  name: 'mike'
};
const tom = {
  name: 'tom'
};

function showThisName(){
  console.log(this.name);
}
function update(birthYear, occupation){
  this.birthYear = birthYear;
  this.occupation = occupation;
}

update.call(mike, 1999, 'singer')

console.log(mike); //{name:'mike', birthYear:1999, occupation:'singer'}
```

- ## apply
함수 매개변수를 처리하는 방법을 제외하면 call과 완전히 같음
<br>call은 일반적인 함수와 마찬가지로 매개변수를 직접 받지만, apply는 매개변수를 배열로 받음
```javascript
const mike = {
  name: 'mike'
};
const tom = {
  name: 'tom'
};

function showThisName(){
  console.log(this.name);
}
function update(birthYear, occupation){
  this.birthYear = birthYear;
  this.occupation = occupation;
}

update.apply(mike, [1999, 'singer'])
console.log(mike); //{name:'mike', birthYear:1999, occupation:'singer'}
```

- ## bind
함수를 호출하는 것이 아니라 this가 바인딩 된 새로운 함수를 리턴함
```javascript
const mike = {
  name: 'mike'
};

function update(birthYear, occupation){
  this.birthYear = birthYear;
  this.occupation = occupation;
}

const updateMike = update.bind(mike); //항상 this를 mike로받음

updateMike(1980, 'police');
console.log(mike); //{name:'mike', birthYear: 1980, occupation:'police'}
```

예제
```javascript
const user = {
  name: 'mike',
  showName : function() {
    console.log(`hello, $(this.name)`);
  },
};

user.showName(); //hello, Mike

let fn = user.showName;

fn.call(user); //hello, Mike
fn.apply(user); //hello, Mike

let boundFn = fn.bind(user);

boundFn(); //hello, Mike
```

___
<br/>

# ***프로토타입(prototype)***

- ## 프로토타입 
자바스크립트는 프로토타입을 기반으로 상속을 구현하여 불필요한 중복을 제거함
<br>생성자 함수가 생성할 모든 인스턴스가 공통적으로 사용할 property나 method를 프로토타입에 미리 구현해둠으로써 인스턴스가 또 구현하는게 아니라 부모 object의 프로토타입의 자산을 공유해서 사용할 수 있음

- ## 프로토타입 체인
특정 객체의 메서드나 프로퍼티에 접근하고자 할때, 해당 객체에 접근하려고 하는 프로퍼티나 객체가 없다면, 프로토타입 링크([[Prototype]]프로퍼티)를 따라 자신의 부모 역할을 하는 프로토타입 객체를 차례로 검색함
___
<br/>

# ***클래스***
<br/>

- ## 클래스
object를 만글기 위한 템플릿
<br>- 템플릿이기 때문에 그 자체는 메모리상에 올라가지 않고, 실제로 데이터를 넣어서 object가 만들어지면 그 object가 메모리에 올라감
<br>- class는 연관 있는 fields(변수, 속성)와 methods(함수)로 이루어져 있음
```javascript
class User {
  constructor(name, age) {
    this.name = name;
    this.age = agel
  }
  showName() {
    console.log(this.name); //User {name:'tom', age:19}
  }
}

const tom = new User('tom', 19)
```

- ## extends
클래스에서 상속은 extends 사용
```javascript
class Car {
  constructor(color){
    this.color = color;
    this.wheels = 4;
  }
  drive() {
    console.log('drive..');
  }
  stopr() {
    console.log('stop!');
  }

  class Bmw extends Car {
    park() {
      console.log('park');
    }
  }
}
const z4 = new Bmw('blue');

//콘솔에 z4를 적으면
//Bmw{color:'blue', wheels:4}를 클릭 //z4객체에서 찾고
//__proto__:Car //proto타입에서 찾아보고 없으면
//constructor: class Bmw
//park: f park()
//__proto__: //또 proto타입에서 찾음
//constructor: class Car
//drive: f drive()
//stop: f stop()
//__proto__:Object
```

- ## 메소드 오버라이딩
```javascript
//Bmw내부에 Car에서 정의한 메소드와 동일한 이름의 메소드가 있을 경우
class Car {
  constructor(color){
    this.color = color;
    this.wheels = 4;
  }
  drive() {
    console.log('drive..');
  }
  stop() {
    console.log('stop!');
  }

  class Bmw extends Car {
    park() {
      console.log('park');
    }
    stop() {
      console.log('off');
    }
    // stop() { //부모의 메소드를 그대로 사용하고 확장하고 싶다면
    //   super.stop();//Car의 stop을 사용
    //   console.log('off');
    // }
  }
}

//콘솔에 z4.stop();을 입력하면 off가 뜸
//동일한 이름으로 메소드를 정의하면 덮어씀
```

- ## 오버라이딩
```javascript
class Car {
  constructor(color){
    this.color = color;
    this.wheels = 4;
  }
  drive() {
    console.log('drive..');
  }
  stopr() {
    console.log('stop!');
  }

  class Bmw extends Car {
    constructor(color){
      super(color);
      this.navigation = 1;
    }
    park() {
      console.log('park');
    }
  }
}
```
___
<br/>

# ***Promise***
<br/>

- ## promise
비동기 코드를 간편하게 처리할 수 있도록 도와주는 Object
<br>어떤 기능을 실행하고 나서 정상적으로 동작하면, 성공의 메시지와 함께 처리된 결과값을 전달해 줌
<br>그러나 기능을 수행하다 예상치 못한 문제가 발생하면 error를 전달해 줌
<br>- State: pending(보류)->fulfilled(이행)or rejected(거부)
```javascript
const pr = new Promise((resolve, reject) => {
  //code
});

//new Promise로 생성함
//resolve는 성공한 경우, reject는 실패했을때 실행되는 함수
//어떤일이 완료 된 후 실행되는 함수를 callback함수라고 함
```
```
//resolve
new Promise                                
state:pending(대기) --resolve(value)--> funlfilled(이행)
result:undefined                        result:value

//reject
new Promise                                
state:pending(대기) --reject(error)--> rejected(거부)
result:undefined                       result:error
```

```javascript
//resolve
const pr = new Promise((resolve, reject) => {
  setTimeour(()=>{
    resolve('ok')
  }, 3000)
}); //pending상태였다가 3초후 fulfilled로 바뀜

pr.then((result) => { //이행 되었을때 실행
  console.log(result); //ok
})
  .catch((err) => { //거부 되었을때 실행
    console.log(err);
  })
  .finally(() => { //이행이든 거부이든 처리가 완료되면 실행
    console.log('끝') //끝
  });



//reject
const pr = new Promise((resolve, reject) => {
  setTimeout(()=>{
    reject(new Error('err..'))
  }, 3000)
});//pending상태였다가 3초후 rejected로 바뀜

pr.then((result) => {
  console.log(result);
})
  .catch((err) => {
    console.log(err); //Error: err....
  })
  .finally(() => {
    console.log('끝') //끝
  });
```
예제
```javascript
//프로미스 체이닝(Promises chaining)

const f1 = () => {
  return new Promise((res, rej) => {
    setTimeout(() => {
      res('1번 주문 완료');
    }, 1000);
  });
};

const f2 = (message) => {
  console.log(message);
  return new Promise((res, rej) => {
    setTimeout(() => {
      rej('xxx');
    }, 3000);
  });
};

const f3 = (message) => {
  console.log(message);
  return new Promise((res, rej) => {
    setTimeout(() => {
      res('3번 주문 완료');
    }, 2000);
  });
};

console.log('시작');
//프로미스가 연결연결 되는것을
//프로미스 체이닝(Promises chaining)이라고 함
f1()
.then(res => f2(res))
.then(res => f3(res))
.then(res => console.log(res))
.catch(console.log)
.finally(() => {
  console.log('끝');
});

//시작
//1번 주문 완료
//xxx
//끝
```
```javascript
//Promises.all
//모든 작업이 완료 될때까지 기다림
const f1 = () => {
  return new Promise((res, rej) => {
    setTimeout(() => {
      res('1번 주문 완료');
    }, 1000);
  });
};

const f2 = (message) => {
  console.log(message);
  return new Promise((res, rej) => {
    setTimeout(() => {
      res('2번 주문 완료');
    }, 3000);
  });
};

const f3 = (message) => {
  console.log(message);
  return new Promise((res, rej) => {
    setTimeout(() => {
      res('3번 주문 완료');
    }, 2000);
  });
};

//Promise.all
Promise.all([f1(), f2(), f3()]).then((res) => {
  console.log(res);
});
//배열부분의 세작업이 모두 완료되어야 then 부분이 실행됨
//['1번 주문 완료', '2번 주문 완료', '3번 주문 완료']
```
```javascript
//Promises.race
//하나라도 먼저 완료되면 끝
const f1 = () => {
  return new Promise((res, rej) => {
    setTimeout(() => {
      res('1번 주문 완료');
    }, 1000);
  });
};

const f2 = (message) => {
  console.log(message);
  return new Promise((res, rej) => {
    setTimeout(() => {
      res('2번 주문 완료');
    }, 3000);
  });
};

const f3 = (message) => {
  console.log(message);
  return new Promise((res, rej) => {
    setTimeout(() => {
      res('3번 주문 완료');
    }, 2000);
  });
};

//Promise.race
Promise.all([f1(), f2(), f3()]).then((res) => {
  console.log(res);
});
//1번 주문 완료
```
___
<br/>

# ***async, await***
<br/>

- ## async
promise에 then메서드를 체인 형식으로 호출하는 것 보다 가독성이 좋아짐
```jacascript
//함수 앞에 async를 적으면 항상 promise를 반환

async function getName() {
  return 'mike';
}

getName().then((name) => {
  console.log(name); //mike
});
```

- ## await
async 함수 내부에서만 사용 가능
<br>일반 함수 내부에서 사용하면 에러 발생
```javascript
function getName(name) {
  return new Promise((resolve, reject) => {
    setTimout(() => {
      resolve(name);
    }, 1000);
  });
}

async function showName() {
  const result = await getName('mike');
  //result에 getName에서 resolve된 값을 await했다가 넣어줌
  console.log(result);
}

console.log('시작'); //시작
showName(); //1초 후에 console.log(result)에서 mike가 찍힘
```
```javascript
const f1 = () => {
  return new Promise((res, rej) => {
    setTimeout(() => {
      res('1번 주문 완료');
    }, 1000);
  });
};

const f2 = (message) => {
  console.log(message); //2. 1번 주문 완료
  return new Promise((res, rej) => {
    setTimeout(() => {
      res('2번 주문 완료');
    }, 3000);
  });
};

const f3 = (message) => {
  console.log(message); //3. 2번 주문 완료
  return new Promise((res, rej) => {
    setTimeout(() => {
      res('3번 주문 완료');
    }, 2000);
  });
};

console.log('시작'); //1. 시작
async function order() {
  const result1 = await f1();
  const result2 = await f2(result1);
  const result3 = await f3(result2);
  console.log(result3); //3. 3번 주문 완료
  console.log('종료'); //4. 종료
}
order();
```
___
<br/>

# ***Generator***
<br/>

- ## Generator
함수의 실행을 중간에 멈췄다가 재개할 수 있는 기능
<br>- function 옆에 *을 쓰고 만들고 내부에 yield키워드 사용
<br>- yield에서 함수 실행 멈출 수 있음
<br>- 외부로 부터 값을 입력받을 수 있음
<br>- 값을 미리 만들어 두지 않음
<br/>
<br/>***장점***
<br/>다른 작업을 하다가 다시 돌아와서 next( ) 해주면 진행이 멈췄던 부분 부터 이어서 실행
<br/>
```javascript
function* fn() {
  yield 1;
  yield 2;
  yield 3;
  return 'finish';
}

const a = fn();
```

- ## Generator : next( )

```javascript
//generator객체는 next메소드가 있음

function* fn(){
  console.log(1);
  yield 1;
  console.log(2);
  yield 2;
  console.log(3);
  console.log(4);
  yield 3;
  return 'finish';
}
const a = fn();

//generator함수를 실행하면 generator객체만 반환되고 함수 본문코드는 실행되지 않음
//콘솔에 a.next();로 호출하면
//가장 가까운 yield문을 만날때까지 실행되고 데이터 객체 반환

a.next();
1 {value:1, done: false} 
//value는 yield오른쪽 값(값을 생략한다면 undifined)
//done은 함수 코드가 끝났는지 나타내고 실행이 끝났으면 true, 아니면 false

a.next();
2 {value:2, done: false}
a.next();
3 4 {value:3, done: false}
a.next();
{value:'finish', done: true} //이제 끝났다는 뜻
a.next();
{value:undefined, done: true}
```
```javascript
//next( )에 인수 전달
function* fn() {
  const num1 = yield '첫번째 숫자를 입력해주세요';
  console.log(num1);

  const num2 = yield '두번째 숫자를 입력해주세요';
  console.log(num2);

  return num1 + num2;
}
const a = fn();

//콘솔에서

a.next();
{value:'첫번째 숫자를 입력해주세요', done:false}

a.next(2); //인수를 넣으면 인수숫자는 num1에 저장
2 //console.log(num1)을 통해 보여줌
{value:'두번째 숫자를 입력해주세요', done:false}

a.next(4);
4 //console.log(num2)
{value:6, done:true} //value는 num1 + num2 값
```

- ## Generator : return( )
```javascript
function* fn(){
  console.log(1);
  yield 1;
  console.log(2);
  yield 2;
  console.log(3);
  console.log(4);
  yield 3;
  return 'finish';
}
const a = fn();

a.next();
1 {value:1, done: false} 
//동일한 코드에서 실행하다가

a.return('END'); //를 실행하면
{value:'END', done:true} //그 즉시 done속성값이 true가 됨
//이후에 next를 실행해도 value얻어올수없고 done
```
  

- ## Generator : throw( )

```javascript
function* fn(){
  try { //try, catch : 예외처리
    console.log(1);
    yield 1;
    console.log(2);
    yield 2;
    console.log(3);
    console.log(4);
    yield 3;
    return 'finish';
  } catch (e) {
    console.log(e);
  }
}
const a = fn();

a.next();
1 {value:1, done: false}
a.next();
2 {value:2, done: false} 를 하다가

//a. throw(new Error('err'))를 실행하면
//Error:err {value:undefined, done:true}
//catch문에 있는 내용 실행되면서 에러가 찍히고 done은 true
```

- ## Generator : iterable
반복이 가능하다는 의미
<br>- 조건
<br>1. Symbol.iterator 메서드가 있음
<br>2. Symbol.iterator는 iterator를 반환해야 한다

- ## Generator : iterator
메서드를 호출한 결과
<br>- 조건
<br>1. next 메서드를 가짐
<br>2. next 메서드는 value와 done 속성을 가진 객체를 반환
<br>3. 작업이 끝나면 done은 true가 됨

```javascript
const arr = [1, 2, 3, 4, 5];

//콘솔에서

const it = arr[Symbol.iterator]();

it.next();
{value:1, done:false}
it.next();
{value:2, done:false}
...
it.next();
{value:5, done:false}
it.next();
{value:undefined, done:true}

//배열은 Symbol.iterator메소드를 갖고 있고, 이 메소드가 반환하는 값이 iterator이므로 iterable하다고 할 수 있음

//즉, 배열은 반복 가능한 개체
```
```javascript
//iterable은 for of를 이용해서 순회할 수 있음

const arr = [1, 2, 3, 4, 5];

//콘솔에서

for(let num of arr){
  console.log(num)
};

1
2
3
4
5
undefined
```
```javascript
//yield를 이용

function* gen1() {
  yield "w";
  yield "o";
  yield "r";
  yield "l";
  yield "d";
}

function* gen2() {
  yield "Hello";
  yield* gen1();
  yield "!";
}

//콘솔에

console.log(...gen2());
Hello, w o r l d ! //가 찍혀 나옴
//true가 될때까지 값을 펼쳐줌
```