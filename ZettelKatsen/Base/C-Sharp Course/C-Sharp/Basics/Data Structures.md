Created: 202401092101
Tags: #cs-basics 

---
### Reference

==Arrays==

To create array we need to type the data type with square brackets and then initialize it. 

>[!example]
>
>```cs
>string[] strArr = new string[n]; // n is a size
>int[] intArr = new int[n];
>```
>Also, we can initialize it in this way:
>```cs
>string[] strArr = {"Hello", "Aiden"};
>```

Oh, I just found out that *int array* can be initialized that simple too: ^2c7576

```cs
// instead of this
int[] arr = new int[] {1,2,3};
// we can write
int[] arr = [1,2,3];
```

^9caede

==List==

List is quite similar to an array but they have some differences. *Array's size is fixed* and cannot be changed while *List is a dynamic type* and can be changed throughout a program. 

>[!example]
>Implementation looks like this:
>```cs
>List<string> myList = new List</string>(n);
>```
>Or:
>```cs
>List<string> myList = new List</string>() {"Hello", "Andrew"};
>```

To add something to the List we use:

```cs
myList.add("Orange");
```

==IEnumerable==
This is something like List but without indexes. As I understood, this is kind of iterable data structure that convenient for my own classes, because i can iterate them using foreach.  ^1e055c

Likewise, IEnumerable is the most efficient data structure to iterate! 

```cs
IEnumerable<string> en = strList;
```

==Dimensions==

By the way, we can create multi-dimensional arrays like this:
```cs
List<string> mda = new List<string>[,] {
	{"Apples", "Milk"},
	{"Oranges", "Lemons"}
};
```
So, the [,] is responsible for the dimensions. If we place two comas it will be three dimensional array:

```cs
List<string> mda = new List<string>[,,]()
```

==Dictionary==

Dictionary is a key - value data structure. Looks like this:

>[!example]
>
>```cs
>Dictionary<string, string> myDct = new Dictionary<string, string>() {
>	{"Pasta", "Food"},
>	{"Cement", "Not Food"}
>};
>```
>Also, we can get a value by the key:
>```cs
>Console.WriteLine(myDct["Pasta"]);
>```

---
### Zero-Links

1. 

-------
### Links

1. [[Data Types]]