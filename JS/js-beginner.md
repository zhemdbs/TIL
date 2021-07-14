# Basic - JS
> 출처 [자바스크립트 기초 강좌](https://youtu.be/KF6t61yuPCY)을 보고 정리한 내용.

## 목차

- JS란?
- [변수](#변수)
- [자료형](#자료형)
- [typeof](#typeof)
- [기본연산자](#기본-연산자)
- [비교, 동등연산자](#비교-연산자-동등-연산자)
- [조건문](#조건문)
- [논리연산자](#논리-연산자)
- [반복문](#반복문)
- [switch문](#switch문)
- [함수(function)](#함수function)
- [함수 표현식, 화살표 함수](#함수표현식-화살표-함수)
- [객체(object)](#객체object)
- [객체(method/this)](#객체methodthis)
- [배열(Array)](#배열array)

## 변수

```javascript
name = "yoon";
age = 30;
```
<br>name 이라는 변수가 다시 사용되지 않기 위해 let, const를 사용
<br>`let` : 한번 선언 후 다른 값으로 바꿀 수 있음
<br>`const` : 절대로 바뀌지 않는 상수, 수정X
<br>즉, 변수를 선언할때, 변하지 않는 값은 const / 변할 수 있는 값은 let으로 선언

- 주의할 점
1. 변수는 문자와 숫자, $와 _만 사용가능
2. 첫글자는 숫자가 될 수 없음
3. 예약어 사용X
4. 가급적 상수는 대문자
5. 변수명은 읽기 쉽고 이해할 수 있도록 선언


## 자료형

* 문자형 string
```javascript
const name1 = "yoon"
const name2 = 'yoon'
const name3 = `yoon` -백틱
//백틱은 문자 내부의 변수를 표현할 때 사용 
const message = `My name is ${name}`;
```

* 숫자형 Number
```javascript
const age = 30;
console.log(1 + 2); //더하기
console.log(10 -3); //빼기
console.log(3 * 2); // * 곱하기
console.log(6 / 3); // / 나누기
console.log(6 % 4); // % 나머지(6을 4로 나눈 나머지 값)

Number("문자") //NaN
```
* 주의사항
```
 - Number(null) //0
 - Number(undefined) //NaN
 
 - Number(0) //false
 - Number('0') //true
 
 - Number('') //false
 - Number(' ') //true
```

* Boolean
```javascript
const a = true; //참
const b = false; //거짓

const name = "yoon";
const age = 30;
console.log(name == 'yoon') //ture
console.log(age > 40) //false
```
* false로 반환
 <br>1. 숫자 0
 <br>2. 빈 문자열 ''
 <br>3. null
 <br>4. undefined
 <br>5. NaN

* null & undefined
 <br>null : 존재하지 않는 값
 <br>undefined : 값이 할당되지 않았다


* typeof 연산자
```
typeof 3;  //number
typeof name; //string
typeof true; //boolean
typeof "XXX"; //string
typeof null; //object
typeof undefined; //undefined
```

## typeof

```javascript
const name = 'yoon';
const a = '나는';
const b = '입니다.';
console.log(a + name + b); //"나는 yoon 입니다."
```

## 기본 연산자

* %(나머지) 사용
 <br>홀수: X % 2 = 1
 <br>짝수: Y % 2 = 0
 <br>어떤 값이 들어와도 5를 넘기면 안된다면 X % 5 = 0~4사이의 값만 반환

```javascript
//연산자 줄여 쓰기
let num = 10;
num = num + 5; //동일 num += 5; ( -= , *= , %= )
 
//증가 연산자, 감소연산자
let num = 10;
num++; //11
num--; //9
```

## 비교 연산자, 동등 연산자

```javascript
//비교 연산자
console.log(10 > 5); //true
console.log(10 == 5); //동등연산자 //false
console.log(10 != 5); //true

//동등 연산자
const a = 1;
const b = "1";
console.log(a == b); //true
console.log(a === b); //일치연산자 //false(타입까지 비교)
```

## 조건문

```javascript
//if문
if(age > 19) {
 console.log('환영합니다.'); //age가 19보다 크면 실행
} else if(age === 19) {
 console.log('수능 잘치세요'); //age가 19이면 실행
} else {
 console.log('안녕히 가세요.'); //age가 19보다 작으면 실행
}
```

## 논리 연산자

- ||(or)
 <br>여러개 중 하나라도 true 면 true
 <br>즉, 모든값이 false 일때만 false 를 반환
  - or는 첫번째 true를 발견하는 즉시 평가를 멈춤
 
```javascript
const name = 'yoon';
const age = 30;

if(name === 'ji' || age > 19){
 console.log('통과');
} //이름은 ji가 아니지만 19이상이기 때문에 '통과'
```

- &&(and)
 <br>모든 값이 true 면 treu
 <br>즉, 하나라도 false 면 false를 반환
  - and는 첫번째 false를 발견하는 즉시 평가를 멈춤
 
```javascript
const name = 'yoon';
const age = 30;

if(name === 'yoon' && age > 19){
 console.log('통과');
} //이름, 나이 모두 조건과 맞기 때문에 '통과'

if(name === 'ji' && age > 19){
 console.log('통과');
} else {
 console.log('돌아가.');
} //나이는 맞지만 이미 ji에서 false 이므로 '돌아가'
```

- !(not)
<br>true 면 false
<br>false 면 true
```javascript
const age = prompt('나이는?');
const isAdult = age > 19;

if(!isAdult){
 console.log('돌아가');
} //30을 입력하면 돌아가가 뜸
```

## 반복문

- for문
```javascript
for (let i = 0; i < 10; i++) {
  //반복할 코드
}
//let i = 0; 초기값
//i < 10; 반복문이 돌면서 조건을 확인하고 false가 되면 멈춤
//i++ 반복문이 한번 실행된 후 작업
```

- while문
```javascript
let i = 0;
while(i < 10){
 //코드
 i++;
}
```

- do..while문
```javascript
let i = 0;
do {
 //코드
 i++;
} while (i < 10)
//일단 코드를 실행하고 조건을 체크
```

- 반복문 빠져나오기
```javascript
//break
//break: 멈추고 빠져나옴

while(true){
 let answer = confirm('계속 할까요?');
 if(!answer){
  break;
 }
} 

//continue
//continue: 멈추고 다음 반복으로 진행

for(let i = 0; i < 10; i++){
 if(i%2){
  continue;
 }
 console.log(i) //짝수만 찍힘
}
```

## switch문

```javascript
switch(평가){
 case A:
 // A일때 코드
 case B:
 // B일때 코드
 ...
}
//if문으로 바꾸면
if(평가 == A){
 // A일때 코드
} else if(평가 == B){
 // B일때 코드
}
```
```
let fruit = prompt('무슨 과일을 사고 싶나요?');
switch(fruit){
 case '사과':
  console.log('100원 입니다.');
  break;
 case '키위':
 case '수박':
  console.log('500원 입니다.'); //키위와 수박이 동일하게 500원일때
  break;
 default : //else랑 같은 뜻
  console.log('그런 과일은 없습니다.');
}
```

## 함수(function)

```javascript
function sayHello(name){
 console.log(`Hello, ${name}`);
}
//function:함수 , sayHello:함수명, (name):매게변수

ex)매게변수x 함수
function showError(){
 alert('에러발생, 다시 시도하셈');
}
showError();

let msg = 'Hello'; //전역 변수(global varable)
console.log(msg) //함수 호출 전 'Hello'
funtion sayHello(name){
 if(name){
  msg += `, ${name}`
 }
 //지역 변수(local varable)
 console.log(msg); //함수 내부 'Hello, yoon'
}

sayHello('yoon');
console.log(msg) //함수 호출 후 'Hello, yoon'

//return으로 값 반환
function add(num1, num2){
 return num1 + num2;
}
const result = add(2,3);
console.log(result); //5

function showError(){
 alert('에러가 발생했습니다');
 return;
}
const result = showError();
console.log(result); //undefined
```
<br>한번에 한작업에 집중
<br>읽기 쉽고 어떤 동작인지 알 수 있게 네이밍


## 함수표현식, 화살표 함수

- 함수 선언문 (어디서든 호출 가능)
```
//sayHello(); 위에 있어도 동작 가능
fuction sayHello(){
 console.log('Hello');
}
sayHello();
```

- 함수 표현식 (코드에 도달하면 생성)
```
let sayHello = funtion(){
 console.log('Hello');
}
sayHello();
```

- 화살표 함수(arrow function)
```
let add = function(num1, num2){
 return num1 + num2
}
//를 화살표 함수로 바꾸면
let add = (num1,num2) => num1 + num2;

//만약 인수가 하나라면 가로도 생략 가능
let sayHello = name => `Hello, ${name}`;
//인수가 없는 함수라면 가로 생략 불가능
let showError = () => {alert('error!');}
```

## 객체(object)

- object
```javascript
const superman = {
  name: 'yoon', //name:키(key) , 'yoon':값(value)
  age:33
}

//ex
function makeObject(name, age){
 return{
  name,
  age,
  hobby : 'football'
 }
}
  
const yoon = makeObject('yoon', 30);
console.log(yoon);
//object {
//  age : 30,
//  hobby : 'football',
//  name : 'yoon'
//}
```
```javascript
  // 객체에 접근하고자 할때
  superman.name //'yoon'
  superman['age'] //33
 
  // 객체에 추가하고자 할때
  superman.gender = 'female';
  superman['hairColor'] = 'brown';
  
  // 객체를 삭제하고자 할때
  delete superman.hairColor;
```
- 단축 프로퍼티
```javascript
const name = 'yoon';
const age = 33;

const superman = {
 name, //name : name 과 같음
 age, //age : age 와 같음
 gender : 'male',
}
```
- 프로퍼티 존재 여부 확인
```javascript
const name = 'yoon';
const age = 33;

superman.birthDay; //undefined

//in 연산자를 사용하면 프로퍼티 있는지 확인 가능
// 어떤값이 나올지 확신할 수 없을 때 사용
'birthDay' in superman; //false
'age' in superman; //true

// ex) 객체 in 
function isAdult(user){
 if(!('age' in user) || //user에 age가 없거나
    user.age < 20){ //20살 미만이거나
  return false;
 }
 return true;
}

const Yoon = {
 name : 'yoon',
 age : 30
};
const Jane = {
 name : 'jane'
};

console.log(isAdult(Jane)) //false (age값이 없기때문에 false)
```

- for...in 반복문
```javascript
//for...in 반복문을 실행하면 객체를 순회하면서 값을 얻을 수 있음
for(let key in superman){
 console.log(key)
 console.log(superman[key])
}

//객체 for...in
const Yoon = {
 name : 'yoon',
 age : 30
};

for(a in Yoon){
 console.log(Yoon[x]) //Yoon['name']이 돌고 Yoon['age']이 돔
}
```

## 객체(method/this)

- method
<br>method : 객체 프로퍼티로 할당 된 함수 
```javascript
const superman = {
 name:'yoon',
 fly: function(){   //fly() 로도 작성 가능
  console.log('날아갑니다')
 }
}
superman.fly(); //날아갑니다.

//fly함수가 superman 객체의 method
```

- this
<br>객체와 method의 관계
```javascript
const user = {
 name : 'yoon',
 sayHello(){
  //console.log(`Hello, i'm____`) //가로에 yoon을 넣고 싶다면
  console.log(`Hello, i'm ${this.name}`);
 }
}
user.sayHello(); //Hello, i'm yoon 
//user가 sayHello의 method의 this가 됨
```
<br>화살표 함수는 일반 함수와는 달리 자신만의 this를 가지지 않음
<br>화살표 함수 내부에서 this를 사용하면, 그 this는 외부에서 값을 가져 옴

```javascript
let boy = {
 name : 'Mike',
 showName : function(){
  //console.log(boy.name)
  console.log(this.name)
 }
};
boy.showName(); //'Mike'

let man = boy;
boy = null;

man.showName(); 
//boy.name으로 하면 error가 뜸 boy가 null을 가지고 name이 없어졋으므로
//반면 this.name으로 하면 'Mike'가 뜸 showName의 method의 this는 해당객체를 가르키기 때문
```

## 배열(array)

<br> 배열(array) : 순서가 있는 리스트
- 배열특징
<br>배열은 문자 뿐만 아니라, 숫자, 객체, 함수 등도 포함할 수 있음
<br>length : 배열의 길이
<br>push() : 배열 끝에 추가
```
let days = ['월','화','수'];
days.push('목')
console.log(days) //['월','화','수','목']
```
<br>pop() : 배열 끝에 요소 제거
```
let days = ['월','화','수'];
days.pop()
console.log(days) //['월','화']
```
<br>shift, unshift : 배열 앞에 제거/추가 (여러요소 한번에 추가,제거 가능)
```
//추가
days.unshift('일');
console.log(days) //['일','월','화','수']

//제거
days.shift();
console.log(days) //['월','화','수']
```
<br>반복문 : for
```javascript
let days = ['월','화','수'];
for(let index = 0; index < days.length; index++){
 console.log(days[index])
}
```
<br>반복문 : for..of
```javascript
let days = ['월','화','수'];
for(let day of days){
 console.log(day)
}
```
