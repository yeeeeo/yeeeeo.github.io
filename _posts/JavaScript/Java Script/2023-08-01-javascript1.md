---
title:  "[Java Script] 변수 생성, 데이터 타입, 데이터 형 변환,비구조화 할당" 
excerpt: "Java Script 필수 문법 1"

categories:
  - Java Script

toc: true
toc_sticky: true
 
date: 2023-08-01
last_modified_at: 2023-08-01

---
## 변수 생성
1. var  
var은 let보다 엄격하지 않다.  
var은 똑같은 변수로 선언이 가능하다.
var로 변수를 생성하면 scope를 벗어나도 변경된 값이 유지된다.
```javascript
// 똑같은 변수 선언 가능
var a;
var a;

// scope
var foo = 'bar1';
console.log(foo);   // bar1

if (1) {
    var foo = 'bar2';
    console.log(foo)    //bar2
}

console.log(foo);       // bar2
```

2. let
let은 이미 선언한 변수를 선언한 변수를 선언한다면 에러가 발생한다.  
let으로 변수를 생성하면 scope를 벗어나면 변경된 값이 유지가 안된다.

```javascript
// 변수 선언
let a;
let a;  // error!

// scope
let foo = 'bar1';
console.log(foo);       // bar1

if (1) {
    let foo = 'bar2';
    console.log(foo);   // bar2
}

console.log(foo);       // bar1
```

3. const
const로 변수를 선언하면 값을 바꿀 수 없다.
```javascript
// 변수 선언
const a = '';

// 값 변경 불가능
const foo = 'bar1';
foo = 'bar2';           // error!
```

## 데이터 타입
1. Boolean  
Boolean은 `true`, `false` 값을 가지는 타입이다.  

```javascript
let foo = true;  // 또는 false
```

2. Null  
Null은 `null`을 가지는 타입이다.

```javascript
let foo = null;
```

3. Undefined  
Undefined는 값이 할당되지 않은 타입이다.

```javascript
let foo;
console.log(foo)    // undefined
```

4. Number  
Number는 숫자 타입이다. 숫자 자료형에서 `NaN`은 숫자가 아닌 것을 의미한다.

```javascript
let foo = 1;
let boo = NaN;
```

5. String  
String은 문자열타입이다. 문자/문자열을 저장한다.  
문자열을 만들 때는 싱글 따옴표(')나 더블 따옴표(")로 감싸준다.  
`+` 연산을 사용해서 문자열을 조합할 수 있다.  
`템플릿 문자열`을 이용하면 + 연산을 사용하지 않고 문자열을 만들 수 있다.  
템플릿 문자열을 만들땐 백틱(`)으로 감싸준다. 변수는 ${}로 감싸준다.

```javascript
let foo = 'hello';
let boo = 'world';

// + 연산자
let result1 = foo + ' ' + boo;

// 템플릿 문자열
let result2 = `${foo} ${boo}`;
```

6. Object  
Object는 `속성`과 `메소드`를가지고 있는 데이터 타입이다.  
JavaScript에서 가장 쉽게 접할 수 있는 것으로 `json`이 있다.  
Object는 `key: value`의 형태로 구성되어 있다.  
key를 이용하여 속성이나 메소드를 접근할 수 있다.

```javascript
let foo = {
    a: 1,           // 속성
    b: 2,           // 속성
    c: () => 10     // 메소드
};
```

8. Array  
Array는 연속적인 데이터를 저장하는 타입이다.  

```javascript
let foo = [1, 2, 3, 4, 5];
```