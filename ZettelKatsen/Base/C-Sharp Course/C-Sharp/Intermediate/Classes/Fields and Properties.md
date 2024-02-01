Created: 202401101739
Tags: #cs-intermediate 

---
### Reference

After creating a class we often make a mistake by creating fields. It might look like this:
```cs
public class Person
{
	public decimal age;
	public string name;
	public decimal weight;
}
```

So, what is a field?

>[!info]
>**Field** is just a variable inside a class that has its own level of access (public, private, protected, internal). 

^030bbe

What could possibly go wrong? However, according to the best practices of the C# - it is better to use **properties** instead of *fields*.  ^847215

>[!info]
>**Property** is a specific syntax to access the data. It uses the read method (getter) and write method (setter) to access some data. Likewise, it has some protection levels and additional logic in the getter/setter can be realized. 

^e9c7bc

Why we must use *properties* instead of *fields*? There are one main reason:

> [!tip] 
> **Flexibility**. Fields just store the data. If we want to change method of data access of validation we must rewrite the code everywhere. On the contrary, fields creates a higher level of abstraction allowing us to add logic to setter (checking the correctness of a data) or compute values on fast (getter). 

So, the class with properties will in that way:

```cs
public class Person
{
	public decimal age {get; set;}
	public string name {get; set;}
	public decimal weight {get; set;}
}
```

---
### Zero-Links

1. 

-------
### Links

1. 