Created: 202401111956
Tags: #cs-intermediate 

---
### Reference

Oh god damn that was a tough topic. However, I've got it all sorted out. Let's look how it works step-by-step! *(according to the MacOS)*

>[!caution]
Before we start you need to install: **Docker** and **Azure Data Studio**

// *Increase RAM allocation for Docker. I would suggest increasing to 4GB* //

Open the *Docker* application and leave it opened. Next, open a terminal to **Create** and **Run** a container for the Image by using this command:

```shell
docker run -e "ACCEPT_EULA=1" -e "MSSQL_USER=SA" -e "MSSQL_SA_PASSWORD=SQLConnect1" -e "MSSQL_PID=Developer" -p 1433:1433 -d --name=sql_connect mcr.microsoft.com/azure-sql-edge
```

^2dfe07

Next, check if the container if running:

```shell
docker container ls -a
```

Stop and Start Container:

```shell
docker stop sql_connect
docker start sql_connect
```

**GOOD**. After you made this *background* steps you must open **Azure Data Studio**. 
Tap a **"New"** button and then click on the **"New Connection"**. 

Fill in the next fields *as follows* (==MacOS==):

>[!info]
>Server: localhost
>Authentication Type: SQL Login
>User name: sa
>Password: SQLConnect1

If you use ==WIndows== fill only **Server** as a *localhost* and **Authentication Type** as a *Windows Authentication*! 

IF YOU HAVE THIS:

>[!error]
>A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server).

Hopefully, you are not fucked up! (For me personal) This happen because I had been forgotten to do this step before launching Azure Data Studio:

![[Database Connection#^2dfe07]]

So, if you do exactly the same as me and you still have this issue - shit happens :(. Try to find something on the stackoverflow. 

Okay, otherwise, if everything is good - congratulations!

>[!success]

* * *
After we finished the most difficult part, let's install some packages, create a database, connect it into the code and do some queries. 

Okay, now click on the "localhost" in the left upper corner and choose *"New Query"*. In the clear field paste this code:

```sql
CREATE DATABASE DotNetCourseDatabase
GO

USE DotNetCourseDatabase
GO

CREATE SCHEMA TutorialAppSchema
GO

CREATE TABLE TutorialAppSchema.Computer(
    ComputerId INT IDENTITY(1,1) PRIMARY KEY,
    Motherboard NVARCHAR(50),
    CPUCores INT,
    HasWifi BIT,
    HasLTE BIT,
    ReleaseDate DATE,
    Price DECIMAL(18,4),
    VideoCard NVARCHAR(50)
);
```

^47e055

It will create the database according to the instructions from the code. Also, you can check if it actually created by commenting all previous code and running:

```sql
SELECT * FROM TutorialAppSchema.Computer
```

Let's add some packages. Write next lines in a terminal. 

**[[Dapper]]**
```shell
dotnet add package Dapper
```

**Microsoft SQLClient** (provides connection to the Microsoft SQL servers)
```shell
dotnet add package microsoft.data.sqlclient
```

**Entity Framework**
```shell
dotnet add package microsoft.data.entityframeworkcore
```

**Entity Framework SQLServer** (to provide access to sql servers from the entity framework) 
```shell
dotnet add package microsoft.data.entityframeworkcore.sqlserver
```

You can check if they was successfully installed in the *YourProjectName.csproj* file. 

* * *

We finished all "outside" work, now we are going to write some code. 

Firstly, we need to make a connection to the database starting from a *connection string:* ^16a212

==MacOS==
```cs
string connection = "Server=localhost;Database=DotNetCourseDatabase;TrustServerCertificate=true;Trusted_Connection=false;User Id=sa;Password=SQLConnect1;";
```

^7c61d0


==Windows==
```cs
string connection = "Server=localhost;Database=DotNetCourseDatabase;TrustServerCertificate=true;Trusted_Connection=true;Password=SQLConnect1;";
```

>[!info]
>The only difference between these two OS in the *User Id* and *Password* part. Because of **Trusted_Connection** is absent in the MacOS (cause it is a Microsoft feature) - we must make it ==false== and then write user id and password. On the contrary, windows users can just write **Trusted_Connection=true**; and thats all. 

Next code utilizes Dapper to connect to a SQL Server database, execute a query fetching the current date and time, and stores the result in a DateTime variable (`rightNow`).

```cs
IDbConnection dbConnection = new SqlConnection(connection);
string sqlCommand = "SELECT GETDATE()"; 

// dbConnection.Query<DateTime>(sqlCommand);
DateTime rightNow = dbConnection.QuerySingle<DateTime>(sqlCommand);
```

>[!info]
>1. Establish a connection to a relational database using Dapper and assign it to an `IDbConnection` variable named `dbConnection`.
>   -
>   
>2. Define a SQL query string (`sqlCommand`) to retrieve the current date and time using the SQL Server `GETDATE()` function.
>   -
> 
>3. Execute the SQL query and retrieve the result as a `DateTime` object, storing it in the `rightNow` variable.


---
### Zero-Links

1. 

-------
### Links

1. 