---
title:  "[Java Script] 전개 연산자, 함수와 화살표 함수, 클래스, 모듈 패턴" 
excerpt: "Java Script 필수 문법 3"

categories:
  - Java Script

toc: true
toc_sticky: true
 
date: 2023-08-01
last_modified_at: 2023-08-01

---
## 전개 연산자 (Spread Operator)
전개 연산자는 하나의 배열 또는 객체를 전달할 때 여러 개의 값으로 받을때 사용한다.  
또는 배열이나 객체를 복사할 때 유용하게 사용한다.  
전개 연산자는 `...`을 사용한다.

- 배열

```javascript
function foo(x, y, z) {
    console.log(x, y, z);
}

var boo = [0, 1, 2];
foo(...boo);    // 0 1 2

var foo = [1, 2, 3];    
var boo = [...foo, 11, 22, 33];
console.log(foo, boo);      // [1, 2, 3] [1, 2, 3, 11, 22, 33]

var boo = [foo, 11, 22, 33];
console.log(foo, boo);      // [1, 2, 3] [[1, 2, 3], 11, 22, 33]

var foo = [1, 2];
var boo = [0, ...foo, 3, 4];
console.log(foo, boo);      // [1, 2] [0, 1, 2, 3, 4]
```

- 객체

```javascript
var foo = {a: 1, b: 2};
var boo = {...foo, a: 2, c: 3};      // foo에서 a를 덮어씌우고 c를 새로 만듦
console.log(foo, boo);               // {a: 1, b: 2} {a: 2, b: 2, c: 3}
```

## 함수와 화살표 함수
ES6부터는 function() {}을 `() => {}`로 사용할 수 있다.  
function() {return }는 `() => ()`의 형태로 사용할 수 있다.  
화살표 함수는 ()를 넣으면 return한다.

일반적인 함수의 형태  

```javascript
function foo() {
    console.log('foo');
}
foo();      // foo
```

화살표 함수 () => {}

```javascript
const foo = () => {
    console.log('foo');
}
foo();
```

화살표 함수 () => ()

```javascript
const foo = () => {return 'foo'};
const boo = () => ('boo');          // return 생략 가능

console.log(foo());
console.log(boo());
```

## 클래스
ES6부터는 class 키워드를 사용할 수 있다.  
메소드를 생성할 때 `get` 키워드를 이용하면 해당 메소드를 속성처럼 사용할 수 있다.  
클래스를 만들 때 내부적으로 속성이나 메소드를 사용하기 위해서는 `this`를 사용해야 한다.  
클래스를 이용하면 객체를 생성할 수 있다.  

```javascript
class Square{
    constructor(height, width) {    // 생성자
        this.height = height;
        this.width = width;
    }
    
    get area() {
        return this.calcArea();
    }
    
    calcArea() {
        return this.height * this.width;
    }
}

var foo1 = new Square(1, 2);
var foo2 = new Square(11, 2);

console.log(foo1.area);     // 2
console.log(foo2.area);     // 22
```

## 모듈 패턴
특정 파일을 가져온다고 해서 파일에 정의된 변수, 함수, 클래스를 사용할 수 없다.  
`module.exports`를 이용하여 해당 파일에 만들어진 함수, 변수, 클래스를 외부에 노출해야 사용 가능하다.

ES5 스타일

```javascript
// ./ES5/index.js
let PI = Math.PI;
let area = function (r) {
    return PI * r * r;
};
module.exports = {
    area: area,
    pi: PI
}

// es5.js
const foo1 = require('./ES5');
const foo2 = require('./ES5/index.js');

let area1 = foo1.area(10);
let area2 = foo2.area(10);

console.log(area1);     // 3.141592...
console.log(area2);     // 3.141592...

// 비구조화 할당을 이용하면 간결하게 사용 가능
const {area} = require('./ES5');
console.log(area(10));  // 3.141592...
```

ES6 스타일

```javascript
// ./ES6/index.js
let PI = Math.PI;

let area = function (r) {
    return PI * r * r;    
};

// module.exports 대신 export default를 사용한다.
export default area

// es6.js
// require() 대신 import [사용할 이름] from [파일]
import area from './ES6/index.js';

let area1 = area(10);
console.log(area1);     // 3.141592...
```

여러개를 외부로 노출하고 싶다면 노출하고 싶은 곳에 export를 붙여주면 된다.

```javascript
// ./ES6/index.js
export const hello = function hello(){
    return 'hello';
};

export const area = function area(r) {
    return Math.PI * r * r;
};

export const v = 'hello world';

// es6.js
import {hello, area} from './ES6/index.js';

console.log(hello());   // hello
console.log(area(1));   // 3.141592...
```
