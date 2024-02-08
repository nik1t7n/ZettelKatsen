Created: 202402041051
Tags: #api-basics 

---
### Reference

Here we are going to connect our API functionality to the database using [[Dapper_Class|Dapper]].

Firstly, lets open **appsettings.json** and add there our *connection string*:

```json
{
    "ConnectionStrings": {
        "DefaultConnection": "Server=localhost; Database=DotNetCourseDatabase; Trusted_Connection=true; TrustServerCertificate=true"
    },
    "Logging": {
        "LogLevel": {
            "Default": "Information",
            "Microsoft.AspNetCore": "Warning"
        }
    },
    "AllowedHosts": "*"
}
```

If we use MacOS we need to use [[Database Connection#^7c61d0|this connection string]] and follow [[Database Connection|this instructions]]. 

Next we must implement the [[Dapper_Class|Dapper class]] to use it further.

After all these steps let's implement our Controller functionality in the [[Users_Controller#^1b48fe| UserController.cs]] file. The full code will look like this:

```cs
using Microsoft.AspNetCore.Mvc;

namespace DotnetAPI.Controllers;

[ApiController]
[Route("[controller]")]
public class UserController : ControllerBase
{
	// dapper connection
    DataContextDapper _dapper;
    public UserController(IConfiguration config)
    {
        Console.WriteLine(config.GetConnectionString("DefaultConnection"));
        _dapper = new DataContextDapper(config);
    }

    [HttpGet("TestConnection")]
    public DateTime TestConnection()
    {
        return _dapper.LoadDataSingle<DateTime>("SELECT GETDATE()");
    }

    [HttpGet("GetUsers/{testValue}")]

    // public IActionResult Test()
    public string[] GetUsers(string testValue)
    {
        string[] responseArray = new string[] {
            "test1",
            "test2",
            testValue
        };

        return responseArray;
    }
}
```

Here we declared *dapper* class and wrote class constructor. In the class constructor we passed our [[Config|configuration file.]] Then just tested if it works by using *Console.WriteLine();* and initialized dapper.

After we created new API path by using **\[HttpGet("TestConnection")]**. If user types *\http://localhost:5000/TestConnection/* it will use one of the *Dapper* methods and return local date.

So, it means that we finally realized connection between our database and API!

---
### Zero-Links

1. 

-------
### Links

1. 