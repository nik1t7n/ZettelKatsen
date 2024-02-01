Created: 202401152335
Tags: #cs-intermediate 

---
### Reference

The config file purpose is to store little pieces of data inside. So, we can take it from the file and inject into our application. 

In my case, I will store my *[[Database Connection#^16a212|connection string]]* in the config file. Let's create a file names **appsettings.json**. 

Inside the file we will create a Dictionary of Connection Strings:

```json
{
"ConnectionStrings": 
	{
	"DefaultConnection": "Server=localhost;Database=DotNetCourseDatabase;TrustServerCertificate=true;Trusted_Connection=false;User Id=sa;Password=SQLConnect1;"
	}
}
```

Next step is that we already can rewrite our [[Dapper_Class|Dapper Class]] and [[Entity Framework|Entity Class]] using configurational file. But before we must add two packages to our project:

```shell
dotnet add package Microsoft.Extensions.Configuration
```

```shell
dotnet add package Microsoft.Extensions.Configuration.Json
```
It will allow us to use ConfigurationBuilder() further. The full code of Dapper class:

```cs
using System.Data;
using Dapper;
using Microsoft.Data.SqlClient;
using Microsoft.Extensions.Configuration;

namespace HelloWorld.Data
{
    public class DataContextDapper
    {

        // private IConfiguration _config;
        private string? _connection;

        public DataContextDapper(IConfiguration config)
        {
            // _config = config; // possible instance of the config
            _connection = config.GetConnectionString("DefaultConnection"); // we get the string from config file
        }


        public IEnumerable<T> LoadData<T>(string sql)
        {
            IDbConnection dbConnection = new SqlConnection(_connection);
            return dbConnection.Query<T>(sql);
        }
        // etc
    }
}
```

So, there are two ways of doing this here. First one is to create a \_config instance and use it further or just get the *connectionString* once from config file and use it as a variable. 

To get the **Connection string** we are using:

```cs
config.GetConnectionString("DefaultConnection"); // "DefaultConnection" is the key of our string
```

And the same we do to the Entity Framework class:

```cs
using HelloWorld.Models;
using Microsoft.EntityFrameworkCore;
using Microsoft.Extensions.Configuration;

namespace HelloWorld.Data
{
	// here we pass a config to the class
    public class DataContextEF(IConfiguration config) : DbContext
    {

		// declare IConfiguration private field to use
        private IConfiguration _config = config;

        public DbSet<Computer>? Computer {get; set;}

        protected override void OnConfiguring(DbContextOptionsBuilder options)
        {
            if (!options.IsConfigured)
            { // get the Connection string
                options.UseSqlServer(_config.GetConnectionString("DefaultConnection"),
                    options => options.EnableRetryOnFailure());
            }
        }
		// etc
    }
}
```

- - -
Further, let's see how the Main file works. We create the **config** variable:

```cs
IConfiguration config = new ConfigurationBuilder()
	.AddJsonFile("appsettings.json")
	.Build();
```

^d1691d

And pass this variable to our classes:

```cs
DataContextDapper dapper = new(config);
DataContextEF entityFramework = new(config);
```

However, we might will face this error:

>[!error]
>Unhandled exception. System.IO.FileNotFoundException: The configuration file 'appsettings.json' was not found and is not optional. The expected physical path was '/Users/nik1t7n/Desktop/csharp_course/HelloWorld/bin/Debug/net8.0/appsettings.json'.
   at Microsoft.Extensions.Configuration.FileConfigurationProvider.HandleException(ExceptionDispatchInfo info)
   at Microsoft.Extensions.Configuration.FileConfigurationProvider.Load(Boolean reload)
   at Microsoft.Extensions.Configuration.FileConfigurationProvider.Load()
   at Microsoft.Extensions.Configuration.ConfigurationRoot..ctor(IList`1 providers)
   at Microsoft.Extensions.Configuration.ConfigurationBuilder.Build()
   at HelloWorld.Program.Main(String[] args) in /Users/nik1t7n/Desktop/csharp_course/HelloWorld/Program.cs:line 19

It means that the program cannot find out *appsettings.json* file. To fix it we must change a little bit out **.csproj** file by adding there:

```cs
<None Update="appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
</None>
```
It will add the file's path to program. 

In conclusion, why do we do it? I mean, what a specific reasons to use configurational files? And yes, there are exactly some reasons to do that:

>[!tip] Why do we need to use Config files?
>1. Code separation and configuration
>2. Settings change without recompilation
>3. It is easy to scale
>4. We can hide confidential information there

---
### Zero-Links

1. 

-------
### Links

1. 