---
title:  "[MSSQL] T-SQL date function" 
excerpt: "MSSQL T-SQL date function"

categories:
  - Mssql

toc: true
toc_sticky: true
 
date: 2023-07-26
last_modified_at: 2023-07-26

---
### DATEPART  
| DATEPART    | 단축명      | 설명                   |
|:------------|:---------|:---------------------|
| YEAR        | yy, yyyy | 년                    |
| MONTH       | mm, m    | 월                    |
| DAY         | dd, d    | 일                    |
| QUARTER     | qq, q    | 분기                   |
| DAYOFYEAR   | dy, y    | 년도의 몇째일              |
| WEEK        | wk, ww   | 년도의 몇째주              |
| WEEKDAY     | dw       | 요일(1 = 일요일, 7 = 토요일) |
| HOUR        | hh       | 시간                   |
| MINUTE      | mi, n    | 분                    |
| SECOND      | ss, s    | 초                    |
| MILLISECOND | ms       | 밀리초                  |  

### DATEADD()
- DATEADD(datepart, 빼거나 더할 값, 날짜)
- 날짜의 datepart에 해당하는 부분을 빼거나 더한 만큼 반환
```sql
SELECT  DATEADD(MONTH, 1, '2006-03-29'),
        DATEADD(DAY, 1, '2006-03-29'),
        DATEADD(MONTH, -1, '2006-03-29'),
        DATEADD(DAY, -1, '2006-03-29')
```  
| DATEADD(MONTH, 1, '2006-03-29') | DATEADD(DAY, 1, '2006-03-29') | DATEADD(MONTH, -1, '2006-03-29') | DATEADD(DAY, -1, '2006-03-29') |
|:--------------------------------|:------------------------------|:---------------------------------|:-------------------------------|
| 2006-04-29                      | 2006-03-30                    | 2006-02-28                       | 2006-03-28                     |  

### DATEDIFF()
- DATEDIFF(datepart,날짜1, 날짜2)
- 날짜1과 날짜2의 datepart에 해당하는 부분의 차이를 반환
```sql
SELECT  DATEDIFF(MONTH, '2006-03-29', '2006-07-29'),
        DATEDIFF(DAY, '2006-03-20', '2006-03-29'),
        DATEDIFF(WEEK, '2006-03-20', '2006-03-29')
```  
| DATEDIFF(MONTH, '2006-03-29', '2006-07-29') | DATEDIFF(DAY, '2006-03-20', '2006-03-29') | DATEDIFF(WEEK, '2006-03-20', '2006-03-29') |
|:--------------------------------------------|:------------------------------------------|:-------------------------------------------|
| 4                                           | 9                                         | 1                                          |  

### DATEPART(), DATENAME()
- DATEPART(datepart, 날짜), DATENAME(datepart, 날짜)
- DATEPART: 날짜에서 지정된 datepart 부분의 값을 반환
- DATENAME: 날짜에서 지정된 datepart 부분의 이름값을 반환
```sql
SELECT  DATEPART(YEAR, '2006-03-29'),
        DATENAME(YEAR, '2006-03-29')
```  
| DATEPART(YEAR, '2006-03-29') | DATENAME(YEAR, '2006-03-29') |
|:-----------------------------|:-----------------------------|
| 2006                         | 2006                         |  

```sql
SELECT  DATEPART(MONTH, '2006-03-29'),
        DATENAME(MONTH, '2006-03-29')
```  
| DATEPART(MONTH, '2006-03-29') | DATENAME(MONTH, '2006-03-29') |
|:------------------------------|:------------------------------|
| 3                             | 3                             |  
```sql
SELECT  DATEPART(WEEK, '2006-03-29'),
        DATENAME(WEEK, '2006-03-29')
```  
| DATEPART(WEEK, '2006-03-29') | DATENAME(WEEK, '2006-03-29') |
|:-----------------------------|:-----------------------------|
| 13                           | 13                           |  
```sql
SELECT  DATEPART(WEEKDAY, '2006-03-29'),
        DATENAME(WEEKDAY, '2006-03-29')
```  
| DATEPART(WEEKDAY, '2006-03-29') | DATENAME(WEEKDAY, '2006-03-29') |
|:--------------------------------|:--------------------------------|
| 4                               | 수요일                             |  
