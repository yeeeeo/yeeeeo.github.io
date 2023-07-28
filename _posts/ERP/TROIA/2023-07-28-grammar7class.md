---
title:  "[TROIA 문법] Classes" 
excerpt: "TROIA 문법 Classes"

categories:
  - Troia

toc: true
toc_sticky: true
 
date: 2023-07-28
last_modified_at: 2023-07-28

---
## Class
> TROIA 클래스는 특성으로서의 멤버와 기능으로서의 메소드, 초기설정을 하는 생성자를 가진 소프트웨어 구조이다.  
> TROIA 클래스가 기능을 나타내는 멤버 필드를 저장할 수 있더라도 일부 동작을 추가하는 `메소드 집합`으로 간주된다.  

### 클래스 생성/편집
![troia class](/assets/images/file/troia/troia16.png)  
TROIA IDE -> New -> New Class  
Hotline : 핫라인 선택  
Name : 클래스 이름  
Base Class : 상속할 클래스  
Short Description : 클래스에 대한 간단한 설명  

### 클래스의 기본 메소드
클래스는 `_VARIABLES`, `_CONSTRUCTOR`라는 이름의 미리 정의된 메소드를 가진다.  
변수 정의를 통한 새 클래스 인스턴스를 정의할 때 이 메소드를 호출한다.  
클래스 이니셜라이저(Class Initializer) 방식이라고 하며 객체지향 프로그래밍 언어의 생성자와 유사하다.  

- _VARIABLES : 멤버 및 기타 필수 변수를 정의
- _CONSTRUCTOR : 클래스 인스턴스의 내부 구조 빌드

### 클래스 인스턴스 정의
'MATHTEST' 클래스의 인스턴스 정의
```java
OBJECT:
    MATHTEST MATHREC;
```

클래스 인스턴스를 정의하기 위해 변수 정의 명령을 실행하면 클래스 이니셜라이저 메서드가 실행된다.  
그러나 동일한 인스턴스가 두번 이상 정의된 경우에도 이니셜라이저 메소드는 한번만 실행된다.

### 클래스 메소드 불러오기
MATHTEST 클래스의 SUM() 메소드 호출  

```java
OBJECT:
    MATHTEST CLASSINSTANCE,
    INTEGER RESULT;

RESULT = CLASSINSTANCE.SUM(5, 6);
```
클래스 메소드를 재귀로 정의하고 다른 클래스 메소드 호출 가능
클래스내에 존재하는 메서드를 호출하려면 `THIS` 키워드 사용  

```java
/* text를 리턴하는 클래스내 메소드 */
PARAMETERS:
    INTEGER PA,
    INTEGER PB;
    
LOCAL:
    INTEGER MAXNUM;

/* 클래스 내부엔 MAX()라는 다른 메소드 존재 */
MAXNUM = THIS.MAX(PA, PB);
RETURN 'Maxinum number is ' + MAXNUM;
```

### 클래스 멤버 접근
대부분의 프로그래밍 언어에서는 클래스 인스턴스 필드에 액세스할 때 도트(.) 연산자를 사용하지만  
