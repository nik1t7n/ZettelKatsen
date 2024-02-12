Created: 202402120923
Tags: #api-intermediate

---
### Reference

Today will be probably quite important topic about code abstraction. We are going to divide *Data Access* layer from the *Application* itself by using **Repository** pattern.

>[!tip] Repository pattern is...
>Repository Design Pattern acts as a middleman or middle layer between the rest of the application and the data access logic. That means a repository pattern isolates all the data access codes from the rest of the application. 
>
>1. The advantage of doing so is that if you need to make any changes, you must do it in one place. 
>2. Another benefit is that testing your controllers becomes easy because the testing framework must not run against the database access code. 

This is how we accessed the database before:

![[Pasted image 20240212094639.png]]

And this how it will be after **Repository patter** implementation:

![[Pasted image 20240212094720.png]]

In other words, we need a class defined for an entity with all the possible database operations (CRUD) and any possible Controller entity operations.

---

Let's implement it! Firstly we create **Data -> UserRepository.cs**.

Then code:

```cs
namespace DotnetAPI.Data 
{
    public class UserRepository 
    {
        DataContextEF _entityFramework;

        public UserRepository(IConfiguration config)
        {
            _entityFramework = new DataContextEF(config);
        }

        public bool SaveChanges()
        {
            return _entityFramework.SaveChanges() > 0;
        }

        public void AddEntity<T> (T entityToAdd)
        {
            if (entityToAdd != null)
            {
                _entityFramework.Add(entityToAdd);    
            }
        }

        public void RemoveEntity<T> (T entityToRemove)
        {
            if (entityToRemove != null)
            {
                _entityFramework.Remove(entityToRemove);    
            }
        }
    }
}
```

Here we just initialized our new class with *Config* parameter and realized some methods such as **AddEntity, RemoveEntity and SaveChanges**. Notice that first two ones use generic type to be more flexible.

---
### Zero-Links

1. 

-------
### Links

1. 