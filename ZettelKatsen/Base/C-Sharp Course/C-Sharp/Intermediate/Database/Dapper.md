Created: 202401121000
Tags: #cs-intermediate 

---
### Reference

Let's create an SQL query to add data to the database using Dapper:

```cs
string sql = @"INSERT INTO TutorialAppSchema.Computer(
                Motherboard,
                HasWifi,
                HasLTE,
                ReleaseDate,
                Price,
                VideoCard
            ) VALUES ( '" + myPC.Motherboard
                + "','" + myPC.HasWifi
                + "','" + myPC.HasLTE
                + "','" + myPC.ReleaseDate
                + "','" + myPC.Price.ToString("0.00", CultureInfo.InvariantCulture)
                + "','" + myPC.VideoCard
            + "' )";
```
The "@" at the beginning allows us to write a string at multiple lines. 
The construction inside the "VALUES" is just a concatenation of string to make a output looks good. In the string:

```cs
myPC.Price.ToString("0.00", CultureInfo.InvariantCulture)
```
We avoid the error below. It might happen due to different decimal points. In some countries people use a comma (,) while some use a period (.). So, this line formates conversion that uses InvariantCulture as the provider, and "0.00" to standardise it. 

>[!error] Error converting data type varchar to numeric
>

In the next lines we execute the query:

```cs
int result = dbConnection.Execute(sql);
Console.WriteLine(result);
```
Or just:
```cs
dbConnection.Execute(sql);
```
The *dbConnection.Execute(sql);* besides making an execution also returns a value of *how many rows were affected*. So, we may or may not save it.   ^ddb079

NEXT, we will *select* and get data from the database:

```cs
            string sqlSelect = @"
            SELECT 
                Computer.Motherboard,
                Computer.HasWifi,
                Computer.HasLTE,
                Computer.ReleaseDate,
                Computer.Price,
                Computer.VideoCard
            FROM TutorialAppSchema.Computer";

            IEnumerable<Computer> computers = dbConnection.Query<Computer>(sqlSelect);

            foreach(Computer pc in computers)
            {
                Console.WriteLine("'" + myPC.Motherboard
                + "','" + myPC.HasWifi
                + "','" + myPC.HasLTE
                + "','" + myPC.ReleaseDate
                + "','" + myPC.Price.ToString("0.00", CultureInfo.InvariantCulture)
                + "','" + myPC.VideoCard
                + "'");
            }
```
Here, we make the *query-string* with all parameters again. One important rule:

>[!tip] Best practices
>It is better to write a class name before the variables inside the *query-string*, because if we have big and complex query it will be difficult to differentiate variables. However, without class clarification it will also work. 

Next we make an **[[Data Structures#^1e055c|IEnumerable]]** variable that will store collected data. Remember, we can use only IEnumerable, because *IDbConnection* returns this type! Further, we can convert it to List using *.ToList()* but at the beginning it always like this. 

Then we just iterate through the variable and print our data :). 

By the way, I have randomly found a tip from ChatGPT about how we should add data to a database. Here it is:

>[!tip] Using "@" instead of string concatenation
> Using "@" placeholders in parametrized queries is preferred over string concatenation as it helps to prevent SQL injections, ensures type safety, improves readability and maintainability.  

So, the code will look like this:
```cs
            // Use parameterized query to safely insert data into the database.
            string sql = @"INSERT INTO TutorialAppSchema.Computer(
                Motherboard,
                HasWifi,
                HasLTE,
                ReleaseDate,
                Price,
                VideoCard
            ) VALUES (
                @Motherboard,
                @HasWifi,
                @HasLTE,
                @ReleaseDate,
                @Price,
                @VideoCard
            )"; // there is no string concatenation
```



---
### Zero-Links

1. 

-------
### Links

1. 