Created: 202401101523
Tags: #cs-basics 

---
### Reference

Okay, I think that topic of scope is quite easy so I will write here only some specific stuff. 

If we initialize for example *int* variable outside the **Main** method we will not be able to reach it from the Main. However, the variable was declared before the Main, so why we cannot? Because the Main method is static (*in terms of console application*) and static methods can access only static elements. Thus, we must add *static* to the int and everything will be ok :)

>[!failure]

```cs
using System;
namespace HelloWorld

{
	internal class Program
	{
		int accesibleInt = 9;
		
		static void Main(string[] args)
		{
			Console.WriteLine(accesibleInt);
		}
	}
}
```


>[!success]

```cs
using System;
namespace HelloWorld

{
	internal class Program
	{
		static int accesibleInt = 9;
		
		static void Main(string[] args)
		{
			Console.WriteLine(accesibleInt);
		}
	}
}
```


Likewise, try to eliminate similar variable names to avoid confusion further. As a rule you can name variables outside the Main **Capitalized** and from **lowercase** inside the Main. 

---
### Zero-Links

1. 

-------
### Links

1. 