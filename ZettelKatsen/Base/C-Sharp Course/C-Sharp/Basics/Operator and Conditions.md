Created: 202401100801
Tags: #cs-basics 

---
### Reference

==Operators==

> [!tip] Interesting fact
> By its priority in C# a division come before multiplication even if multiplication stands before!

We can concatenate strings by using ==+== operator:

```cs
string a = "hel";
string b = "lo";

Console.WriteLine(a+b); // "hello"
```

If we have a string as a sentence, for example: "Hello my friend" and we want to get the array that looks like {"Hello", "my", "friend"}. The ==split== can be used:

```cs
string greet = "Hello my friend";
string[] greetArr = greet.Split(" "); // in the parentheses the denomnator is written
```

To print the *greetArr* we **cannot** use only Console.WriteLine! We must use loops. 

![[Loops#^d08d4e]]

```cs
foreach(string el in greetArr)
{
	Console.WriteLine(el);
}
```

==Conditionals==

We can compare variables by using *Equals* method:

```cs
int a = 5;
int b = 10;

Console.WriteLine(a.Equals(b)); // false
Console.WriteLine(a.Equals(b/2)); // true
```

---
### Zero-Links

1. 

-------
### Links

1. [[Data Types]]
2. [[Data Structures]]