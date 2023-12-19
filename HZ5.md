## HZ 5

Informationen für Auditing und Logging generieren. Auswertungen und Alarme definieren und implementieren.

Im Code wird implementiert, dass bei falschen Benutzerdaten die Meldung "login failed for user '{request.Username}'" in der Konsole angezeigt wird. Wenn die Daten korrekt sind, wird die Meldung "login successful for user '{request.Username}'" angezeigt.

Code:
``` csharp
public ActionResult<User> Login(LoginDto request)
{
    if (request == null || request.Username.IsNullOrEmpty() || request.Password.IsNullOrEmpty())
    {
        return BadRequest();
    }
    string username = request.Username;
    string passwordHash = MD5Helper.ComputeMD5Hash(request.Password);

    User? user = _context.Users
        .Where(u => u.Username == username)
        .Where(u => u.Password == passwordHash)
        .FirstOrDefault();

    if (user == null)
    {
        _logger.LogWarning($"login failed for user '{request.Username}'");
        return Unauthorized("login failed");
    }

    _logger.LogInformation($"login successful for user '{request.Username}'");
    return Ok(CreateToken(user));
}
```


Auf der Konsole sind diese Loginformationen ersichtlich:

![image](https://github.com/FruitNinja69/VincentRobertThikalvannan_LB_183/assets/89131450/55013093-e7a1-40e4-817a-fa55a629c3cc)
