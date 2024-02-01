Created: 202401171926
Tags: #cs-intermediate 

---
### Reference

Here we are going to talk about how to **serialize / deserialize** JSON files in *two different ways*. Likewise I will show you how to deserialize some data from JSON straight to out database!

To begin with we have a file called Computers.json with the a lot of [[Models#^90c910|Computer]] class instances. It looks nearly like this:

```json
[{"ComputerId":1,"motherboard":"Edgepulse","hasWifi":false,"hasLTE":true,"releaseDate":"2013-04-20","videoCard":"Morar Inc"},

{"ComputerId":2,"motherboard":"Teklist","hasWifi":false,"hasLTE":true,"releaseDate":"2019-04-08","videoCard":"Waters-Hudson"},

// ...
 
{"ComputerId":99,"motherboard":"Brainbox","hasWifi":false,"hasLTE":true,"releaseDate":"2013-06-21","videoCard":"O'Kon, Hagenes and Bashirian"},

{"ComputerId":100,"motherboard":"Gabtune","hasWifi":false,"hasLTE":false,"releaseDate":null,"videoCard":"Thompson Inc"}]
```

Firstly, we need to [[File Reading and Writing#^257f33|read]] all this information from the JSON to our code:

```cs
string computersJson = File.ReadAllText("Computers.json");
```

==System.TextJson==    ->    ==Deserialization==

From here, we will use the first method of manipulating JSON named **System.TextJson**:

```json
// all this is a one string ^_^

// don't forget to put the "?" here to avoid not-nullable object
IEnumerable<Computer>? computersSystem = System.Text.Json.JsonSerializer.Deserialize<IEnumerable<Computer>>(computersJson, options); // here
```
Here we create an IEnumerable of our Computer class objects that were deserialized using this method. But you might have a question, **what is a options**? 

>[!tip] Case difference
>As the best practices of Javascript it is better to use **camelCase** (with first small letter) while in C# it is better to use  **PascalCase** (with all words are capitalized). Hence the conflict arises and we can easily *catch an error*! So, there is a solution:

Before declaring the *computerSystem* variable we can set the setting. 
```cs
JsonSerializerOptions options = new()
{
	PropertyNamingPolicy = JsonNamingPolicy.CamelCase
};
```

>[!info] Remember
>Using the **System.TextJson** method we must pass the settings (options) during both: serialization and deserialization!

==System.TextJson==    ->    ==Serialization==

The serialization process looks quite similar:

```cs
string computersCopySystem = System.Text.Json.JsonSerializer.Serialize(computersNewtonsoft, options); // options are still here

File.WriteAllText("fileName.json", computersCopySystem);
```
Here we wrote all data to the variable and then added it to a file. 

Congratulations, you have successfully deserialized and serialized data from JSON using first method. Now let's consider the second one!

==Newtonsoft==    ->    ==Deserialization==

Before use this method we must install a package:

```shell
dotnet add package Newtonsoft.Json
```

Logic looks quite similar too:

```cs
IEnumerable<Computer>? computersNewtonsoft = JsonConvert.DeserializeObject<IEnumerable<Computer>>(computersJson);
```
You might ask: *"where are the options?"*. Here the difference between **System.TextJson** and **Newtonsoft**.

>[!tip] Difference between **System.TextJson** and **Newtonsoft**
>While in the *TextJson* we need to set setting during both processes, in the *Newtonsoft* we must set settings **only during serialization**. At deserialization this package does it automatically!

==Newtonsoft==    ->    ==Serialization==

```cs
JsonSerializerSettings settings = new()
{
	ContractResolver = new CamelCasePropertyNamesContractResolver()
};

string computersCopyNewtonsoft = JsonConvert.SerializeObject(computersNewtonsoft, settings);

File.WriteAllText("fileName.json", computersCopyNewtonsoft);
```
Here we have the serialization process using the settings set above. 

- - -
==Adding to the Database==

Here we go! After we have all the data here we can easily add it to the database using [[Dapper]].
We declare our [[Config#^d1691d|config file]] and dapper too. 

```cs
foreach(Computer computer in computersNewtonsoft)
{
	  string sql = @"INSERT INTO TutorialAppSchema.Computer(
				Motherboard,
				HasWifi,
				HasLTE,
				ReleaseDate,
				Price,
				VideoCard
			) VALUES ( '" + EscapeSingleQuote(computer.Motherboard)
				+ "','" + computer.HasWifi
				+ "','" + computer.HasLTE
				+ "','" + computer.ReleaseDate?.ToString("yyyy-MM-dd")
				+ "','" + computer.Price.ToString("0.00", CultureInfo.InvariantCulture)
				+ "','" + EscapeSingleQuote(computer.VideoCard)
			+ "' )";

	  dapper.ExecuteSql(sql); // dapper usage
}
```
Here we added all of Computer objects to our database. 

However, I had an issue about single quote. It was kind of conflict between SQL language and motherboard name, so i wrote a method to fix it:

```cs
static string EscapeSingleQuote(string input)
{
	  string output = input.Replace("'", "''");
	  return output;
}
```

---
### Zero-Links

1. 

-------
### Links

1. 