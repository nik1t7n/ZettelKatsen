Created: 202402061139
Tags: #api-basics 

---
### Reference

Before we did only [[Users_Controller#^d9908f|GET]] http requests so it is perfect time to consider two more requests called **PUT** and **POST**. We are going to implement two more methods in our *UserController.cs* file that do such requests.

Let's begin from the full code and then I will explain it:

```cs
using Microsoft.AspNetCore.Mvc;

namespace DotnetAPI.Controllers;

[ApiController]
[Route("[controller]")]
public class UserController : ControllerBase
{

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

    [HttpGet("GetUsers")]
    public IEnumerable<User> GetUsers()
    {
        string sql = @"
        SELECT [UserId],
            [FirstName],
            [LastName],
            [Email],
            [Gender],
            [Active] 
        FROM TutorialAppSchema.Users;";

        IEnumerable<User> users = _dapper.LoadData<User>(sql);
        return users;
    }

    [HttpGet("GetSingleUser/{userId}")]
    public User GetSingleUser(string userId)
    {
        string sql = $@"
        SELECT [UserId],
            [FirstName],
            [LastName],
            [Email],
            [Gender],
            [Active] 
        FROM TutorialAppSchema.Users
        WHERE UserId = {userId};";
        return _dapper.LoadDataSingle<User>(sql);
    }

    [HttpPut("EditUser")]
    public IActionResult EditUser(User user)
    {
        string sql = $@"
            UPDATE TutorialAppSchema.Users 
            SET 
                [FirstName] = '{user.FirstName}',
                [LastName] = '{user.LastName}',
                [Email] = '{user.Email}',
                [Gender] = '{user.Gender}',
                [Active] = {(user.Active ? 1 : 0)} 
            WHERE UserId = {user.UserId}";

        Console.WriteLine(sql);

        if (_dapper.ExecuteSql(sql))
        {
            return Ok();
        } 

        throw new Exception("Failed to update User");
        
    }

    [HttpPost("AddUser")]
    public IActionResult AddUser(User user)
    {
        string sql = $@"
        INSERT INTO TutorialAppSchema.Users 
        (
            [FirstName],
            [LastName],
            [Email],
            [Gender],
            [Active] 
        )
        VALUES 
        (
            '{user.FirstName}',
            '{user.LastName}',
            '{user.Email}',
            '{user.Gender}',
            {(user.Active ? 1 : 0)} 
        )";

        if (_dapper.ExecuteSql(sql))
        {
            return Ok();
        }


        throw new Exception("Failed to add User!");
    }
}
```

Here we have created two new attributes **\[HttpPut("EditUser")]** and **\[HttpPost("AddUser")]**. Former will make put requests with updating database while latter will add absolutely new user by doing post request.

There is no something very special here. Maybe **IActionResult**. It returns response from the server (how out command worked). Successful or not.

```cs
if (_dapper.ExecuteSql(sql))
{
	return Ok();
}

throw new Exception("Failed to add User!");
```

Likewise, we check if our program worked well and then return either OK (200) or Exception.

---
### Zero-Links

1. 

-------
### Links

1. 