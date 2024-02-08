Created: 202402070914
Tags: #api-basics 

---
### Reference

In this lecture I am going to show you how to setup **DataContextEF.cs** model in terms of our database.

As always I will provide full code and then we will describe it:

```cs
using DotnetAPI.Models;
using Microsoft.EntityFrameworkCore;

namespace DotnetAPI.Data 
{
    public class DataContextEF : DbContext 
    {
        private readonly IConfiguration? _config;
        private readonly string? _connectionString;

        public DataContextEF(IConfiguration config)
        {
            _config = config;
            _connectionString = _config.GetConnectionString("DefaultConnection");
        }

        public virtual DbSet<User> Users {get; set;}
        public virtual DbSet<UserSalary> UserSalary {get; set;}
        public virtual DbSet<UserJobInfo> UserJobInfo {get; set;}


        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            if (!optionsBuilder.IsConfigured)
            {
                optionsBuilder 
                    .UseSqlServer(_connectionString, 
                        optionsBuilder => optionsBuilder.EnableRetryOnFailure());
            }
        }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.HasDefaultSchema("TutorialAppSchema");

            modelBuilder.Entity<User>()
                .ToTable("Users", "TutorialAppSchema")
                .HasKey(user => user.UserId);

            modelBuilder.Entity<UserSalary>()
                .HasKey(user => user.UserId);   
                
            modelBuilder.Entity<UserJobInfo>()
                .HasKey(user => user.UserId); 
        }
    }
}
```

We inherit **DbContext** class to our class which allows us to use full functionality of Entity Framework.

Then we configure it and create three **virtual** ==DbSet properties==.

>[!tip] DbSet is...
>DbSet property is used to represent some database table into collection in the code.

Also we make them *virtual*. It is made for possible overwrites in the inherited classes.

Next step is providing our *Connection String* to EF by using ==OnConfiguring== method. We make it **protected override**.

>[!tip] Protected is...
>Access modifier *protected* provides access to the method only inside of our current class or in the derived (inherited) classes.

And while using *override* we are just *rewriting/redefining* already existing method for our personal purposes. 

Inside the *OnConfiguring* method we checks if it was already configured and if not we continue by providing connection string and enabling method that will try to reconnect to the database in case of some possible failures.


After this we overwriting second method called ==OnModelCreating==. Here we manually point that we have *not default* schema (default is dbo) but another one. 

Then we know that our model called **User** while table in the database called **Users**. To avoid such confusions we will manually set up table name and also add *Primary Key* to each table.

Congrats, we have configured out Entity Framework model ^\_^

---
### Zero-Links

1. 

-------
### Links

1. 