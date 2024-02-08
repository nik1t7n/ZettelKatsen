Created: 202402062124
Tags: #api-basics 

---
### Reference

After we created new [[Put_&_Post|PUT and POST]] queries last time there was some inconvenient issue. At the moment where we made [[Put_&_Post#^27930e|AddUser]] we passes User class instance as the argument. However, we don't need a *UserId* property from the class/

To solve this problem we can use DTO (Data Transfer Object) to change our User model a little bit.

>[!tip] DTO (Data Transfer Object)
>This is a design pattern used to transfer data between application subsystems. In other words we can make our program more flexible by changing its functionality.

In this case we need to eliminate the *UserId* property. Let's figure it out.

Firsly we must create a new folder with a new file **Dtos -> UserToAddDto.cs**. Then inside of the file we just copy all the User model and delete specific field:

```cs
namespace DotnetAPI
{
    public partial class UserToAddDto 
    {
        public string FirstName {get; set;} = "";
        public string LastName {get; set;} = "";
        public string Email {get; set;} = "";
        public string Gender {get; set;} = "";
        public bool Active {get; set;}
    }
}
```

Then just pass this model as the argument to our **AddUser** method:

```cs
// ...
public IActionResult AddUser(UserToAddDto user)
// ...
```

Congratulations! It's all done! Now there won't be *UserId* property in the insert field.

---
### Zero-Links

1. 

-------
### Links

1. 