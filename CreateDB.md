# Creating the Database

**To create a database**

```SQL
CREATE DATABASE [InsertDatabaseNameHere]
USE [DatabaseNameChosen]
GO
```

**The script should begin with DROP TABLE statements. This is to clean up the DB for recreation.**
**The DROP TABLE statements should drop in REVERSE ORDER in which is created**
  
```SQL
IF EXISTS (SELECT * FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'Payment')
    DROP TABLE Payment
IF EXISTS (SELECT * FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'Client')
    DROP TABLE Client
```

**To Create a db table, we use CREATE TABLE statement**
**Note that the order we create and drop tables is important because of how the foreign keys are related**
  
```SQL
CREATE TABLE Client
(  
    ClientID            int
        CONSTRAINT PK_Client_ClientID
        PRIMARY KEY		
		IDENTITY(1,1)						NOT NULL,
    FirstName           varchar(50)			NOT NULL,
    LastName            varchar(50)			NOT NULL,
    Phone               varchar(14)			
		CONSTRAINT CK_Client_Phone
			CHECK (Phone LIKE '([0-9][0-9][0-9]) [0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]')
											NOT NULL,
    Balance             money				NOT NULL
)
CREATE TABLE Payment
(
    PaymentID           int             
        CONSTRAINT PK_Payment_PaymentID
        PRIMARY KEY							NOT NULL,
    [Date]              datetime			NOT NULL,
    Amount              smallmoney			NOT NULL,
    ClientID            int
        CONSTRAINT FK_Payment_ClientID_Client_ClientID
        FOREIGN KEY REFERENCES
        Client(ClientID)					NOT NULL
)
```


