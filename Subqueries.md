# Subqueries

* Subqueries are a query within a query. 
  * It is usually found within a WHERE or HAVING clause
```SQL

--1. Select the Payment dates and payment amount for all payments that were Cash
SELECT PaymentDate, Amount
FROM   Payment
WHERE  PaymentTypeID = -- Using = means that the RH side must be a single value
    -- Assuming that every PaymentTypeDescription will be UNIQUE,
    -- The following subquery will return a single column and a single row
    (SELECT PaymentTypeID
     FROM   PaymentType
     WHERE  PaymentTypeDescription = 'cash')
-- Here is the Inner Join version of the above
SELECT PaymentDate, Amount
FROM   Payment P
    INNER JOIN PaymentType PT
            ON PT.PaymentTypeID = P.PaymentTypeID
WHERE  PaymentTypeDescription = 'cash'


--2. Select The Student ID's of all the students that are in the 'Association of Computing Machinery' club
-- TODO: Student Answer Here
SELECT  StudentID
FROM    Activity
WHERE   ClubId = 
        (SELECT ClubId
         FROM   Club
         WHERE  ClubName = 'Association of Computing Machinery')
```


* Subqueries can help find the highest value in a certain attribute
```SQL
-- To get the payment type IDs whose count is greater than or equal to all the others
-- (i.e.: whose count is the highest)
SELECT  PaymentTypeID
FROM    Payment
GROUP BY PaymentTypeID
HAVING COUNT(PaymentTypeID)  >= ALL (SELECT COUNT(PaymentTypeID)
                                     FROM Payment 
                                     GROUP BY PaymentTypeID)
                                     
                                     
--7. Select the Payment Type Description(s) that have the highest number of Payments made.
SELECT PaymentTypeDescription
FROM   Payment 
    INNER JOIN PaymentType 
        ON Payment.PaymentTypeID = PaymentType.PaymentTypeID
GROUP BY PaymentType.PaymentTypeID, PaymentTypeDescription 
HAVING COUNT(PaymentType.PaymentTypeID) >= ALL (SELECT COUNT(PaymentTypeID)
                                                FROM Payment 
                                                GROUP BY PaymentTypeID)                                     
```
