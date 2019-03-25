# Simple Selects

> This is an intro into writing SQL scripts. We use different clauses that can help us query the database.

```SQL
--  Select first names and last names of the students.
SELECT  FirstName, LastName
FROM    Student
```

- The WHERE clause is used to give a CONDITION to the query.
```SQL
--5. Select the Staff names who have positionID of 3
SELECT FirstName, LastName,
       PositionID 
FROM   Staff
WHERE  PositionID = 3
```
- WHERE clause can use:
1. = (The equals will compare the result as a string or numerical value)
2. LIKE (The LIKE clause will compare the string value character by character)
2a. (This is where wildcards are used, such as _ or % or [])
2b. _ represents a single character
2c. % represents zero or more characters
2d. [] is a patteren for single character matching what is inside the brackets(ie. postalcode)
