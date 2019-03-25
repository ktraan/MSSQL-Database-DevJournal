# Constraints, Altered Tables, Non-clustered indexes

* Constraints
  * Constraints are used to place a constraint on an attribute in a table. 
  * It is used on PK, FK, or normal attributes.
  * They can also have a CHECK, where it will CHECK the condition before creating the table

```SQL
 CustomerNumber  int
     -- The following is a PRIMARY KEY constraint that has a specific name
     -- Primary Key constraints ensure a row of data being added to the table
     -- will have to have a unique value for the Primary Key column(s)
     CONSTRAINT PK_Customers_CustomerNumber
         PRIMARY KEY

 CustomerNumber  int
     -- Foreign Key constraints ensure that when a row of data is being
     -- inserted or updated, there is a row in the referenced table
     -- that has the same value as its Primary Key
     CONSTRAINT FK_Orders_CustomerNumber_Customers_CustomerNumber
         FOREIGN KEY REFERENCES
         Customers(CustomerNumber)   NOT NULL,

 CurrentSalePrice    money
     CONSTRAINT CK_InventoryItems_CurrentSalePrice
         CHECK (CurrentSalePrice > 0)    NOT NULL,
```           

  * There can also be IDENTITY on a check constraint.
  * This means that the database will generate a unique whole number
  * IDENTITY(seedNumber, increment)

```SQL
 CustomerNumber  int
      CONSTRAINT PK_Customers_CustomerNumber
         PRIMARY KEY
         IDENTITY(100, 1) -- The first number is the "seed",
                          -- and the last number is the "increment
```

* ALTER TABLE is used to change an attribute of the table
  * It is used for adding constraints without having to change the CREATE TABLE statements.
```SQL
ALTER TABLE Client
	ADD Email			varchar(100)		
		CONSTRAINT CK_Client_Email
			CHECK (Email LIKE '%_@_%._%')	
												NULL
```

* Non-clustered indexes are for improving the performance of the database when retrieving information
```SQL
CREATE NONCLUSTERED INDEX IX_Customers_FirstName
    ON Customers (FirstName)
CREATE NONCLUSTERED INDEX IX_Customers_LastName
    ON Customers (LastName)
GO -- End of a batch of instructions
```
