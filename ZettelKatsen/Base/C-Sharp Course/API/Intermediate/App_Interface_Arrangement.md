Created: 202402152205
Tags: #api-intermediate 

---
### Reference

Now we will just finish all the job that we started in [[Interface|previous lecture]] by configuring *Interface* for peripheral functionality such as *UserSalary* and *UserJobInfo*.

Before we start exploring code, here the drawing how I see the concepts that we made:

![[Pasted image 20240215221418.png]] ^b1548e

So, we have the **APP** (Main File) that have ability to use controllers. And they, in turn, use **[[Interface|IUserRepository]]** and it connect already to **[[Repository_Pattern|UserRepository]]**. Further we see Entity Framework / Dapper that had direct access to the database. Likewise, I consider two red layers as a pure abstraction.

---
### Zero-Links

1. 

-------
### Links

1. 