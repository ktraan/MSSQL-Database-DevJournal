# Joins

## Inner Joins

* Inner joins are used to join two tables together 
```SQL
--1.	Select Student full names and the course ID's they are registered in.
SELECT  FirstName + ' ' + LastName AS 'Full Name',
        CourseId
FROM    Student -- Start the FROM statement by identifying one of the tables you want
    INNER JOIN Registration -- Identify another table you are connection to
        -- ON is where we specify which columns should be used in the relationship
        ON Student.StudentID = Registration.StudentID
```

* You can have multiple joins
```SQL
--1.a. Select Student full names, the course ID and the course name that the students are registered in.
SELECT  FirstName + ' ' + LastName AS 'FullName',
        C.CourseId,
        CourseName
FROM    Student AS S
    INNER JOIN Registration AS R
        ON S.StudentID = R.StudentID    -- ON helps us identify MATCHING data
    INNER JOIN Course AS C
        ON R.CourseId = C.CourseId
```

* This code snippet shows how DISTINCT and ORDER BY are used with a join
```SQL
--2.	Select the Staff full names and the Course ID's they teach.
--      Order the results by the staff name then by the course Id
SELECT  DISTINCT -- The DISTINCT keyword will remove duplate rows from the results
        FirstName + ' ' + LastName AS 'Staff Full Name',
        CourseId
FROM    Staff S
    INNER JOIN Registration R
        ON S.StaffID = R.StaffID
ORDER BY 'Staff Full Name', CourseId
```

* You can also have a WHERE clause to have a condition before it selects the data
```SQL
--5.	Select the Student full name, course names and marks for studentID 199899200.
-- TODO: Student Answer Here...
SELECT  FirstName + ' ' + LastName AS 'Student',
        CourseName,
        Mark
FROM    Student S
    INNER JOIN Registration R ON R.StudentID = S.StudentID
    INNER JOIN Course C ON C.CourseId = R.CourseId
WHERE   S.StudentID = '199899200'
```
```SQL
--8.	What is the course list for student ID 199912010 in semester 2001S. Select the Students Full Name and the CourseNames
-- TODO: Student Answer Here...
SELECT  FirstName + ' ' + LastName AS 'Student',
        CourseName
--        , S.StudentID -- Used for WHERE clause
--        , R.Semester  -- Used for WHERE clause
FROM    Student S
    INNER JOIN Registration R ON S.StudentID = R.StudentID
    INNER JOIN Course C       ON R.CourseId = C.CourseId
WHERE   S.StudentID = 199912010
  AND   R.Semester = '2001S'
```
* You can also use inner joins with aggregate functions
```SQL
SELECT  CourseName, AVG(Mark) AS 'Average Mark'
FROM    Registration R
    INNER JOIN Course C ON R.CourseId = C.CourseId
GROUP BY CourseName
ORDER BY 'Average Mark' DESC
```


## Left Outer Joins

* Left outer joins work the same as inner joins, but left outer joins will return null data
* For LOJ, you must be careful with the tables you are trying to join. 
* The table to the left will return all of it's matching rows
```SQL
SELECT  FirstName  + ' ' + LastName AS 'Student Name',
        AVG(Mark) AS 'Average'
FROM    Student S
    LEFT OUTER JOIN Registration R
        ON S.StudentID  = R.StudentID
GROUP BY FirstName, LastName
```

```SQL
--8. How many second-year courses have the staff taught? Include all the staff and their job position.
-- A second year couse is one where the number portion of the CourseId starts with a '2'
SELECT  FirstName + ' ' + LastName AS 'Staff Name',
        PositionDescription AS 'Job Position',
        COUNT(CourseId) AS '2nd Year Courses'
FROM    Position P
    LEFT OUTER JOIN Staff S
        ON P.PositionID = S.PositionID
    LEFT OUTER JOIN Registration R
        ON S.StaffID = R.StaffId
WHERE   CourseId LIKE 'DMIT2%'
GROUP BY FirstName, LastName, PositionDescription
```

```SQL
--10. Display the names of all students who have not made a payment.

SELECT FirstName + ' ' + LastName AS 'Students that have not paid'
FROM   Student S
    LEFT OUTER JOIN Payment P
        ON S.StudentID = P.StudentID
GROUP BY FirstName, LastName
HAVING COUNT(Amount) <= 0
```
