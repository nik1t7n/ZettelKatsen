Created: 202402031927
Tags: #api-basics 

---
### Reference

Here we are going to create our first custom controller. Most of the things will remain the same but I will show some new features.

I have created a new file called **UserController.cs** where I implemented the functionality. ^1b48fe

Let's see full code and then understand how it works:

```cs
using Microsoft.AspNetCore.Mvc;

namespace DotnetAPI.Controllers;

[ApiController]
[Route("[controller]")]
public class UserController : ControllerBase
{

    public UserController()
    {

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

Here we created trivial logic of the controller. It just takes *testValue* and returns it. 

The new part is **\[HttpGet("GetUsers/{testValue}")]**. Here we say to the program that after our *hostname/GetUsers* we can provide a value. It will look like this:

```
hostname/GetUsers?testValue="HelloWorld"
```

However, we also can try it in [[First_Controller#^bc3559|swagger]].

---
### Zero-Links

1. 

-------
### Links

1. 