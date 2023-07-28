---
title:  "[TROIA 문법] Messages" 
excerpt: "TROIA 문법 Messages"

categories:
  - Troia

toc: true
toc_sticky: true
 
date: 2023-07-28
last_modified_at: 2023-07-28

---
## MESSAGE COMMAND
![troia massage](/assets/images/file/troia/troia15.png)
> 프로그래머는 팝업 메시지를 사용하여 사용자에게알리거나 확인, 옵션과 같은 중요한 데이터를 얻는다.  
> TROIA 에서 이러한 메시지를 표시하려면 `MESSAGE` 명령을 사용한다.

- MESSAGE 구문
```java
MESSAGE {module} {messagetype}{messageid} WITH {inputparamsformessagetext};

/* 예시 구문 */
MESSAGE BAS C100 WITH;
```

메세지 유형

| 유형    | 코드 | 내용         |
|:------|:---|:-----------|
| 정보    | I  | 정보 아이콘     |
| 오류    | E  | 오류 아이콘     |
| 경고    | W  | 경고 아이콘     |
| 확인    | C  | 예/아니오 질문   |
| 옵션    | O  | 맞춤 옵션      |
| 매개 변수 | P  | 사용자 키보드 입력 |

### 사용자 응답 및 시스템 변수 읽기
확인, 옵션, 매개 변수 메시지 유형은 어떤 옵션이 선택되었는지 또는 사용자가 입력한 텍스트를 읽어야한다.  
사용자 응답은 `CONFIRM` 및 `SYS_CONFIRMTEXT` 시스템 변수로 설정되므로 값을 읽을 수 있다.  
확인 메시지인 경우 사용자가 예 옵션을 선택하면 CONFIRM 시스템 변수가 YES로 설정되고 아니면 NO로 설정된다.

```java
MESSAGE BAS C100 WITH;

IF CONFIRM == 'YES' THEN 
    STRINGVAR1 = 'User said: yes!';
ELSE
    STRINGVAR1 = 'User said: no!';
ENDIF;
```