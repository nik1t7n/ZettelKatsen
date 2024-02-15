Created: 202402152222
Tags: #api-intermediate 

---
### Reference

After we discussed [[App_Interface_Arrangement#^b1548e|how our program arranged]] - let's explore the code. First is going to be **IUserRepository**:

```cs
using DotnetAPI.Models;

namespace DotnetAPI.Data 
{
    public interface IUserRepository 
    {
        public bool SaveChanges();
        public void AddEntity<T>(T entityToAdd);
        public void RemoveEntity<T>(T entityToRemove);
        public IEnumerable<User> GetUsers();
        public User GetSingleUser(int userId); // 1
        public UserSalary GetSingleUserSalary(int userId); // 2
        public UserJobInfo GetSingleUserJobInfo(int userId); // 3
    }
}
```
Here we just declared another 3 methods.

Next we fully eliminate usage of Entity Framework in the **UserRepository** file replacing it with our new methods. Full huge code:

```cs
using AutoMapper;
using DotnetAPI.Data;
using DotnetAPI.Dtos;
using DotnetAPI.Models;
using Microsoft.AspNetCore.Mvc;

namespace DotnetAPI.Controllers;

[ApiController]
[Route("[controller]")]
public class UserEFController : ControllerBase
{  
    IUserRepository _userRepository;
    // no Entity Framework
    IMapper _mapper;

    public UserEFController(IConfiguration config, IUserRepository userRepository)
    {
        _userRepository = userRepository;

        _mapper = new Mapper(new MapperConfiguration(cfg =>{
            cfg.CreateMap<UserToAddDto, User>();
            cfg.CreateMap<UserSalary, UserSalary>().ReverseMap();
            cfg.CreateMap<UserJobInfo, UserJobInfo>().ReverseMap();
        }));

    }

    [HttpGet("GetUsers")]
    public IEnumerable<User> GetUsers()
    {
	    // here
        return _userRepository.GetUsers();
    }

    [HttpGet("GetSingleUser/{userId}")]
    public User GetSingleUser(int userId)
    {
	    // here
       return _userRepository.GetSingleUser(userId);
    }
    
    [HttpPut("EditUser")]
    public IActionResult EditUser(User user)
    {
	    // here
        User? userDb = _userRepository.GetSingleUser(user.UserId);
            
        if (userDb != null)
        {
            userDb.Active = user.Active;
            userDb.FirstName = user.FirstName;
            userDb.LastName = user.LastName;
            userDb.Email = user.Email;
            userDb.Gender = user.Gender;
            if (_userRepository.SaveChanges())
            {
                return Ok();
            } 

            throw new Exception("Failed to Update User");
        }
        
        throw new Exception("Failed to Get User");
    }


    [HttpPost("AddUser")]
    public IActionResult AddUser(UserToAddDto user)
    {
        User userDb = _mapper.Map<User>(user);

		// here
        _userRepository.AddEntity<User>(userDb);
        if (_userRepository.SaveChanges())
        {
            return Ok();
        } 

        throw new Exception("Failed to Add User");
    }

    [HttpDelete("DeleteUser/{userId}")]
    public IActionResult DeleteUser(int userId)
    {
	    // here
        User? userDb = _userRepository.GetSingleUser(userId);
            
        if (userDb != null)
        {
	        // here
            _userRepository.RemoveEntity<User>(userDb);
            if (_userRepository.SaveChanges())
            {
                return Ok();
            } 

            throw new Exception("Failed to Delete User");
        }
        
        throw new Exception("Failed to Get User");
    }

    [HttpGet("UserSalary/{userId}")]
    public UserSalary GetUserSalaryEF(int userId)
    {
	    // here
        return _userRepository.GetSingleUserSalary(userId);
    }

    [HttpPost("UserSalary")]
    public IActionResult PostUserSalaryEf(UserSalary userForInsert)
    {
	    // here
        _userRepository.AddEntity<UserSalary>(userForInsert);
        // here
        if (_userRepository.SaveChanges())
        {
            return Ok();
        }
        throw new Exception("Adding UserSalary failed on save");
    }


    [HttpPut("UserSalary")]
    public IActionResult PutUserSalaryEf(UserSalary userForUpdate)
    {
	    // here
        UserSalary? userToUpdate = _userRepository
            .GetSingleUserSalary(userForUpdate.UserId);

        if (userToUpdate != null)
        {
            _mapper.Map(userForUpdate, userToUpdate);
	        // here
            if (_userRepository.SaveChanges())
            {
                return Ok();
            }
            throw new Exception("Updating UserSalary failed on save");
        }
        throw new Exception("Failed to find UserSalary to Update");
    }


    [HttpDelete("UserSalary/{userId}")]
    public IActionResult DeleteUserSalaryEf(int userId)
    {
	    // here
        UserSalary? userToDelete = _userRepository.GetSingleUserSalary(userId);

        if (userToDelete != null)
        {
	        // here
            _userRepository.RemoveEntity<UserSalary>(userToDelete);
            // here
            if (_userRepository.SaveChanges())
            {
                return Ok();
            }
            throw new Exception("Deleting UserSalary failed on save");
        }
        throw new Exception("Failed to find UserSalary to delete");
    }


    [HttpGet("UserJobInfo/{userId}")]
    public UserJobInfo GetUserJobInfoEF(int userId)
    {
	    // here
        return _userRepository.GetSingleUserJobInfo(userId);
    }

    [HttpPost("UserJobInfo")]
    public IActionResult PostUserJobInfoEf(UserJobInfo userForInsert)
    {
	    // here
        _userRepository.AddEntity<UserJobInfo>(userForInsert);
        // here
        if (_userRepository.SaveChanges())
        {
            return Ok();
        }
        throw new Exception("Adding UserJobInfo failed on save");
    }


    [HttpPut("UserJobInfo")]
    public IActionResult PutUserJobInfoEf(UserJobInfo userForUpdate)
    {
	    // here
        UserJobInfo? userToUpdate = _userRepository
            .GetSingleUserJobInfo(userForUpdate.UserId);

        if (userToUpdate != null)
        {
            _mapper.Map(userForUpdate, userToUpdate);
            // here
            if (_userRepository.SaveChanges())
            {
                return Ok();
            }
            throw new Exception("Updating UserJobInfo failed on save");
        }
        throw new Exception("Failed to find UserJobInfo to Update");
    }


    [HttpDelete("UserJobInfo/{userId}")]
    public IActionResult DeleteUserJobInfoEf(int userId)
    {
	    // here
        UserJobInfo? userToDelete = _userRepository
            .GetSingleUserJobInfo(userId);

        if (userToDelete != null)
        {
	        // here
            _userRepository.RemoveEntity<UserJobInfo>(userToDelete);
            // here
            if (_userRepository.SaveChanges())
            {
                return Ok();
            }
            throw new Exception("Deleting UserJobInfo failed on save");
        }
        throw new Exception("Failed to find UserJobInfo to delete");
    }
}
```

In that places where I mentioned `// here` comment - there we replaced Entity Framework with IUserRepository.

Logic if this methods fully copied and just transferred to new file in terms of Abstraction.

---
### Zero-Links

1. 

-------
### Links

1. 