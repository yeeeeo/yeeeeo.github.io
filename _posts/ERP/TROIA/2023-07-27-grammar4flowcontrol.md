---
title:  "[TROIA 문법] Flow Control" 
excerpt: "TROIA 문법 Flow Control"

categories:
  - Troia

toc: true
toc_sticky: true
 
date: 2023-07-27
last_modified_at: 2023-07-27

---
## IF문
### 기본 구문
```java
IF 조건문 THEN
    block
ENDIF;
```

### 예시 구문
```java
INTEGERVAR1 = 5;
INTEGERVAR2 = 10;

IF INTEGERVAR1 < INTEGERVAR2 THEN
    INTEGERVAR3 = INTEGERVAR2;
ENDIF;
```

## IF-ELSE문
### 기본 구문
```java
IF 조건문 THEN
    block
ELSE
    block
ENDIF;
```

### 예시 구문
```java
INTEGERVAR1 = 5;
INTEGERVAR2 = 10;

IF INTEGERVAR1 == INTEGERVAR2 THEN
    INTEGERVAR3 = INTEGERVAR1;
ELSE 
    IF INTEGERVAR1 > INTEGERVAR2 THEN
        INTEGERVAR3 = INTEGERVAR1;
    ELSE
        INTEGERVAR3 INTEGERVAR2;
    ENDIF;
ENDIF;
```

## SWITCH문
TROIA에서 SWITCH문을 사용할 때 BREAK 키워드를 쓰지 않아도 CASE 값이 일치하면 SWITCH문이 종료된다.
### 기본 구문
```java
SWITCH item
    CASE value[, value]:
        case block 1
    CASE value:
        case block 2 
    .
    .
    .
    CASE value:
        case block n
    DEFAULT:
        default block
ENDSWITCH;
```

### 예시 구문
```java
INTEGERVAR1 = 5;

SWITCH INTEGERVAR1
    CASE 1:
        INTEGERVAR2 = INTEGERVAR1;
    CASE 2:
        INTEGERVAR2 = INTEGERVAR1;
    CASE 5:
        INTEGERVAR2 = INTEGERVAR1;
    DEFAULT:
        INTEGERVAR2 = 0;
ENDSWITCH;
```

## WHILE 루프
### 기본 구문
```java
WHILE 조건문
BEGIN
    block
ENDWHILE;
```

### 예시 구문 (1에서 10까지 합계)
```java
INTEGERVAR1 = 1;
INTEGERVAR2 = 0;

WHILE INTEGERVAR1 <= 10
BEGIN
    INTEGERVAR2 = INTEGERVAR2 + INTEGERVAR1;
    INTEGERVAR1 = INTEGERVAR1 + 1;
ENDWHILE;
```

## LOOP 명령
`테이블` 전용 루핑 명령  
구분자로 분할 된 문자열을 루핑할 수 있는 옵션 (PARSE)  
BREAK & CONTINUE

### 기본 구문
```java
LOOP AT 테이블명
BEGIN
    block
ENDLOOP;
```

## 문자열
### 이스케이프 및 특수 문자
TROIA는 하드 코드 문자열(특수 문자, 개행 문자, 띄어쓰기 등)에 대해 이스케이프 문자를 지원하지 않는다.  
이스케이프하는 대신 `TOCHAR()` 시스템 함수를 사용하여 특수 문자를 하드 코드 문자열에 삽입한다.  
TOCHAR() 함수는 요청된 문자의 10진수 ASCII 대응을 가져와 단일 문자를 문자열로 리턴한다.  
Ex. ' -> TOCHAR(39)  
Ex. 개행 문자 -> TOCHAR(10)

### 기본 문자열 함수
문자열 변수에 대한 기본 정보를 반환하는 시스템 함수

| 시스템 함수      | 설명                              |
|:------------|:--------------------------------|
| STRLEN()    | 주어진 문자열의 길이를 반환                 |
| STRPOS()    | 다른 문자열 안에 주어진 문자열의 인덱스를 반환      |
| ISNUMERIC() | 모든 문자가 숫자인지 문자열 확인              |
| STRLIKE()   | SQL LIKE op와 같은 주어진 패턴과 문자열을 비교 |

문자열을 수정하는데 가장 많이 사용되는 시스템 함수

| 시스템 함수      | 설명                          |
|:------------|:----------------------------|
| TRIM()      | 시작과 끝에서 공백을 제거              |
| REPLACE()   | 주어진 문자열을 다른 문자열로 변환         |
| STRSTR()    | 인덱스와 길이가 있는 문자열의 하위 문자열을 반환 |
| LOWERCASE() | 주어진 언어로 주어진 문자열의 소문자를 반환    |
| UPPERCASE() | 주어진 언어로 주어진 문자열의 대문자를 반환    |

### 문자열 루핑 (PARSE)
문자열을 토큰(줄 바꿈 또는 특정 구분 문자 사용)으로 분할하고 각 토큰에 대해 작업을 수행  
PARSE 명령은 일종의 루프 문으로 BREAK & CONTINUE 문은 구문 분석 명령에도 작동

#### 기본 구분
```java
PARSE {mainstring} INTO {token} [DELIMITER {delimiter}]
BEGIN
    parse block
ENDPARSE;
```

#### 예시 구문
```java
STRINGVAR1 = 'a,b,c,d';

PARSE STRINGVAR1 INTO STRINGVAR2 DELIMITER ','
BEGIN
    STRINGVAR3 = STRINGVAR3 + STRINGVAR2;
ENDPARSE;
```

