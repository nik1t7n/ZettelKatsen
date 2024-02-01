Created: 202401101750
Tags: #cs-intermediate 

---
### Reference

In the moment when we create a field/property inside a class and make it *string*. We can possibly face an disclaimer from a compilator because of "non-nullable string". It means that if user does not fill this field/property, the error will appear. 

We have two ways how to avoid this problem. First one is just add "?" after *string*:

```cs
public class Person
{
	public string? Name {get; set;} // "?" automaticly makes string nullable
}
```

Or we can write a constructor for the class:

```cs
public class Person
{
	public string Name {get; set;}

	public Person()
	{
		if (Name == null) Name = " "; 
	}
}
```

A little bit more laconic option using *compound assignment*:

```cs
//instead of "if" just write
Name ??= " ";
```

Using these methods you will definitely eliminate "not-nullable string" error!  

>[!success]
>BTW, I have found one more method that is the **MOST** convenient!

```cs
public class Person
{
	public string Name {get; set;} = "";
}
```

---
### Zero-Links

1. 

-------
### Links

1. 