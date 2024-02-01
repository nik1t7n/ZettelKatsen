Created: 202401090901
Tags: #cs-basics 

---
### Reference

Let's begin from the smallest ones!

There are two types of "bite" variables in C#: ==byte== and ==sbyte==
They use only only 8 bits of memory (255 nums)

> [!info]
>**Byte** is unsigned by default, it means that in can have only positive numbers from 0 to 255 (inclusive). 
>
>**Sbyte** is a signed bite variable respectively, so it means that it will have the same amount of numbers (255) but divided into positives and negatives – from *-128* to *127*.  
>
>```cs
>byte myByte = 255;
>sbyte mySByte = -128;
>```




Next ones is the ==unshort== and ==short==. It uses already 16 bits of memory, which means that it can handle more data inside!

> [!info]
> **Unshort** is an unsigned type. It can have any values from *0* to *65535*. 
>
> **Short** handles the same amount of absolute data, but it allowed to use negatives too. From *-32768* to *32768*.
> 
>```cs
>unshort myByte = 65535;
>sbyte mySByte = -31000;
>```

And finally the MAIN one is the ==int==! It contains 32 bits. 

> [!info]
> **Int** is a signed type. It handles $10^{9}$ values in positive and the same in negative. 
> 
>```cs
>int myInt = 2000001;
>```


The ==long== is the most capacious non-float because it contains 64 bits. 
> [!info]
> **Long** is a signed type. It handles $10^{18}$ values in positive and the same in negative. 
> 
>```cs
>long myLong = 100000009;
>```

--
Other types is quite similar but have different amount of capacity (bits inside). There are ==float==, ==double== and ==decimal==. 

> [!info]
> **Float** can handle 32 bits floating point number. It initialized with a "f" letter in the end. 
>
> **Double** is absolutely the same, but handles 64 bits. It may be initialized with "d" in the end and without it. 
> 
> **Decimal** capacity is 128 bits ($10^{36}$ values). It initialized using a "m" letter. 
> 
>```cs
>float myFloat = 0.751f;
>double firstD = 0.237;
>double secondD = 0.237d;
>decimal myDecimal = 0.355m;
>```

--
Last two types are ==string== and ==bool==. String just handles characters while bool only True or False. 

>[!example]
>```cs
>string myStr = "Nikita Hello";
>bool b = true;
>```

---
### Zero-Links

1. 

-------
### Links

1. 