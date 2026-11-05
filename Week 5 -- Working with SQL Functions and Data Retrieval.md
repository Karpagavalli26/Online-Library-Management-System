# Online Library Management System -- (Weeks 5)

## Week 5 -- Working with SQL Functions and Data Retrieval

### 1. What is a SQL Function?

A function accepts an input value and returns a result. Oracle provides built-in functions for numeric calculations, text manipulation, dates, data conversion and group calculations.

### 2. Number Functions

| Function | Purpose | Example |
|---|---|---|
| ROUND(n, d) | Rounds a number | ROUND(125.678, 2) → 125.68 |
| TRUNC(n, d) | Truncates decimal places | TRUNC(125.678, 2) → 125.67 |
| MOD(m, n) | Returns remainder | MOD(17, 5) → 2 |
| ABS(n) | Absolute value | ABS(-25) → 25 |

**SQL Query:**

```sql
SELECT book_id, price,
       ROUND(price, 0) AS rounded_price,
       MOD(book_id, 2) AS remainder
FROM BOOK;
```

### 3. Character Functions

| Function | Purpose | Example |
|---|---|---|
| UPPER(text) | Uppercase | UPPER('oracle') → ORACLE |
| LOWER(text) | Lowercase | LOWER('SQL') → sql |
| INITCAP(text) | Initial capital letters | INITCAP('online library') → Online Library |
| LENGTH(text) | Character count | LENGTH('BOOK') → 4 |
| SUBSTR(text, start, length) | Extracts part of text | SUBSTR('DATABASE',1,4) → DATA |
| INSTR(text, search) | Finds position | INSTR('ORACLE','A') → 3 |
| TRIM(text) | Removes leading/trailing spaces | TRIM(' SQL ') → SQL |

**SQL Query:**

```sql
SELECT member_id,
       UPPER(member_name) AS member_name_upper,
       LENGTH(member_name) AS name_length
FROM MEMBER;
```

### 4. Date Functions

| Function | Purpose | Example |
|---|---|---|
| SYSDATE | Current database date and time | SYSDATE |
| ADD_MONTHS(date,n) | Adds months | ADD_MONTHS(SYSDATE, 1) |
| MONTHS_BETWEEN(d1,d2) | Difference in months | MONTHS_BETWEEN(SYSDATE, join_date) |
| LAST_DAY(date) | Last day of month | LAST_DAY(SYSDATE) |
| NEXT_DAY(date,'MONDAY') | Next named weekday | NEXT_DAY(SYSDATE,'MONDAY') |

**SQL Query:**

```sql
SELECT member_id, member_name, join_date,
       ADD_MONTHS(join_date, 12) AS renewal_date
FROM MEMBER;
```

### 5. Conversion Functions

- **TO_CHAR:** Converts a number or date to character format.
- **TO_DATE:** Converts character data to a DATE using a format model.
- **TO_NUMBER:** Converts character data to a number.

Use explicit formats to avoid ambiguity.

**SQL Queries:**

```sql
SELECT TO_CHAR(SYSDATE, 'DD-MON-YYYY') AS today
FROM DUAL;

SELECT TO_DATE('31-DEC-2026', 'DD-MON-YYYY') AS sample_date
FROM DUAL;

SELECT TO_NUMBER('1250') + 50 AS total
FROM DUAL;
```

### 6. Aggregate (Group) Functions

| Function | Purpose |
|---|---|
| COUNT(*) | Counts rows |
| SUM(column) | Adds numeric values |
| AVG(column) | Calculates average |
| MIN(column) | Finds minimum |
| MAX(column) | Finds maximum |

**SQL Query:**

```sql
SELECT COUNT(*) AS total_books,
       AVG(price) AS average_price,
       MIN(price) AS lowest_price,
       MAX(price) AS highest_price
FROM BOOK;
```

### 7. GROUP BY and HAVING

GROUP BY creates groups of rows with the same value. Aggregate functions calculate a result for each group.

HAVING filters groups after grouping, whereas WHERE filters individual rows before grouping.

**SQL Query 1: GROUP BY**

```sql
SELECT category_id, COUNT(*) AS book_count
FROM BOOK
GROUP BY category_id;
```

**SQL Query 2: GROUP BY with HAVING**

```sql
SELECT category_id, COUNT(*) AS book_count
FROM BOOK
GROUP BY category_id
HAVING COUNT(*) > 1
ORDER BY category_id;
```

---

## 8. Inserting Records into Tables

### 8.1 CATEGORY RECORDS

