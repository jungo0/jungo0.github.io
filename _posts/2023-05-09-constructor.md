---
title:  "[JavaScript] 생성자 함수(Constructor Function)"
subtitle: "df"
categories: JavaScript
tag: [생성자 함수, JavaScript]
toc: true
author_profile: false


sidebar:
    nav: "counts"
---
![](/assets/images/javascript.jpg)
## <span style='color:RGB(135, 203, 206)'> 생성자 함수

> 생성자 함수는 JavaScript에서 객체를 생성하기 위해 사용되는 특수한 함수입니다. 생성자 함수로 객체를 생성하기 위해서는 new 연산자를 호출합니다.

 

다음 예제는 Date()라는 생성자 함수와 new 연산자를 사용하여 Date 객체를 생성합니다.
```javascript
var date = new Date();
```
JavaScript는 Date 생성자 이외에도 Array, Boolean, Error, Function, Number 등 다양한 내장 생성자를 제공합니다.

### 생성자 함수 만들기
개발자가 직접 생성자 함수를 만들어야 하는 경우가 존재합니다. 다음 예제는 UserInfo라는 생성자 함수를 구현합니다.
```javascript
// 생성자 함수
function UserInfo() {
  this.name = 'Nick';
  this.age = 20;
  this.addresss = 'Busan';
}

// 객체 생성
let userInfo = new UserInfo();

console.log(userInfo);
```
[실행 결과]
```javascript
UserInfo {name: 'Nick', age: 20, addresss: 'Busan'}
```
생성자 함수는 화살표 함수(Arrow Function)로 만들 수 없으며 오직, function 키워드를 사용해야 합니다.

 

생성자 함수의 이름은 생성자 함수와 일반 함수를 구분하기 위해 첫 글자를 대문자로 시작하는 것이 좋습니다.

### 매개변수가 존재하는 생성자 함수

Date() 생성자 함수처럼 매개변수가 존재하는 생성자 함수를 만들 수 있습니다.
```javascript
// 매개변수가 없는 Date 생성자 함수
var date1 = new Date();

// 1개의 매개변수가 존재하는 Date 생성자 함수
var date3 = new Date('2020-5-4');

// 5개의 매개변수 존재하는 Date 생성자 함수
var date2 = new Date(1999,10,25,2,50);
 ```

다음 예제는 3개의 매개변수(name, age, address)를 가지는 생성자 함수입니다.

```javascript
function UserInfo(name, age, address) {
  this.name = name;
  this.age = age;
  this.addresss = address;
}

let userInfo = new UserInfo('홍길동', 20, '서울');

console.log(userInfo);
```
[실행 결과]

```javascript
UserInfo {name: '홍길동', age: 20, addresss: '서울'}
```



### 생성자 함수의 this
this는 쉽게 말하자면 자기 자신으로 생성자 함수를 호출한 객체를 의미합니다.
```javascript
function UserInfo() {
  this.name = 'Bob';
}

let user = new User();
```
---
### 생성자 vs 객체 리터럴
"생성자를 굳이 만들어야 하나?"라는 생각을 가질 수 있습니다. 다음 예제처럼 객체 리터럴을 활용하여 객체를 생성할 수 있기 때문이죠.
```javascript
let userInfo = {
  name: '홍길동',
  age: 20,
  addresss: '서울'
}
```
동일한 프로퍼티(name, age, address)를 가지는 3개의 객체가 필요한 경우 다음 예제처럼 객체를 생성할 수 있습니다.
```javascript
let userInfo1 = {
  name: '홍길동',
  age: 20,
  addresss: '서울'
}

let userInfo2 = {
  name: '홍길동',
  age: 20,
  addresss: '서울'
}

let userInfo3 = {
  name: '홍길동',
  age: 20,
  addresss: '서울'
}
```
소스코드가 중복되어 가독성이 떨어집니다.

 

다음 예제처럼 객체 usrInfo2와 userInfo3을 userInfo1으로 초기화하면 코드가 심플해집니다. 하지만, 치명적인 단점이 존재합니다.
```javascript
let userInfo1 = {
  name: '홍길동',
  age: 20,
  addresss: '서울'
}

let userInfo2 = userInfo1;
let userInfo3 = userInfo1;

userInfo3.name = '마이콜';

console.log(userInfo1.name);
console.log(userInfo2.name);
console.log(userInfo3.name);
```
[실행 결과]
```
마이콜
마이콜
마이콜
```
userInfo3.name을 변경했는데, userInfo1.name, userInfo2.name도 변경되는 문제가 발생합니다. 각 객체가 독립적으로 동작하지 않고 동일한 객체를 가리키고 있기 때문입니다.

 

다음 예제처럼 생성자를 사용하여 3개의 객체를 생성하고 userInfo3.name의 값을 변경해봅시다.
```javascript
function UserInfo() {
  this.name = '홍길동';
  this.age = 20;
  this.addresss = '서울';
}

let userInfo1 = new UserInfo();
let userInfo2 = new UserInfo();
let userInfo3 = new UserInfo();

userInfo3.name = '마이콜'

console.log(userInfo1.name);
console.log(userInfo2.name);
console.log(userInfo3.name);
```
[실행 결과]
```
홍길동
홍길동
마이콜
```
생성자를 사용하여 생성된 객체는 독립적으로 동작하는 것을 확인할 수 있습니다.

 

생성자 함수는 동일한 프로퍼티를 가지는 객체를 심플하게 생성할 수 있으며, 각 객체의 독립성을 보장합니다.