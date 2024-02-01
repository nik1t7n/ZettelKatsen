Created: 202401101509
Tags: #cs-basics 

---
### Reference

In my opinion, because of C# is a fully OOP language it does not have any functions but methods. So, ==methods== are the same as functions but within a class. In C# it looks like this:

```cs
using System;
namespace HelloWorld

{
	internal class Program
	{
		static void Main(string[] args)
		{
			int[] arr = [1,2,3,4,5];
			Console.WriteLine(getSum(arr));
		}

		static private int getSum(int[] arr)
		{
			int sum = 0;
			foreach(int el in arr) sum += el;
			return sum;
		}
	}
}
```

It turns out that *methods* must be in a scope of *internal class Program*, but outside the Main method, but in general it works the same as functions. 

---
### Zero-Links

1. 

-------
### Links

1. [[Models]]