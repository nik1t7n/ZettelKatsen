Created: 202401262100
Tags: #sql_basics 

---
### Reference

I think here everything is pretty self-explanatory and trivial. Here the code:

==INSERT==

```sql
INSERT INTO TutorialAppSchema.Computer 
(
    [Motherboard],
    [CPUCores],
    [HasWifi],
    [HasLTE],
    [ReleaseDate],
    [Price],
    [VideoCard]
) VALUES 
(
    'Sample-Motherboard',
    4,
    1,
    0,
    '2021.01.01',
    1000,
    'RTX 4060 T'
)
```
Notice that we haven't specified ComputerId because [[Create a table#^2a6f4c|it will be filled automatically]]. However we can do it by writing this before the code:

```sql
SET IDENTITY_INSERT TutorialAppSchema.Computer ON   --it can allow us to insert ComputerId
```

Next, let's ==DELETE== something by ComputerId:

```sql
DELETE FROM TutorialAppSchema.Computer WHERE ComputerId = 101
```

And last – ==UPDATE==:

```sql
UPDATE TutorialAppSchema.Computer SET CPUCores = 8 WHERE ComputerId = 101 -- if there is no such number (101) it will apply to the all rows

UPDATE TutorialAppSchema.Computer SET CPUCores = 2 WHERE ReleaseDate < '2017.01.01'
```
You can manipulate with it and make conditions any way you want. 

Likewise, you can sort something. 

>[!tip] Sorting
>-
>```sql
>ORDER BY HasWifi, ReleaseDate DESC
>```

We can sort by one or many fields and change the direction (ascending, descending). 

---
### Zero-Links

1. 

-------
### Links

1. 