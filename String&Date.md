# String and Date Functions

## String Functions

```SQL
-- LEN
SELECT LEN('Hello World') AS 'Number of characters'
-- LEFT
SELECT LEFT('Hello World', 5) AS 'First five characters'
-- RIGHT
SELECT RIGHT('Hello World', 5) AS 'Last five characters'

  SELECT LEFT(FirstName,1) + '.' + LEFT(LastName,1) + '.' AS 'Staff Initials'
  FROM   Staff
  ORDER BY 1 -- sorted by the first column

-- SUBSTRING
SELECT SUBSTRING('Hello World', 1, 2)
-- REVERSE
  SELECT REVERSE('Dan')
  -- (Club whose id is an anagram)
  -- Select the insert statement below to add a row into the Club table
  -- INSERT INTO Club(ClubId, ClubName) VALUES ('ABCBA', 'Active Bat Catching Brotherhood Assoc.')
SELECT	ClubId, ClubName
FROM	Club
WHERE   ClubId = REVERSE(ClubId)
-- Modifying
  -- LTRIM, RTRIM -- To remove whitespace from the left or the right
  -- UPPER, LOWER -- Return upper and lower characters
```
## Date Functions
```SQL
-- GETDATE()
SELECT GETDATE() AS 'Database Server- Current Date/Time'
-- DATENAME - See https://msdn.microsoft.com/en-CA/library/ms174395.aspx for DateParts
SELECT DATENAME(MONTH, GETDATE()) AS 'Database Server- Current Month'
-- DATEPART - Similar to above
SELECT DATEPART(WEEKDAY, GETDATE()) AS 'Day of the week',
       DATENAME(WEEKDAY, GETDATE()) AS 'Day of the week'
-- DAY
-- MONTH -- Birthdays this month - Student.Birthdate
  SELECT FirstName, MONTH(Birthdate) AS 'Birth Month' FROM Student
  WHERE  MONTH(Birthdate) = DATEPART(MONTH, GETDATE())
-- YEAR
-- DATEDIFF - Staff.DateHired - DateReleased
SELECT FirstName + ' ' + LastName AS 'Staff Name',
       DATEDIFF(DAY, DateHired, DateReleased) AS 'Days Employed'
         -->> DateReleased - DateHired, expressed as number of Days
FROM   Staff
WHERE  DateReleased IS NOT NULL

-- DATEADD
SELECT DATEADD(DAY, 7, GETDATE()) AS 'Date a week from now'
-- ISDATE
SELECT ISDATE(GETDATE()) AS 'GETDATE() Info',
       ISDATE('Hi Dan') AS 'Not a Date'
```

* SELECTS with  string/date functions

```SQL
-- 1. Select the staff names and the name of the month they were hired
SELECT  FirstName, LastName, DATENAME(mm, DateHired) AS 'Month Hired'
FROM    Staff


-- 2a. How long have I worked for this school??
SELECT  DATEDIFF(dd, 'Jan 1, 2000', GETDATE())


-- 3. How Many Students where born in each month? Display the Month Name and the Number of Students.
SELECT  DATENAME(mm, Birthdate) AS 'Month Name',
        COUNT(1) AS 'Number of Students'
FROM    Student
GROUP BY DATENAME(mm, Birthdate)


-- 5. Select all the course names that have grades from 2004. NOTE: the first 4 characters of the semester indicate the year.
SELECT  DISTINCT
        CourseName
FROM    Registration R
    INNER JOIN Course C ON C.CourseId = R.CourseId
WHERE   Mark IS NOT NULL
  AND   LEFT(Semester, 4) = 2004
