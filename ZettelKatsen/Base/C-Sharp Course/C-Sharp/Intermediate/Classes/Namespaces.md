Created: 202401110718
Tags: #cs-intermediate 

---
### Reference

**Namespaces** is a kind of mechanism that allows developers to split their code to different files and then easily manage them. This method is very useful during an OOP development. 

Let's see how it works!

I will use an example of the models. For example, you have a lot of classes in your project and you want to categorize them. You need to create the **Models** folder and then create a file for each model. 

*Models* -> Computer.cs | Person.cs | University.cs

I want to show only Computer.cs file:

```cs
namespace HelloWorld.Models
{
    public class Computer
		{
			public string Motherboard { get; set; } = "";
			public int CPUCores { get; set; }
			public bool HasWifi { get; set; }
			public bool HasLTE { get; set; }
			public DateTime ReleaseDate { get; set; }
			public decimal Price { get; set; }
			public string VideoCard { get; set; } = "";
		}
}
```
So, the main logic is that we must write a key word ==namespace== with the name of our project dot our folder. Then just implement the class and that's it! You can use it into another files. 

The main files will look like this:

```cs
using System;

//----------------------
using HelloWorld.Models; // here we connected our namespace
//----------------------

namespace HelloWorld

{
	internal class Program
	{
		static void Main(string[] args)
		{

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

            Console.WriteLine(myPC.Motherboard);
            Console.WriteLine(myPC.Price);
		}
	}
}
```

---
### Zero-Links

1. 

-------
### Links

1. [[Models]]