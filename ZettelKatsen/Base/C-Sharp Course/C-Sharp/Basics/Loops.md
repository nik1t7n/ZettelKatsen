Created: 202401100920
Tags: #cs-basics 

---
### Reference

Okay, *while* and *for* loops are quite obvious so I will show just ==how to iterate== *for* loop in an array:

```cs
int[] arr = new int[] {1,2,3,4,5,6,7,8,9};

for (int i = 0; i < arr.Length; i++) // using .Length --without parentheses
{
	Console.WriteLine(arr[i]);
}
```

A little trick from last files :)
>[!tip] HINT
>![[Data Structures#^9caede]]

There is also very convenient for-like loop called ==foreach==. It is very safe because we cannot get "out-of-range" error using this loop. Likewise, it is 2x faster than simple *for* loop! ^d08d4e

```cs
foreach(int element in arr)
{
	Console.WriteLine(element);
}
```

Besides *while-loop* there is also a ==do-while== loop:

```cs
int[] arr = [1,2,3,4,5];
int index = 0;

do
{
	Console.WriteLine(arr[index]);
	index++;
} 
while (index < arr.Length);

// output: 1 2 3 4 5
```
So, the main point of this loop is that it will run at least one time, because it firstly does the action and then checks the condition. 

>[!tip] Embedded sum method
>```cs
>int[] arr = [1,2,3,4,5];
>total = arr.Sum(); // 15

By the way!
> [!question] > The "Do-While" loop is the fastest, next "foreach", then "while" and then "for"


---
### Zero-Links

1. 

-------
### Links

1. 