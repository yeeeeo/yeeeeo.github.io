---
title:  "[TROIA 문법] Operators and Expressions" 
excerpt: "TROIA 문법 Operators and Expressions"

categories:
  - Troia

toc: true
toc_sticky: true
 
date: 2023-07-27
last_modified_at: 2023-07-27

---
## 연산자
> TROIA 인터프리터에게 피연산자를 사용하여 수학적, 관계형 및 논리 연산을 수행하도록 한다.

### 산술 연산자

| 기호 | 의미            |
|:---|:--------------|
| +  | 더하기 or 문자열 연결 |
| -  | 빼기            |
| *  | 곱하기           |
| /  | 몫             |
| %  | 나머지           |
| ^  | 제곱            |

### 관계 연산자

| 기호 | 의미     |
|:---|:-------|
| == | 같다     |
| != | 같지 않다  |
| >  | 크다     |
| >= | 크거나 같다 |
| <  | 작다     |
| <= | 작거나 같다 |

### 논리 연산자

| 기호             | 의미     |
|:---------------|:-------|
| !              | NOT    |
| &&             | AND    |
| &#124;&#124;   | OR     |

## 표현식
### THIS
TROIA 언어에서는 클래스/대화상자의 인스턴스 이름을 지정해야 한다.  
THIS 키워드는 동일한 인스턴스를 나타내는데 사용된다.
```java
CUSTREC.CALCULATE(P1);      /* CUSTREC 클래스의 CALCULATE 메소드 */
THIS.SEARCH(P1);            /* 현재 클래스/다이얼로그의 SEARCH 메소드 */
RESULT = ABS(5 - 10);       /* 시스템 함수 ABS */
```