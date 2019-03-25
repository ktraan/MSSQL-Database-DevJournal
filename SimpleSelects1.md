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
* = (The equals will compare the result as a string or numerical value)
* LIKE (The LIKE clause will compare the string value character by character)
  *(This is where wildcards are used, such as _ or % or [])
  * _ represents a single character
  * % represents zero or more characters
  * [] is a patteren for single character matching what is inside the brackets(ie. postalcode)
* BETWEEN (BETWEEN sets a range of values, therefore needing a minimum and maximum value)
* IS (Used for NULL or NOT NULL)
  


```SQL
--11. Select the CourseID's and CourseNames where the CourseName contains the word 'programming'
SELECT	CourseId, CourseName
FROM	Course
WHERE	CourseName LIKE 'programming%'

--13. Select Student Names, Street Address and City where the lastName is only 3 letters long.
SELECT	FirstName, LastName, StreetAddress, City
FROM	Student
WHERE	LastName LIKE '___' -- 3 underscores


--14. Select all the StudentID's where the PaymentAmount < 500 OR the PaymentTypeID is 5
SELECT	StudentID
FROM	Payment
WHERE	Amount BETWEEN 0 AND 500 OR PaymentTypeID LIKE '5'
```

