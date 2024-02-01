Created: 202401162127
Tags: #cs-intermediate 

---
### Reference

I think it is obvious what we are going to do here. Let's start. 

==WRITING==

All this work will be implemented into the Main file. Firstly, let's **write** something to the file:

```cs
File.WriteAllText("log.txt", "Text");
// or
File.WriteAllText("log.txt", someVariable);
```
Here we have written a text to a file. However, I should mention that:

>[!caution]
>This method rewrite all file every time when we use it!

So, we have another method that is more detailed:

```cs
using StreamWriter openFile = new("log.txt", append: true);
openFile.WriteLine("Text");
openFile.Close();
```
In this code we have used the **StreamWriter** construction to make *append* instead of full replace. Then we just wrote our data to the file and **closed** it. Always remember to close file or you will get this issue about that **The file is currently used by other process!**. 

By the way, we can escape writing it manually and just use the same construction but with some changes:

```cs
using (StreamWriter openFile = new("log.txt"))
{
	openFile.WriteLine("Text");
}
```
It is quite similar with python. By using this method - we are avoiding to close file *manually*!

==READING==

Well, everything is almost the same here:

```cs
string result = File.ReadAllText("log.txt");
```

^257f33

Or using **StreamReader**:

```cs
using (StreamReader reader = new StreamReader(filePath)) 
{ 
	string line = reader.ReadLine(); 
	Console.WriteLine(line); 
	// You don't need to explicitly close the StreamReader due to the 'using' statement 
}
```

---
### Zero-Links

1. 

-------
### Links

1. 