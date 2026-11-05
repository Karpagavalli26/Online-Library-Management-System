# Online Library Management System -- (Weeks 3)

## Week 3 -- Implementing SQL Data Definition Commands

### 1. DDL Overview

DDL (Data Definition Language) is used to create, modify, rename and delete database structures such as tables.

**DDL Commands:**

- CREATE – Creates a new table.
- ALTER – Modifies an existing table.
- RENAME – Changes the table name.
- TRUNCATE – Deletes all records from a table.
- DROP – Deletes the entire table structure.

### 2. CREATE TABLE

**Description:** CREATE TABLE is used to create a new table with specified columns and constraints.

#### 2.1 CATEGORY TABLE

```sql
CREATE TABLE CATEGORY (
    CATEGORY_ID NUMBER(4) PRIMARY KEY,
    CATEGORY_NAME VARCHAR2(40) NOT NULL UNIQUE,
    DESCRIPTION VARCHAR2(100)
);
```

#### 2.2 AUTHOR TABLE

```sql
CREATE TABLE AUTHOR (
    AUTHOR_ID NUMBER(4) PRIMARY KEY,
    AUTHOR_NAME VARCHAR2(60) NOT NULL,
    BIOGRAPHY VARCHAR2(200)
);
```

#### 2.3 PUBLISHER TABLE

```sql
CREATE TABLE PUBLISHER (
    PUBLISHER_ID NUMBER(4) PRIMARY KEY,
    PUBLISHER_NAME VARCHAR2(60) NOT NULL,
    CONTACT_NO VARCHAR2(15)
);
```

#### 2.4 MEMBER TABLE

```sql
CREATE TABLE MEMBER (
    MEMBER_ID NUMBER(5) PRIMARY KEY,
    MEMBER_NAME VARCHAR2(60) NOT NULL,
    EMAIL VARCHAR2(80) UNIQUE,
    PHONE VARCHAR2(15),
    JOIN_DATE DATE DEFAULT SYSDATE,
    MEMBER_TYPE VARCHAR2(10)
);
```

#### 2.5 BOOK TABLE

```sql
CREATE TABLE BOOK (
    BOOK_ID NUMBER(5) PRIMARY KEY,
    ISBN VARCHAR2(20) UNIQUE,
    TITLE VARCHAR2(100) NOT NULL,
    CATEGORY_ID NUMBER(4),
    AUTHOR_ID NUMBER(4),
    PUBLISHER_ID NUMBER(4),
    PRICE NUMBER(8,2),
    TOTAL_COPIES NUMBER(4),
    AVAILABLE_COPIES NUMBER(4),
    FOREIGN KEY (CATEGORY_ID) REFERENCES CATEGORY(CATEGORY_ID),
    FOREIGN KEY (AUTHOR_ID) REFERENCES AUTHOR(AUTHOR_ID),
    FOREIGN KEY (PUBLISHER_ID) REFERENCES PUBLISHER(PUBLISHER_ID)
);
```

#### 2.6 BOOK_ISSUE TABLE

```sql
CREATE TABLE BOOK_ISSUE (
    ISSUE_ID NUMBER(6) PRIMARY KEY,
    BOOK_ID NUMBER(5),
    MEMBER_ID NUMBER(5),
    ISSUE_DATE DATE,
    DUE_DATE DATE,
    RETURN_STATUS VARCHAR2(10),
    FOREIGN KEY (BOOK_ID) REFERENCES BOOK(BOOK_ID),
    FOREIGN KEY (MEMBER_ID) REFERENCES MEMBER(MEMBER_ID)
);
```

#### 2.7 BOOK_RETURN TABLE

```sql
CREATE TABLE BOOK_RETURN (
    RETURN_ID NUMBER(6) PRIMARY KEY,
    ISSUE_ID NUMBER(6),
    RETURN_DATE DATE,
    FINE_AMOUNT NUMBER(8,2),
    PAYMENT_STATUS VARCHAR2(10),
    FOREIGN KEY (ISSUE_ID) REFERENCES BOOK_ISSUE(ISSUE_ID)
);
```

### 3. DESC COMMAND

**Description:** DESC is used to display the structure of an existing table, including column names and data types.

```sql
DESC CATEGORY;
DESC AUTHOR;
DESC PUBLISHER;
DESC MEMBER;
DESC BOOK;
DESC BOOK_ISSUE;
DESC BOOK_RETURN;
```

### 4. ALTER TABLE

**Description:** ALTER TABLE is used to modify the structure of an existing table by adding, modifying or dropping columns.

**SQL Query:**

```sql
CREATE TABLE DDL_PRACTICE (
    TEST_ID NUMBER(3),
    TEST_NAME VARCHAR2(30)
);

ALTER TABLE DDL_PRACTICE ADD REMARKS VARCHAR2(50);
```

### 5. RENAME TABLE

**Description:** RENAME is used to change the name of an existing table.

**SQL Query:**

```sql
RENAME DDL_PRACTICE TO DDL_PRACTICE_NEW;

RENAME DDL_PRACTICE_NEW TO DDL_PRACTICE;
```

### 6. TRUNCATE TABLE

**Description:** TRUNCATE removes all records from a table while keeping its structure.

**SQL Query:**

```sql
TRUNCATE TABLE DDL_PRACTICE;
```

### 7. DROP TABLE

**Description:** DROP is used to delete an entire table, including its structure and records.

**SQL Query:**

```sql
DROP TABLE DDL_PRACTICE;
```

### 8. DDL COMMANDS SUMMARY

| Command | Purpose |
|---|---|
| CREATE | Creates database objects |
| DESC | Displays table structure |
| ALTER | Modifies table structure |
| RENAME | Renames a table |
| TRUNCATE | Deletes all records |
| DROP | Deletes a table completely |

---

**End of Week 3 – SQL Data Definition Commands**
