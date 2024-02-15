Created: 202402152111
Tags: #api-intermediate 

---
### Reference

Here we are going to add one more layer of abstraction between data collection and the program itself by using **Interfaces**. As I understood, this is something, that hides the logic and realization, leaving only methods declarations.

We need to create new **IUserRepository.cs** file in the *Data* folder. Code looks like this:

```cs
namespace DotnetAPI.Data 
{
    public interface IUserRepository 
    {
        public bool SaveChanges();
        public void AddEntity<T>(T entityToAdd);
        public void RemoveEntity<T>(T entityToRemove);
    }
}
```

We just declare all methods here and it serves as a certain *instruction* to the [[Repository_Pattern|UserRepository]] file that tells what methods should be realized.

Then we inherit interface to the UserRepository class:

```cs
public class UserRepository : IUserRepository
```

Connect our new interface to the original class in **MAIN** file:

```cs
builder.Services.AddScoped<IUserRepository, UserRepository>(); // here
var app = builder.Build();
```

And change methods' names inside of the controller, such as:

```cs
// new constructor
DataContextEF _entityFramework;    
    IUserRepository _userRepository;
    IMapper _mapper;

    public UserEFController(IConfiguration config, IUserRepository userRepository)
    {
        _entityFramework = new DataContextEF(config);
        _userRepository = userRepository;

        _mapper = new Mapper(new MapperConfiguration(cfg =>{
            cfg.CreateMap<UserToAddDto, User>();
            cfg.CreateMap<UserSalary, UserSalary>().ReverseMap();
            cfg.CreateMap<UserJobInfo, UserJobInfo>().ReverseMap();
        }));

    }
```

```cs
// add
_userRepository.AddEntity<User>(userDb);
```

```cs
// Remove
_userRepository.RemoveEntity<User>(userDb);
```

```cs
// SaveChanges
_userRepository.SaveChanges()
```

---
### Zero-Links

1. 

-------
### Links

1. 