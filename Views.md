# Views

* Views are used sort of like methods in C#
* You can create a view which will act like a SELECT statement by using aliases.
* Some reasons to use views are security, simplicity, and reuseablility.

  * You always want to use 'V' which stands for view.
  
```SQL
IF OBJECT_ID('StaffList', 'V') IS NOT NULL
    DROP VIEW StaffList
GO
CREATE VIEW StaffList
AS
    SELECT  FirstName + ' ' + LastName AS 'StaffFullName'
    FROM    Staff
GO

-- Now we can use the StaffList view as if it were a table
SELECT  StaffFullName
FROM    StaffList
-- SP_HELPTEXT StaffList    -- Gets the text of the View
-- SP_HELP StaffList        -- Gets schema info on the View
GO
```


* You can also alter views
```SQL
--2.  Create a view of staff ID's, full names, positionID's and datehired called StaffConfidential.
IF OBJECT_ID('StaffConfidential', 'V') IS NOT NULL
    DROP VIEW StaffConfidential
GO
CREATE VIEW StaffConfidential
AS
    SELECT  StaffID,
            FirstName + ' ' + LastName AS 'FullName',
            PositionID,
            DateHired
    FROM    Staff
GO
-- I can use it accordingly:
SELECT  FullName, DateHired
FROM    StaffConfidential
GO
--2a. Alter the StaffConfidential view so that it includes the position name.
ALTER VIEW StaffConfidential
AS
    SELECT  StaffID,
            FirstName + ' ' + LastName AS 'FullName',
            P.PositionID,
            PositionDescription AS 'PositionName',
            DateHired
    FROM    Staff S
        INNER JOIN Position P ON S.PositionID = P.PositionID
GO
SELECT  FullName, PositionName, PositionID
FROM    StaffConfidential
GO
```
