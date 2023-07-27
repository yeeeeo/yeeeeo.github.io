---
title:  "[TROIA 문법] Data Types" 
excerpt: "TROIA 문법 Data Types"

categories:
  - Troia

toc: true
toc_sticky: true
 
date: 2023-07-27
last_modified_at: 2023-07-27

---
## Data Type  

| Data Type     | Ex (Default Value)                    |
|:--------------|:--------------------------------------|
| INTEGER       | 5 (0)                                 |
| LONG          | 12312312 (0)                          |
| DECIMAL       | 1.32 (0.0)                            |
| BOOLEAN       | 0 or 1 (0)                            |
| DATETIME      | 29.10.1923 16:30:30 (Definition Time) |
| DATE          | 29.10.1923 (Definition Time)          |
| TIME          | 21:30                                 |
| TIMES         | 21:30:13                              |
| STRING        | 'Hello World' (Empty String)          |
| STRINGBUILDER | (Empty String)                        |
| TABLE         |                                       |

- STRINGBUILDER
STRINGBUILDER는 문자열 작성 작업 전용으로 설계된 기호 유형과 같은 문자열이다.  
STRING 대신 STRINGBUILDER 변수를 사용하면 문자열 연결 성능이 크게 향상된다.  
<u>문자열 연결에서 더 높은 성능을 얻으려면 '+' 연산자 대신 APPENDSTRING 명령을 사용해야한다.</u>
STRINGBUILDER와 STRING 사이에 다른 특징은 없지만 문자열 연결을 제외하고  
일반 문자열 작업에서 STRING 대신 STRINGBUILDER 유형을 사용하지 않는 것이 좋다.  

## 키워드 및 식별자

| 이름            | 이름        | 이름         | 이름           | 이름       |
|:--------------|:----------|:-----------|:-------------|:---------|
| GET           | IF        | MARKERSET  | RETURNVALUE  | COPY     |
| EXECUTE       | MESSAGE   | SELECT     | MARKERPOINT  | RETURN   |
| BREAK         | DECIMAL   | INSERT     | MOVE         | SELECTED |
| BREAKPOINT    | DELETE    | INSERTED   | NOTFOUND     | SET      |
| CALL          | DELETED   | ZOOMID     | NOTSELECTED  | SQL      |
| CLASS         | DEQUE     | JAVA       | NULL         | ZOOM     |
| CLEAR         | ENQUE     | VOID       | PAGENUM      | WHILE    |
| CONFIRM       | ENTITYID  | LOOP       | RETURN       | SWITCH   |
| TRUE          | TIMES     | FALSE      | UPDATED      | ZOOMFYI  |
| PUT           | BEGINTRAN | COMMITTRAN | ROLLBACKTRAN | BOOLEAN  |
| STRINGBUILDER |           |            |              |          |

