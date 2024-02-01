Created: 202401121233
Tags: #cs-intermediate 

---
### Reference

In this note we are going to move *Dapper* to its own file to make it more universal.

As usual, we create separate folder and file to this class. Then implement [[Namespaces|namespace]]. The code should look like this: ^0f7e19

```cs
namespace HelloWorld.Data
{
    public class DataContextDapper
    {
        private string _connection = "Server=localhost;Database=DotNetCourseDatabase;TrustServerCertificate=true;Trusted_Connection=false;User Id=sa;Password=SQLConnect1;";
    }
}
```
Here we created a class and the private [[Fields and Properties#^030bbe|field]]. We typed the "\_" before to create semantic difference avoiding possible confusions. 

Let's create some functionality ([[Methods]]) to our class:

```cs
public IEnumerable<T> LoadData<T>(string sql)
{
    IDbConnection dbConnection = new SqlConnection(_connection);
    return dbConnection.Query<T>(sql);
}
```
This method load data (logically) from a database. However, there is one feature - **<\T>**.
It is a generic type. 

>[!info]
>Generic type is a type or method that is defined with one or more type parameters, allowing it to work with various data types without sacrificing type safety.

So, further we can add any class or data structure into our method and it will work perfectly fine!

Next let's create a method that will execute some command to a database:

```cs
public bool ExecuteSql(string sql)
{
	IDbConnection dbConnection = new SqlConnection(_connection);
	return dbConnection.Execute(sql) > 0;
}
```
In general, the logic remains the same. The only thing that may be confusing is bool. We use this because of more often we do not care about [[Dapper#^ddb079|how many rows were affected]]. Then we just need a result - if the command worked or not (true/false). 

Hence, the final code of the class file with additional methods looks like this:

```cs
using System.Data;
using Dapper;
using Microsoft.Data.SqlClient;

namespace HelloWorld.Data
{
    public class DataContextDapper
    {
        private string _connection = "Server=localhost;Database=DotNetCourseDatabase;TrustServerCertificate=true;Trusted_Connection=false;User Id=sa;Password=SQLConnect1;";

		// load all data
        public IEnumerable<T> LoadData<T>(string sql)
        {
            IDbConnection dbConnection = new SqlConnection(_connection);
            return dbConnection.Query<T>(sql);
        }

		// load only one row
        public T LoadDataSingle<T>(string sql)
        {
            IDbConnection dbConnection = new SqlConnection(_connection);
            return dbConnection.QuerySingle<T>(sql);
        }

        public bool ExecuteSql(string sql)
        {
            IDbConnection dbConnection = new SqlConnection(_connection);
            return dbConnection.Execute(sql) > 0;
        }

		// the same as the previous one but with exact number of affected rows
        public int ExecuteSqlWithRowCount(string sql)
        {
            IDbConnection dbConnection = new SqlConnection(_connection);
            return dbConnection.Execute(sql);
        }

    }
}
```

* * *
Next separate part is to create instance of our class into the Main file and replace all previous SQL manipulations to our new functionality. 

Declaring the class using "[[Models#^3af64b|easy assignment]]":
```cs
DataContextDapper dapper = new();
```
And start to replace old code:

```cs
// DateTime rightNow = dbConnection.QuerySingle<DateTime>(sqlCommand);
DateTime rightNow = dapper.LoadDataSingle<DateTime>(sqlCommand);
```

```cs
bool result = dapper.ExecuteSql(sql);

//or

// int result = dapper.ExecuteSqlWithRowCount(sql);
```

And:

```cs
IEnumerable<Computer> computers = dapper.LoadData<Computer>(sqlSelect);
```

In conclusion, it might seem useless because nothing changed significantly but if we are going to scale our project into big one - it will help us a lot. We will avoid a lot of code repetitions!

---
### . Zero-Links

1. 

-------
### Links

1. 