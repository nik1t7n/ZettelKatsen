Created: 202401261956
Tags: #sql_basics

---
### Reference

Oh, we are finally here! I have already bought a PC on windows but the lessons will be on Mac btw. Here we are going to repeat [[Database Connection#^47e055|creation of our Computer table]]. Let's start!

Create the database, start to use it and then create a schema:
```sql
CREATE DATABASE DotNetCourseDatabase
GO

USE DotNetCourseDatabase
GO

CREATE SCHEMA TutorialAppSchema
GO
```
The **GO** word basically says that everything after GO statement is a separate query. So, if we don't type this statement - something might be wrong or works not as we wanted. 

Next, we created the schema. It uses for logical division of the database field. Exactly here we divided Computer model. Schema also allows to isolate and control the elements more flexible. 

Then, we are going to create the table itself:
```sql
CREATE TABLE TutorialAppSchema.Computer
(
	-- it will automatically write and increment values. IDENTITY(starting, to_increment)
	
	ComputerId INT IDENTITY(1,1) PRIMARY KEY -- PK provides always a unique value here. also it sorts data in table by this field
	
	-- , Motherboard CHAR(10) -> "x": "x "
	-- , Motherboard VARCHAR(10) -> "x": "x"
	
	, Motherboard NVARCHAR(50) -- can handle unicode symbols
	, CPUCores INT
	, HasWifi BIT -- one or zero
	, HasLTE BIT
	, ReleaseDate DATETIME
	, Price DECIMAL(18, 4) -- 18 whole number size and 4 digits after the point
	, VideoCard NVARCHAR(50)
)

GO
```
As I wrote in the comments, 

>[!tip] IDENTITY && PRIMARY KEY
>**IDENTITY** automatically gives a value to the field. We can specify *START* and *INCREMENT* values. 
>**PRIMARY KEY** ensures that the value will be always unique and it sorts the field by this values. 

^2a6f4c

Likewise, there are three types of "*Strings*" here. 
1. **CHAR(n)** – reserves all specified space. If we reserved 10 and typed only *"X"*, the result will be "X         "!
2. **VARCHAR(n)** is more flexible. It also has maximum value but it will take exactly the same symbols as we specified. 
3. **NVARCHAR(n)** - the same as VARCHAR but it can handle non-unicode symbols too, such as "@#$%^&" etc. 

Instead of *BOOL* we used **BIT** because it is absolutely the same (0 or 1). Then we used **DECIMAL** due to its huge size. The whole number size and amount of digits after point can be specified too. 

And lastly let's *SELECT* all data from the table:
```sql
SELECT * FROM TutorialAppSchema.Computer
```


---
### Zero-Links

1. 

-------
### Links

1. 