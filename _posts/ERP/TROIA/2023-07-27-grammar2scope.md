---
title:  "[TROIA 문법] Varialbles and Scope" 
excerpt: "TROIA 문법 Varialbles and Scope"

categories:
  - Troia

toc: true
toc_sticky: true
 
date: 2023-07-27
last_modified_at: 2023-07-27

---
## Scope
> TROIA 에는 전역(Global), 멤버(Member), 로컬(Local)의 세 가지 수준의 범위가 있다.

### 전역 범위 (Global Scope)
변수가 전역 변수로 정의된 경우 소프트웨어의 모든 부분에서 액세스할 수 있다.  
TROIA에서 가장 큰 범위이며 `트랜잭션`에 의해 제한된다.  
즉, 전역 변수를 정의하면 모든 항목이 트랜잭션에서 실행되는 경우  
모든 Dialog 또는 클래스 메서드/이벤트에서 액세스할 수 있다.

### 멤버 범위 (Member Scope)
정의된 클래스의 모든 메서드에서 액세스할 수 있다.  
멤버 변수는 클래스의 각 인스턴스에 대해 정의된다.  
클래스 인스턴스 멤버 변수에 액세스하려면 `@` 연산자가 사용된다.
Ex) INSTANCE1 @ XPOS : INSTANCE1 이라는 클래스 인스턴스의 XPOS 멤버 변수

### 로컬 범위 (Local Scope)
정의된 메소드/이벤트에서만 액세스할 수 있다. 

## 변수 정의 명령
### GLOBAL 명령  
```java
/* 단일 변수 정의 */
GLOBAL:
    STRING STRINGVAR1;
    
/* 다중 변수 정의 */
GLOBAL:
    STRING STRINGVAR1,
    STRING STRINGVAR2,
    TABLE TABLEVAR1,            /* <--- 인터널 테이블 */
    INTEGER INTVAR,
    MYCLASS MYCLASSREC;         /* <--- 클래스 클래스변수 */
```

### MEMBER 명령
생성자 등을 포함한 클래스 메서드에서만 사용할 수 있으므로 Dialog, Report 등에서 Member 명령을 사용할 수 없다.
```java
/* 단일 변수 정의 */
MEMBER:
    STRING STUDENTNAME;

/* 다중 변수 정의 */
MEMBER:
    STRING FIRSTNAME,
    STRING LASTNAME,
    TABLE ITEMLIST,
    INTEGER XPOSITION,
    MYCLASS MYCLASSREC;
```

### LOCAL 명령
```java
/* 단일 변수 정의 */
LOCAL:
    STRING STRINGVAR1;

/* 다중 변수 정의 */
LOCAL:
    STRING STRINGVAR1,
    STRING STRINGVAR2,
    TABLE TABLEVAR1,
    INTEGER INTVAR,
    MYCLASS MYCLASSREC;
```

### OBJECT 명령
OBJECT 명령은 가장 오래되고 가장 많이 사용되는 변수 정의 명령이다.  
OBJECT 명령으로 변수를 정의하면 데이터 유형과 사용되는 방법에 따라 범위가 달라진다.  

|                                      | Dialog/Report<br/>Event&Method | Class<br/>_CONSTRUCTOR&_VARIABLES | Class<br/>Method |
|:-------------------------------------|:-------------------------------|:----------------------------------|:-----------------|
| **Table**                            | Global                         | Global                            | Global           |
| **Class<br/>Instance**               | Global                               | Global                            | Global           |
| **Simple Types<br/>(STRING, TABLE, ...)** | Global                               | Member                            | Local            |  

```java
/* 단일 변수 정의 */
OBJECT:
    STRING STRINGVAR1;

/* 다중 변수 정의 */
OBJECT:
    STRING STRINGVAR1,
    STRING STRINGVAR2,
    TABLE TABLEVAR1,
    INTEGER INTVAR,
    MYCLASS MYCLASSREC;
```

## 시스템 변수
> 시스템, 사용자 세션 또는 일부 특정 작업에 대한 정보를 저장하는 미리 정의된 변수이다.

| 시스템 변수          | 설명                              |
|:----------------|:--------------------------------|
| SYS_CURRENTDATE | 현재 시각 (ex.11.07.2023 09:18:18 ) |
| SYS_CLIENT      | 로그인 사용자가 사용하는 클라이언트 정보 (ex. 00) |
| SYS_LANGU       | 로그인 사용자가 사용하는 언어 (ex. KO)       |
| SYS_USER        | 로그인 사용자 ID (ex. hjyeo)          |
| CONFIRM         | 확인 메시지에서 선택한 값 (ex. YES or NO)  |
