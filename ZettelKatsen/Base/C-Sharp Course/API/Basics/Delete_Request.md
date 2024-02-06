Created: 202402062216
Tags: #api-basics 

---
### Reference

Here we are finishing the "HTTP requests tetralogy" with **DELETE** request.

It is pretty easy and quite similar with previous codes:

```cs
[HttpDelete("DeleteUser/{userId}")]
public IActionResult DeleteUser(int userId)
{
	string sqlToDeleteUser = $"DELETE FROM TutorialAppSchema.Users WHERE UserId = {userId}";

	if (_dapper.ExecuteSql(sqlToDeleteUser))
	{
		return Ok();
	}
	else
	{
		throw new Exception("There is no such User ID in the database or failed to delete user. Try again!");
	}
}
```

I think there is no need in explanations because everything here is already self-explanatory.

---
### Zero-Links

1. [[Put_&_Post]]
2. [[First_Controller]]

-------
### Links

1. 