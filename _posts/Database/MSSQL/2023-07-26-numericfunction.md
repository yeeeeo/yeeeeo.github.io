---
title:  "[MSSQL] T-SQL numeric function" 
excerpt: "MSSQL T-SQL numeric function"

categories:
  - Mssql

toc: true
toc_sticky: true
 
date: 2023-07-26
last_modified_at: 2023-07-26

---
### CEILING()
- CEILING(숫자형)
- 소수점 이하를 무조건 올림
```sql
SELECT  CEILING(1.3), CEILING(2.9)
```

| CEILING(1.3)| CEILING(2.9) |
|:------------|:-------------|
| 2           | 3            |

### FLOOR()
- FLOOR(숫자형)
- 소수점 이하를 무조건 내림
```sql
SELECT  FLOOR(1.9), FLOOR(1.1)
```

| FLOOR(1.9) | FLOOR(1.1) |
|:-----------|:-----------|
| 1          | 1          |

### ROUND()
- ROUND(숫자형, 자릿수)
- 정해진 자릿수에 따라 반올림 (정수 자리는 -1, -2, ...)
```sql
SELECT  ROUND(1.2539, 0), ROUND(1.2539, 1), ROUND(1.2539, 2), ROUND(1.2539, 3)
```

| ROUND(1.2539, 0) | ROUND(1.2539, 1) | ROUND(1.2539, 2) | ROUND(1.2539, 3) |
|:-----------------|:-----------------|:-----------------|:-----------------|
| 1.0000           | 1.3000           | 1.2500           | 1.2540           |