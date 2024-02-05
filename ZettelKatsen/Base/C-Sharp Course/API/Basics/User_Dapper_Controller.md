Created: 202402050845
Tags: #api-basics 

---
### Reference

Here everything is so trivial so I think there is no need in detailed explanation.

The main idea of what we will do is that we want to connect database to our controller through *Dapper*. Firstly, we need to [[API_Database_Connection|configure the dapper and write it to the controller]].

Then just make two methods:

```cs
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
```

The first method provides us JSON file with all users from a database, while second returns only one user by his ID.

---
### Zero-Links

1. 

-------
### Links

1. 