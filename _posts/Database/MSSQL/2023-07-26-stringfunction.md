---
title:  "[MSSQL] T-SQL string function" 
excerpt: "MSSQL T-SQL string function"

categories:
  - Mssql

toc: true
toc_sticky: true
 
date: 2023-07-26
last_modified_at: 2023-07-26

---
### LEFT(), RIGHT()
- LEFT(문자열, 정수), RIGHT(문자열, 정수)
- LEFT() : 문자열의 왼쪽부터 정수 길이만큼 반환
- RIGHT() : 문자열의 오른쪽부터 정수 길이만큼 반환
```sql
SELECT  LEFT(Country, 3) AS Left3_CountryName,
        RIGHT(Country, 3) AS Right3_CountryName,
        Country
FROM    Customers
```
| **Left3_CountryName** | Right3_CountryName | Country | 
|:----------------------|:-------------------|:--------| 
| Ger                   | any                | Germany |
| Mex                   | ico                | Mexico  |
| Mex                   | ico                | Mexico  |
| UK                    | UK                 | UK      |
| ...                   | ...                | ...     |

### LEN()
- LEN(문자열)
- 문자열의 길이를 반환
```sql
SELECT  LEN(Country) AS CountryNameLength,
        Country
FROM    Customers
```
| **CountryNameLength** | Country | 
|:----------------------|:--------| 
| 7                     | Germany |
| 6                     | Mexico  |
| 6                     | Mexico  |
| 2                     | UK      |
| ...                   | ...     |

### LOWER(), UPPER()
- LOWER(문자열), UPPER(문자열)
- LOWER : 문자열을 소문자로 변환
- UPPER : 문자열을 대문자로 변환
```sql
SELECT  LOWER(Country) AS LowerCountry,
        UPPER(Country) AS UpperCountry,
        Country
FROM    Customers
```
| **LowerCountry** | UpperCountry | Country | 
|:-----------------|:-------------|:--------| 
| germany          | GERMANY      | Germany |
| mexico           | MEXICO       | Mexico  |
| mexico           | MEXICO       | Mexico  |
| uk               | UK           | UK      |
| ...              | ...          | ...     |

### LTRIM(), RTRIM()
- LTRIM(문자열), RTRIM(문자열)
- LTRIM : 문자열 왼쪽의 공백 제거
- RTRIM : 문자열 오른쪽의 공백 제거
```sql
SELECT  'A' + LTRIM(RTRIM('  BC  ')) + 'D' AS RTRIM_LTRIM_STR,
        'A' + '  BC  ' + 'D' AS NOTRIM_STR
```
| **RTRIM_LTRIM_STR** | NOTRIM_STR | 
|:--------------------|:-----------| 
| ABCD                | A BC D     |

### REPLICATE()
- REPLICATE(문자열, 정수)
- 지정된 횟수만큼 문자열 반복
```sql
SELECT  RIGHT(REPLICATE('0', 10) + '123', 10) AS REPLACE_0
```
| **REPLACE_0** |
|:--------------|
| 0000000123    |

### SUBSTRING()
- SUBSTRING(문자열, 시작, 길이)
- 문자열의 시작부터 길이만큼 추출
```sql
SELECT  SUBSTRING(CustomerID, 2, 2) AS SUBSTRING_CustomerID,
        CustomerID
FROM    Customers
```
| **SUBSTRING_CustomerID** | CustomerID | 
|:-------------------------|:-----------| 
| LF                       | ALFKI      |
| NA                       | ANATR      |
| NT                       | ANTON      |
| RO                       | AROUT      |
| ...                      | ...        |