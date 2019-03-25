# Simple Selects 2

## The following will go over Aggregate functions of AVG(), SUM(), COUNT()
## Also will go over GROUP BY, ORDER BY, HAVING clauses

#### Aggregate functions will return a single value and by doing so will require a GROUP BY clause

* AVG() will create an average
* SUM() will create a sum
* COUNT() will return the count of the attribute

```SQL
SELECT  AVG(Mark) AS 'Average Mark',
        SUM(Mark) AS 'Total of Marks',
        COUNT(Mark) AS 'How Many Marks'
FROM    Registration
```

#### The WHERE clause can also be used to give the function a condition

```SQL
SELECT  COUNT(Mark) AS 'Student Count for DMIT152'
FROM    Registration
WHERE   CourseId = 'DMIT152'
```

#### The GROUP BY clause will group the non-aggregate functions to group together the duplicates

```SQL
SELECT  CourseId,                   -- This column is a non-aggregate
        AVG(Mark) AS 'Average Mark' -- This column performs Aggregate (produce 1 value)
FROM    Registration
GROUP BY CourseId    
```

#### The ORDER BY clause will order the result, can be either ASCending or DESCending.
#### By default, ORDER BY wil be ASC

```SQL
SELECT  PaymentTypeID,                              -- Non-aggregate column (btw, it's a FK)
        COUNT(PaymentTypeID) AS 'Count of Pay Type' -- Aggregate column
FROM    Payment
GROUP BY PaymentTypeID
ORDER BY COUNT(PaymentTypeID) ASC


#### The HAVING clause will filter the aggregate values
* It is usually used with a comparison operator (>, >=, =, <, <=)
```SQL
Select the average Mark for each studentID. Display the StudentId and their average mark
SELECT StudentID,
       AVG(Mark) AS 'Avg Mark'
FROM   Registration
GROUP BY StudentID
-- The HAVING clause is where we do filtering of Aggregate information
HAVING AVG(Mark) > 80
```
