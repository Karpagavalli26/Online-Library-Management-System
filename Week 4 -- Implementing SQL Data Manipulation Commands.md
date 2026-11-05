# Online Library Management System -- (Weeks 4)

## Week 4 -- Implementing SQL Data Manipulation Commands

### 1. DML Overview

DML changes the records stored in tables. INSERT adds rows, UPDATE changes existing rows, and DELETE removes selected rows. SELECT retrieves rows and is commonly taught alongside DML in this weekly plan.

### 2. INSERT

**Description:** INSERT is used to add new records into a table.

**Syntax:**

```sql
INSERT INTO table_name (column1, column2)
VALUES (value1, value2);
```

**SQL Queries:**

```sql
INSERT INTO CATEGORY VALUES (1,'Computer Science','Programming Books');
INSERT INTO CATEGORY VALUES (2,'Mathematics','Math Books');

INSERT INTO AUTHOR VALUES (1,'A Kumar','Database Author');
INSERT INTO AUTHOR VALUES (2,'R Meena','Programming Author');

INSERT INTO PUBLISHER VALUES (1,'Tech Books','9876500001');

INSERT INTO MEMBER VALUES
(101,'Arun Kumar','arun@mail.com','9000000001',SYSDATE,'STUDENT');

INSERT INTO MEMBER VALUES
(102,'Bala Devi','bala@mail.com','9000000002',SYSDATE,'STUDENT');

INSERT INTO BOOK VALUES
(201,'ISBN001','Oracle Database',1,1,1,650,5,5);

INSERT INTO BOOK VALUES
(202,'ISBN002','Python Basics',1,2,1,500,4,4);

INSERT INTO BOOK_ISSUE VALUES
(301,201,101,SYSDATE,SYSDATE+14,'ISSUED');

COMMIT;
```

**Expected Result:** Records are inserted successfully into the respective tables.

### 3. UPDATE

**Description:** UPDATE modifies existing records in a table.

```sql
UPDATE BOOK
SET AVAILABLE_COPIES=4
WHERE BOOK_ID=201;
```

**Expected Result:** 1 row updated.

### 4. ROLLBACK

**Description:** ROLLBACK cancels uncommitted changes.

```sql
ROLLBACK;
```

**Expected Result:** The previous uncommitted changes are cancelled.

### 5. SELECT, WHERE and ORDER BY

**Description:** SELECT retrieves records, WHERE filters records based on conditions, and ORDER BY sorts the results.

```sql
SELECT * FROM BOOK;

SELECT * FROM MEMBER;

SELECT TITLE,PRICE
FROM BOOK
WHERE PRICE>400
ORDER BY PRICE DESC;
```

### 6. CASE Expression

**Description:** CASE returns a value based on specified conditions.

```sql
SELECT TITLE,
CASE
WHEN AVAILABLE_COPIES>0 THEN 'AVAILABLE'
ELSE 'NOT AVAILABLE'
END STATUS
FROM BOOK;
```

### 7. Substitution Variables in SQL*Plus

**Description:** The ampersand (&) asks the user to enter a value when the query executes.

```sql
SELECT TITLE
FROM BOOK
WHERE CATEGORY_ID=&CATEGORY_NO;
```

### 8. Transaction Control

**Description:**

- **COMMIT:** Saves changes permanently.
- **ROLLBACK:** Cancels uncommitted changes.
- **SAVEPOINT:** Creates a point to which a transaction can be rolled back.

**SQL Query:**

```sql
UPDATE BOOK
SET AVAILABLE_COPIES=AVAILABLE_COPIES-1
WHERE BOOK_ID=201;

SAVEPOINT after_update;

ROLLBACK TO after_update;

ROLLBACK;
```

---

**End of Week 4 – SQL Data Manipulation Commands**
