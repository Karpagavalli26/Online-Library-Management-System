# Online Library Management System -- (Weeks 6)

## Week 6 -- Implementing SQL Operators and Joins

### 1. SQL Operators

| Operator Group | Operators / Examples | Purpose |
|---|---|---|
| Arithmetic | `+`, `-`, `*`, `/` | Calculate values |
| Comparison | `=`, `<>`, `>`, `<`, `>=`, `<=` | Compare values |
| Logical | `AND`, `OR`, `NOT` | Combine conditions |
| Special | `IN`, `BETWEEN`, `LIKE`, `IS` | Match a list, range, pattern or NULL |
| Set | `UNION`, `INTERSECT`, `MINUS` | Combine query results |

### 2. Special Operator Examples

**BETWEEN Operator**
```sql
SELECT TITLE
FROM BOOK
WHERE PRICE BETWEEN 300 AND 700;
```

**IN Operator**
```sql
SELECT TITLE
FROM BOOK
WHERE CATEGORY_ID IN (1,2);
```

**LIKE Operator**
```sql
SELECT TITLE
FROM BOOK
WHERE TITLE LIKE 'O%';
```

**IS NULL Operator**
```sql
SELECT MEMBER_NAME
FROM MEMBER
WHERE EMAIL IS NULL;
```

- `LIKE` uses `%` for zero or more characters and `_` for exactly one character.
- `BETWEEN` includes both boundary values.
- NULL must be tested using `IS NULL` or `IS NOT NULL`, not `= NULL`.

### 3. Why Joins Are Needed

Related information is stored in separate normalized tables. A join combines columns from related tables so a report can show readable information, such as a book title with the member who borrowed it.

### 4. INNER JOIN

```sql
SELECT ISSUE_ID, MEMBER_NAME, TITLE
FROM BOOK_ISSUE I
INNER JOIN MEMBER M
ON I.MEMBER_ID = M.MEMBER_ID
INNER JOIN BOOK B
ON I.BOOK_ID = B.BOOK_ID;
```

INNER JOIN returns rows where the join condition matches in both tables.

### 5. LEFT OUTER JOIN

```sql
SELECT M.MEMBER_NAME, I.ISSUE_ID
FROM MEMBER M
LEFT OUTER JOIN BOOK_ISSUE I
ON M.MEMBER_ID = I.MEMBER_ID;
```

LEFT OUTER JOIN returns all rows from the left table and matching rows from the right table. Unmatched right-side columns display NULL.

### 6. SELF JOIN

```sql
SELECT B1.TITLE, B2.TITLE
FROM BOOK B1
JOIN BOOK B2
ON B1.CATEGORY_ID = B2.CATEGORY_ID
AND B1.BOOK_ID < B2.BOOK_ID;
```

A self join joins a table to itself. This query compares books that belong to the same category.

### 7. NATURAL JOIN

```sql
SELECT CATEGORY_NAME, TITLE
FROM CATEGORY
NATURAL JOIN BOOK;
```

NATURAL JOIN automatically joins columns with the same name and compatible data types. Use it carefully because matching column names determine the join condition.

### 8. CROSS JOIN

```sql
SELECT CATEGORY_NAME, AUTHOR_NAME
FROM CATEGORY
CROSS JOIN AUTHOR;
```

CROSS JOIN returns the Cartesian product. Every category is paired with every author.

### 9. Set Operators

Set operators combine the results of two SELECT statements. Each SELECT must return the same number of columns, in the same order, with compatible data types.

**UNION**
```sql
SELECT MEMBER_ID FROM BOOK_ISSUE
UNION
SELECT MEMBER_ID FROM BOOK_RETURN;
```

**INTERSECT**
```sql
SELECT MEMBER_ID FROM BOOK_ISSUE
INTERSECT
SELECT MEMBER_ID FROM BOOK_RETURN;
```

**MINUS**
```sql
SELECT MEMBER_ID FROM BOOK_ISSUE
MINUS
SELECT MEMBER_ID FROM BOOK_RETURN;
```

**Set Operators Using ISSUE_ID**

```sql
SELECT ISSUE_ID FROM BOOK_ISSUE
UNION
SELECT ISSUE_ID FROM BOOK_RETURN;
```

```sql
SELECT ISSUE_ID FROM BOOK_ISSUE
INTERSECT
SELECT ISSUE_ID FROM BOOK_RETURN;
```

```sql
SELECT ISSUE_ID FROM BOOK_ISSUE
MINUS
SELECT ISSUE_ID FROM BOOK_RETURN;
```

- `UNION` returns distinct rows from both queries.
- `INTERSECT` returns rows common to both queries.
- `MINUS` returns rows from the first query that are absent from the second query.

### 10. Summary

| Topic | Commands Covered |
|---|---|
| Special Operators | BETWEEN, IN, LIKE, IS NULL |
| Joins | INNER JOIN, LEFT OUTER JOIN, SELF JOIN, NATURAL JOIN, CROSS JOIN |
| Set Operators | UNION, INTERSECT, MINUS |
