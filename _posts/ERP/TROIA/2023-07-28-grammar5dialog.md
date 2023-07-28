---
title:  "[TROIA 문법] Dialog" 
excerpt: "TROIA 문법 Dialog"

categories:
  - Troia

toc: true
toc_sticky: true
 
date: 2023-07-28
last_modified_at: 2023-07-28

---
## Dialog
> Dialog는 사용자가 특정 작업을 수행할 수 있는 사용자 인터페이스 양식이다.  
> Dialog의 주요 구성 요소는 컨트롤(버튼, 텍스트 필드, 콤보 상자, 그래픽 등 사용자 상호 작용)이다.  
> Dialog에서 메서드를 정의하고 다른 사람으로부터 메소드를 호출하여 동작을 추가할 수 있다.  

### Dialog 창 생성/편집
![troia dialog create1](/assets/images/file/troia/troia13.png)  
CODE DB에서 TROIA IDE 항목 클릭

![troia dialog create2](/assets/images/file/troia/troia14.png)  
TROIA IDE -> New -> New Dialog  
Hotline : 핫라인 선택  
Name : 다이얼로그 이름  
Caption : 다이얼로그 설명  
Base Dialog : 상속할 다이얼로그

### 기본 Dialog 이벤트
이벤트는 특정 작업이 발생할 때 시스템에서 자동으로 호출하는 미리 정의된 메서드이다.  

가장 많이 사용되는 Dialog 이벤트

| 이름     | 설명                                                    |
|:-------|:------------------------------------------------------|
| Before | 다이얼로그 창이 열릴 때 첫 번째 이벤트, 컨트롤 정의 후 시작됨 (다이얼로그가 표시되지 않음) |
| After  | 'Before' 이벤트 이후에 시작되었지만 다이얼로그는 여전히 표시되지 않음            |
| Onshow | 사용자 인터페이스에 다이얼로그가 표시될 때, 'After' 이벤트후에 시작됨            |

### 컨트롤 : TextField
TextField및 제어 기호 유형의 하위 유형  

| Sub Type     | Type     | Key Features                                    | 
|:-------------|:---------|:------------------------------------------------|
| Text         | STRING   | 짧은 문자열을 입력받기 위한 기본 하위 유형                        |
| Editor       | STRING   | 큰 텍스트를 받기 위한 방법                                 |
| File Chooser | STRING   | 파일 경로를 얻기 위해 내장 파일 선택기를 사용                      |
| Troia Editor | STRING   | TROIA 코드를 문자열로 얻거나 표시하기 위해 내장된 formmater를 사용    |
| Password     | STRING   | 비밀번호를 얻거나 표시하는 방법                               |
| Decimal      | DECIMAL  | Decimal 값들을 얻거나 표시하는 방법                         |
| Long         | LONG     | Long 값들을 얻거나 표시하는 방법                            |
| Integer      | INTEGER  | Integer 값들을 얻거나 표시하는 방법                         |
| Date         | DATE     | 날짜를 얻거나 표시하기 위해 내장된 날짜 선택기를 zoom과 함께 사용         |
| Datetime     | DATETIME | 날짜와 시간을 얻거나 표시하기 위해 내장된 날짜와 시간 선택기를 zoom과 함께 사용 |

TextField의 기본 이벤트

| Event       | Description & Event Fire            |
|:------------|:------------------------------------|
| GainFocus   | 사용자가 Text Field에 집중할 때              |
| LoseFocus   | 사용자가 Text Field 뒤의 다른 컨트롤로 커서를 옮길 때 |
| TextChanged | 사용자가 Text Field의 값을 변경하면 포커스를 잃기 전에 |

### Dialog 전환 (CALL DIALOG)
- 다이얼로그를 여는 두가지 주요 방법
  1. 트랙잭션의 시작 다이얼로그로 다이얼로그 정의
     - 시스템은 트랜잭션이 열리면 자동으로 시작 다이얼로그를 호출
  2. TROIA 코드를 통해 다이얼로그 호출
     - `CALL DIALOG` 명령을 작성하여 다이얼로그 전환

- CALL DIALOG 구문
```java
CALL DIALOG {dialog};
CALL DIALOG WITH LOCATION {x}, {y} SIZE {width},{height};       /* <-- 팝업으로 호출 */
```

### Dialog 닫기 (SHUTDOWN)
CALL DIALOG 명령은 실행중인 메서드에서 코드 실행을 중지하고 클라이언트에서 새 다이얼로그를 연다.  
다이얼로그를 닫음려면 `SHUTDOWN` 명령을 사용해야 한다.  
SHUTDOWN 명령은 마지막으로 열린 다이얼로그를 닫고 이전 다이얼로그로 전환한다.  
닫힌 다이얼로그가 트랜잭션 시스템의 마지막 다이얼로그이면 자동으로 트랜잭션을 닫는다.  

- SHUTDOWN 구문
```java
SHUTDOWN;
```

TROIA에서 값 또는 변수를 다이얼로그에 전송할때 이전 다이얼로그에서 정의한 제어 기호 값을 그대로 사용 가능하다.  
다이얼로그가 닫힌 후 `닫힌 다이얼로그에 의해 정의된 전역 변수는 메모리에서 제거되지 않으므로` 여전히 사용 가능하다.  
따라서 프로그래머는 새 변수와 컨트롤을 정의할 때 닫힌 다이얼로그의 기호 이름과 유현을 고려해야한다.