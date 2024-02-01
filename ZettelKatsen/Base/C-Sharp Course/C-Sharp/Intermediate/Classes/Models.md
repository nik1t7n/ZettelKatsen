Created: 202401101709
Tags: #cs-intermediate

---
### Reference

Oh, we started a new part of the course that a little bit harder than previous. Today's topic is the ==models==. 

>[!info]
>**Models** is a class or certain structure that contains some information inside. By using models it is easier to organize and structure an information. 

Okay, let's dive into it and look at how it works inside!

Firstly, I want to create a model called *Computer* that will have some information inside.

```cs
using System;
namespace HelloWorld

{
	internal class Program
	{

		public class Computer
		{
			public string Motherboard;
			public int CPUCores;
			// etc
		}

		static void Main(string[] args)
		{


		}
	}
}
```

Here the problems start. What have we done right now? We created **fields**. 

![[Fields and Properties#^847215]]

Let's see how it should looks like:

```cs
using System;
namespace HelloWorld

{
	internal class Program
	{

		public class Computer
		{
			public string Motherboard { get; set; }
			public int CPUCores { get; set; }
			public bool HasWifi { get; set; }
			public bool HasLTE { get; set; }
			public DateTime ReleaseDate { get; set; }
			public decimal Price { get; set; }
			public string VideoCard { get; set; }
			
		}

		static void Main(string[] args)
		{


		}
	}
}
```

^90c910

Next let's correct [[(NOT)Nullable string]] error. 

This is a little hint :)

>[!tip] Simple class assignment in Main
>--
>```cs
>// instead of writing
>Computer myPC = new Computer()
>{
>	// etc
>};
>
>// we can write
>Computer myPC = new()
>{
>	// etc
>}
>```

^3af64b


So, the full code will look like this:

```cs

using System;
namespace HelloWorld

{
	internal class Program
	{

		public class Computer
		{
			public string Motherboard { get; set; }
			public int CPUCores { get; set; }
			public bool HasWifi { get; set; }
			public bool HasLTE { get; set; }
			public DateTime ReleaseDate { get; set; }
			public decimal Price { get; set; }
			public string VideoCard { get; set; }
			

            public Computer()
            {
                Motherboard ??= " ";
                VideoCard ??= " ";
            }
		}

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

1. 