---
title:  "[Java Script] 조건문, 반복문, Array Object 고급 사용법" 
excerpt: "Java Script 필수 문법 2"

categories:
  - Java Script

toc: true
toc_sticky: true
 
date: 2023-08-01
last_modified_at: 2023-08-01

---
## 조건문
기본구문

```javascript
if (조건) {
    // ... 실행될 코드 ...
}
```

if ~ else
```javascript
if (조건1){
    // ... 코드1 ...
} else if (조건2) {
    // ... 코드2 ...
} else if (조건3) {
    // ... 코드3 ...
} else {
    // ... 코드4 ...
} 
```

## 반복문
기본구문 (for 문)

```javascript
for (초기문; 조건문; 증감문) {
    // ... 실행될 코드 ...
}
```

```javascript
for (let i = 0; i < 3; i++) {
    console.log(i);
}
```

기본구문 (for ~ in 문)

```javascript
for (index in [Array 또는 Object]) {
    // ... 실행될 코드...
}
```

for ~ in은 객체나 배열을 이용하여 반복문을 돌리는 방법이다.  
조건문이나 증감문이 없더라도 배열 길이만큼 반복할 수 있다.  
객체의 모든 키값을 접근하여 사용할 수 있다.

```javascript
let l = [10, 20, 30, 40];
for (index in l) {
    console.log(index, l[index]);
}

// 결과
// 0 10
// 1 20
// 2 30
// 3 40
```

```javascript
let l = {foo: 1, boo: 2};
for (key in l) {
    console.log(key, l[key]);
}

// 결과
// foo 1
// boo 2
```

## Array 고급 사용법
Array는 데이터 삽입, 길이, 검색, 제거를 할 수 있다.  
push() : 배열 가장 마지막 요소에 추가  
pop() : 배열 마지막 요소를 지우면서 반환  
length : 배열의 길이 반환

```javascript
let foo = [];   // let foo = new Array(); 로도 생성 가능

console.log(foo.length);    // foo 길이 출력 : 0

foo.push(1);     // foo에 1 삽입
foo.push("1");   // foo에 "1" 삽입

console.log(foo, foo[0], foo[1]);    // [1, '1'] 1 "1"

console.log(foo.length);    // foo 길이 출력 : 2
console.log(foo.pop());     // 마지막 요소를 제거한 후 반환 : "1" 
console.log(foo.length);    // foo 길이 출력 : 1
console.log(foo.pop());     // 마지막 요소를 제거한 후 반환 : 1
console.log(foo.length);    // foo 길이 출력 : 0
```

indexOf() : 배열에서 요소를 찾고 인덱스를 반환, 존재하지 않으면 -1을 반환

```javascript
let foo = [10, 20, 30, 40, 50];

console.log(foo.indexOf(30));       // 2
console.log(foo.indexOf(100));       // -1
```

배열은 자체적으로 반복문을 돌릴 수 있다.

```javascript
let foo = [10, 20, 30, 40, 50];

foo.forEach(function (item, index, array) {
    console.log(item, index, array);
});

// 결과
// 10 0 [10, 20, 30, 40, 50]
// 20 1 [10, 20, 30, 40, 50]
// 30 2 [10, 20, 30, 40, 50]
// 40 3 [10, 20, 30, 40, 50]
// 50 4 [10, 20, 30, 40, 50]
```

반복문을 돌리면서 특정 값들만 필터링을 해야 한다면 forEach 대신 `filter`를 사용

```javascript
let foo = [10, 11, 20, 21, 30, 31];

let newFoo = foo.filter(function (item, index, array) {
    if (item % 10 == 0) {   // 10의 배수 검사
        return true;        // true를 반환하면 newFoo에 item 추가
    }
});

console.log(newFoo);        // [10, 20, 30]
```

## Object 고급 사용법
JavaScript는 모든 것을 객체로 취급한다.  
객체는 프로퍼티(속성)와 메소드(함수)로 이루어져 있다.
hasOwnProperty()는 해당 객체에 키값이 있는지 검사한다.

```javascript
let foo = {"a": 10, "b": 3};     // new Object({"a": 10, "b": 3})
console.log(foo, foo["a"], foo["b"]);   // {a: 10, b: 3} 10 3

foo["c"] = 30;   // 프로퍼티 추가
console.log(foo);    // {a: 10, b: 3, c: 30}

console.log(foo.hasOwnProperty('a'), foo.hasOwnProperty('asd'));
// true, false
```