### Basic authentication
```C#
using Microsoft.IdentityModel.Tokens;
using Microsoft.IdentityModel.Jwt;
using System.Security.Claims;
```

User model include
```C#
public class User
{
	public Guid Id { get; set;}
	public string Username { get; set; }
	public string Password { get; set; }
	public string Salt { get; set; }
}
```

And helper functions to identify a user on an api endpoint with ``[Authorize]``
```C#
[HttpGet]
[Authorize]
public IActionResult Get()
{
	var userId = _pauliHelper.GetRequestUserId(HttpContext);
	var user = _context.Users.Find(userId);
	if (user == null) return BadRequest("User not found from JWT claim. This should not be possible.");
	
	return Ok($"Hello {user.Username} securly");
}
```