```sql
INSERT INTO CATEGORY VALUES (1,'Computer Science','Programming and Database Books');
INSERT INTO CATEGORY VALUES (2,'Mathematics','Mathematics Reference Books');
INSERT INTO CATEGORY VALUES (3,'Literature','English Literature Books');
```

### 8.2 AUTHOR RECORDS

```sql
INSERT INTO AUTHOR VALUES (1,'Abraham Silberschatz','Database Systems Author');
INSERT INTO AUTHOR VALUES (2,'E Balagurusamy','Programming Author');
INSERT INTO AUTHOR VALUES (3,'R S Aggarwal','Mathematics Author');
INSERT INTO AUTHOR VALUES (4,'William Shakespeare','Literature Author');
```

### 8.3 PUBLISHER RECORDS

```sql
INSERT INTO PUBLISHER VALUES (1,'Tech Publications','9876500001');
INSERT INTO PUBLISHER VALUES (2,'Education Books','9876500002');
```

### 8.4 MEMBER RECORDS

```sql
INSERT INTO MEMBER VALUES (101,'Arun Kumar','arun@gmail.com','9000000001',TO_DATE('01-01-2026','DD-MM-YYYY'),'STUDENT');
INSERT INTO MEMBER VALUES (102,'Bala Devi','bala@gmail.com','9000000002',TO_DATE('05-01-2026','DD-MM-YYYY'),'STUDENT');
INSERT INTO MEMBER VALUES (103,'Charan Raj','charan@gmail.com','9000000003',TO_DATE('10-01-2026','DD-MM-YYYY'),'STAFF');
INSERT INTO MEMBER VALUES (104,'Divya Sri','divya@gmail.com','9000000004',TO_DATE('15-01-2026','DD-MM-YYYY'),'STUDENT');
INSERT INTO MEMBER VALUES (105,'Elango','elango@gmail.com','9000000005',TO_DATE('20-01-2026','DD-MM-YYYY'),'STUDENT');
```

### 8.5 BOOK RECORDS

```sql
INSERT INTO BOOK VALUES (201,'ISBN001','Oracle Database',1,1,1,650,5,4);
INSERT INTO BOOK VALUES (202,'ISBN002','Python Programming',1,2,1,500,4,3);
INSERT INTO BOOK VALUES (203,'ISBN003','Java Programming',1,2,2,550,6,5);
INSERT INTO BOOK VALUES (204,'ISBN004','Mathematics for Engineers',2,3,2,400,5,5);
INSERT INTO BOOK VALUES (205,'ISBN005','English Literature',3,4,1,350,3,3);
```

### 8.6 BOOK ISSUE RECORDS

```sql
INSERT INTO BOOK_ISSUE VALUES (301,201,101,TO_DATE('01-10-2026','DD-MM-YYYY'),TO_DATE('15-10-2026','DD-MM-YYYY'),'RETURNED');
INSERT INTO BOOK_ISSUE VALUES (302,202,102,TO_DATE('05-10-2026','DD-MM-YYYY'),TO_DATE('19-10-2026','DD-MM-YYYY'),'ISSUED');
INSERT INTO BOOK_ISSUE VALUES (303,203,103,TO_DATE('07-10-2026','DD-MM-YYYY'),TO_DATE('21-10-2026','DD-MM-YYYY'),'RETURNED');
INSERT INTO BOOK_ISSUE VALUES (304,204,101,TO_DATE('10-10-2026','DD-MM-YYYY'),TO_DATE('24-10-2026','DD-MM-YYYY'),'ISSUED');
INSERT INTO BOOK_ISSUE VALUES (305,205,104,TO_DATE('12-10-2026','DD-MM-YYYY'),TO_DATE('26-10-2026','DD-MM-YYYY'),'RETURNED');
```

### 8.7 BOOK RETURN RECORDS

```sql
INSERT INTO BOOK_RETURN VALUES (401,301,TO_DATE('14-10-2026','DD-MM-YYYY'),0,'PAID');
INSERT INTO BOOK_RETURN VALUES (402,303,TO_DATE('20-10-2026','DD-MM-YYYY'),0,'PAID');
INSERT INTO BOOK_RETURN VALUES (403,305,TO_DATE('25-10-2026','DD-MM-YYYY'),10,'PAID');
```

### 8.8 COMMIT

**Description:** Saves all inserted records permanently in the database.

```sql
COMMIT;
```

---

**End of Week 5 – SQL Functions and Data Retrieval**
