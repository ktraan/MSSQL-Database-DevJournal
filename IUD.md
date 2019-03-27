# Insert, Update, Delete

## Insert
```SQL
-- The syntax for the INSERT statement is 
INSERT INTO TableName(Comma, Seperated, Listof, ColumnNames)
VALUES ('A', 'Value', 'Per', 'Column')

-- 1. Let's add a new course called "Expert SQL". It will be a 90 hour course with a cost of $450.00
INSERT INTO Course(CourseId, CourseName, CourseHours, CourseCost)
VALUES ('DMIT777', 'Expert SQL', 90, 450.00)

-- Another syntax for the INSERT statement is to use a SELECT clause in place of the VALUES clause.
-- This is used for zero-to-many possible rows to insert.

INSERT INTO Staff(FirstName, LastName, DateHired, PositionID)
VALUES ('Shane', 'Bell', GETDATE(), 
        (SELECT PositionID
        FROM   Position
        WHERE  PositionDescription = 'Instructor'))
        
-- Multiple inserts
-- 3. There are three additional clubs being started at the school:
--      - START - Small Tech And Research Teams
--      - CALM - Coping And Lifestyle Management
--      - RACE - Rapid Acronym Creation Experts
--    SELECT * FROM Club
INSERT INTO Club(ClubId, ClubName)
VALUES ('START', 'Small Tech And Research Teams'),
       ('CALM', 'Coping And Lifestyle Management'),
       ('RACE', 'Rapid Acronym Creation Experts')
```    

## Update

```SQL
-- The syntax for the UPDATE statement is 

UPDATE  TableName
-- the SET Portion is a comma seperated list of assignment statements
SET     ColumnName = Expression,    
        Column2 = Expression
WHERE   ConditionalExpression

1. Increase the course cost by 10%
UPDATE Course
SET    CourseCost = CourseCost * 1.10
WHERE  CourseName IN ('Expert SQL', 'Quality Assurance')
-- Should see 2 rows affected

-- 4. Someone in the registrar's office has noticed a bunch of data-entry errors.
--    All the student cities named 'Edm' should be changed to 'Edmonton'
UPDATE Student
SET    City = 'Edmonton'
WHERE  City = 'Edm'
```

## Delete

```SQL
1. Remove all the members of the CSS club.
DELETE FROM Activity
WHERE  ClubID = 'CSS'

2. Remove the club from the Club's table.
DELETE FROM Club
WHERE  ClubID = 'CSS'

-- 3. The student "Flying Nun" has withdrawn from the school. Remove this student from all clubs they are participating in.
DELETE FROM Activity
WHERE  StudentID IN (SELECT StudentID
                     FROM Student
                     WHERE FirstName = 'Flying'
                       AND LastName = 'Nun')
```
