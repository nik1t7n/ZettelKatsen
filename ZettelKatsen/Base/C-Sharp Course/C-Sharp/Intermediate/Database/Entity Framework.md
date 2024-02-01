Created: 202401130822
Tags: #cs-intermediate 

---
### Reference

Entity Framework (EF) is a kind of "easier version" of the [[Dapper]]. Why? Because it make almost the same functionality but without direct use of SQL. You just need to type command and EF will do everything for you. 

>[!tip] It is more preferable to use Dapper
>Dapper gives us more control over SQL queries and gives more understanding of it. Hence, we can manipulate data more accurately and understand anything that happens in the code

Nevertheless, we should know the Entity Framework because a lot of people still use it. 

Firstly, we need to create its own file to make the class DataContextEF [[Dapper_Class#^0f7e19|as we did while was creating the Dapper Class]].

```cs
using HelloWorld.Models;
using Microsoft.EntityFrameworkCore;

namespace HelloWorld.Data
{
    public class DataContextEF : DbContext // inheritance
    {

    }
}
```
One interesting here - we **inherited** all features of EF class DbContext to our own class!

Next, let's create a DbSet [[Fields and Properties#^e9c7bc|property]]:

```cs
public DbSet<Computer>? Computer {get; set;}
```

>[!info] DbSet <\T>
>It creates a collection of objects that represents the table in a database. In simple words, it creates a copy of some table to our code so that we can manipulate it easily. *DbSet* provides a sort of abstraction under the database. We can *add, select, change and delete* some data in the database due to it. 

After that we need to **override** some methods from DbContext in our own class. First one is:

```cs
protected override void OnConfiguring(DbContextOptionsBuilder options)
{
	if (!options.IsConfigured) // check
	{
	options.UseSqlServer("Server=localhost;Database=DotNetCourseDatabase;TrustServerCertificate=true;Trusted_Connection=false;User Id=sa;Password=SQLConnect1;",
			options => options.EnableRetryOnFailure());
			
	}
}
```
As I understood, we do not use these methods directly in the Main file but it makes "background work". Exactly this method is responsible for configuring the database connection. It is automatically called by the EF Core framework when the DbContext is being configured.

It checks if it was already configured and if it was not - the program works. Also, if there was some trouble or interruption - the code will try to connect again. It works due to the "*options => options.EnableRetryOnFailure()*" command. 

Second one is:

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
	modelBuilder.HasDefaultSchema("TutorialAppSchema");

	modelBuilder.Entity<Computer>().HasKey(c => c.ComputerId);
	// .ToTable("Computer", "TutorialAppSchema");
}
```
This method is needed for the *default schema* configuration and the *primary key* identification. It provides more accurate and flexible data model display into the structure of the database. 

>[!info] Schema
>Schema in databases is used to group objects logically. It makes easier to organize data, isolate different applications and it provides more accurate structure of a database. 

>[!info] Primary key
>PK is the unique identifier for each entry in a table. It ensures its uniqueness and serves as a key for quick access and data binding in a database. 

So, the full code will look like this:

```cs
using HelloWorld.Models;
using Microsoft.EntityFrameworkCore;

namespace HelloWorld.Data
{
    public class DataContextEF : DbContext
    {

        public DbSet<Computer>? Computer {get; set;}

        protected override void OnConfiguring(DbContextOptionsBuilder options)
        {
            if (!options.IsConfigured)
            {
                options.UseSqlServer("Server=localhost;Database=DotNetCourseDatabase;TrustServerCertificate=true;Trusted_Connection=false;User Id=sa;Password=SQLConnect1;",
                    options => options.EnableRetryOnFailure());
            }
        }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.HasDefaultSchema("TutorialAppSchema");

            modelBuilder.Entity<Computer>().HasKey(c => c.ComputerId);
            // .ToTable("Computer", "TutorialAppSchema");
        }

    }
}
```

- - -
Next part is a work with the Main file. 

Firstly, let's create an instance of the class:

```cs
DataContextEF entityFramework = new();
```

Then we need to add our model (class) to the database. Notice, we do not use any of SQL queries!

```cs
Computer myPC = new()
{
	Motherboard = "ZX690",
	CPUCores = 16,
	HasWifi = true,
	HasLTE = false,
	ReleaseDate = DateTime.Now,
	Price = 947.83m,
	VideoCard = "RTX 2060"
};

// these lines do all the work
entityFramework.Add(myPC);
entityFramework.SaveChanges();
```

Therefore, to get and print our data we just need:

```cs
// get
IEnumerable<Computer>? computersEF = entityFramework.Computer?.ToList<Computer>();

// print
if (computersEF != null)
{
	foreach(Computer pc in computers)
	{
		Console.WriteLine("'" + pc.ComputerId
		+ "','" + pc.Motherboard
		+ "','" + pc.HasWifi
		+ "','" + pc.HasLTE
		+ "','" + pc.ReleaseDate.ToString("yyyy-MM-dd")
		+ "','" + pc.Price.ToString("0.00", CultureInfo.InvariantCulture)
		+ "','" + pc.VideoCard
		+ "'");
	}
}
```

Do you see how little code is here! It may seem convenient and it is. However, we pay for convenience with functionality :(. For example, we cannot change something specific directly in the SQL query. So, because of this - it is more preferable to use Dapper. 

---
### Zero-Links

1. 

-------
### Links

1. 