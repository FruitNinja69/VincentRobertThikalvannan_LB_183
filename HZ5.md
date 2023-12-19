## HZ 5

Informationen für Auditing und Logging generieren. Auswertungen und Alarme definieren und implementieren.

### Logging 

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

### Auswahl und Beschreibung der Artefakts
Als Artefakt habe ich einen Teil des Codes aus der Insecure App ausgewählt, der zeigt, wie die Anwendung Log-Informationen und Warnungen ausgibt, insbesondere während des Einloggprozesses.

### Nachweis der Zielreichung 
Ich habe diese Handlungsziel umgesetzt, indem die Insecure App Logging informationen generiert. 

### Erklärung des Artefakts
Wenn kein Benutzer gefunden wird, wird eine Warnung im Log erstellt, die besagt, dass die Anmeldung für den angegebenen Benutzer fehlgeschlagen ist, und es wird ein "Unauthorized"-Status zurückgegeben. Wenn ein Benutzer erfolgreich angemeldet ist, wird eine Log-Information für den erfolgreichen Anmeldevorgang erstellt, und es wird ein "Ok"-Status mit einem generierten Token zurückgegeben.

### Kritische Beurteilung

Ich habe mit meinem Artefakt das Logging nur für den Einloggprozess implementiert. Allerdings könnte man diese Logging auch auf andere Aspekte erweitern, wie beispielsweise bei den CRUD-Befehlen. Wenn Nutzer Änderungen vornehmen, wäre es nützlich festzuhalten, welcher Nutzer diese Änderungen vorgenommen hat.



