## HZ 3
Mechanismen für die Authentifizierung und Autorisierung umsetzen können.

### Authentifizierung

In der "Insecure App" ist nun eine Zwei-Faktor-Authentifizierung integriert. Diese ermöglicht es dem Benutzer, sie zu aktivieren, sobald er sich angemeldet hat. Nach der Aktivierung wird ein QR-Code generiert, den der Benutzer mit seinem Handy scannen kann. Es ist erforderlich, die App "Google Authenticator" auf dem Handy herunterzuladen, um diesen Prozess abzuschließen.

Bild eines generierten QR-Codes:

![image](https://github.com/FruitNinja69/VincentRobertThikalvannan_LB_183/assets/89131450/7869d1f7-e9fb-4c2e-98b5-4b0fdf734e3a)

Bild von der Login-Seite, auf der man den 2FA-Code eingeben muss:

![image](https://github.com/FruitNinja69/VincentRobertThikalvannan_LB_183/assets/89131450/d176b379-22c4-4edd-ac8b-7535707b7149)

Google Authenticator:

![image](https://github.com/FruitNinja69/VincentRobertThikalvannan_LB_183/assets/89131450/e1568293-127f-4732-9d8b-b7b5be51d92b)

Implentation im Code:

``` csharp
if (user.SecretKey2FA != null)
{
    string secretKey = user.SecretKey2FA;
    string userUniqueKey = user.Username + secretKey;
    TwoFactorAuthenticator authenticator = new TwoFactorAuthenticator();
    bool isAuthenticated = authenticator.ValidateTwoFactorPIN(userUniqueKey, request.UserKey);
    if (!isAuthenticated)
    {
        return Unauthorized("login failed");
    }
}
``` 

``` csharp
public ActionResult<Auth2FADto> Enable2FA()
{
    var user = _context.Users.Find(_userService.GetUserId());
    if (user == null)
    {
        return NotFound(string.Format("User {0} not found", _userService.GetUsername()));
    }
    {
        var secretKey = Guid.NewGuid().ToString().Replace("-", "").Substring(0, 10);
        string userUniqueKey = user.Username + secretKey;
        string issuer = _configuration.GetSection("Jwt:Issuer").Value!;
        TwoFactorAuthenticator authenticator = new TwoFactorAuthenticator();
        SetupCode setupInfo = authenticator.GenerateSetupCode(issuer, user.Username, userUniqueKey, false, 3);

        user.SecretKey2FA = secretKey;
        _context.Update(user);
        _context.SaveChanges();

        Auth2FADto auth2FADto = new Auth2FADto();
        auth2FADto.QrCodeSetupImageUrl = setupInfo.QrCodeSetupImageUrl;

        return Ok(auth2FADto);
    }
}
```
Im Beginn des Anmeldevorgangs erfolgt die Zwei-Faktor-Authentifizierung (2FA). Wenn ein Nutzer über einen 2FA-Schlüssel verfügt, wird geprüft, ob der eingegebene Benutzerschlüssekorrekt ist. Bei Misserfolg wird eine "Unauthorized" (401)-Meldung zurückgegeben.

### Autoriserung
``` csharp
  public ActionResult Delete(int id)
 {
     var news = _context.News.Find(id);
     if (news == null)
     {
         return NotFound(string.Format("News {0} not found", id));
     }

     if (!_userService.IsAdmin() && _userService.GetUserId() != news.AuthorId)
     {
         return Forbid();
     }

     _context.News.Remove(news);
     _context.SaveChanges();
     
     return Ok();
 }
```

### Auswahl und Beschreibung der Artefakts
Als Artefakt habe ich einen Teil des Codes aus der Insecure App genommen, der zeigt, wie die App Mechanismen für die Authentifizierung und Autorisierung haben.Ich habe auch einen Teil der App gezeigt, um zu verdeutlichen, wie der Anmeldeprozess und der QR-Code aussehen. Darüber hinaus habe ich auch den Code für Google Authenticator hinzugefügt, um zu zeigen, wie er aussieht.

### Nachweis der Zielreichung 
Ich habe dieses Ziel erreicht, indem ich dem Insecure App die Zwei-Faktor-Authentifizierung (2FA) hinzugefügt habe. Die Autorisierung wird ebenfalls umgesetzt, indem ich in der Funktion "Delete" überprüfe, ob der Benutzer als Administrator angemeldet ist oder nicht. Damit habe ich Mechanismen für die Authentifizierung und Autorisierung erfolgreich implementiert.

### Erklärung des Artefakts
#### Autoriserung
Im Code-Abschnitt wird überprüft, ob der Benutzer kein Administrator ist. Wenn der Benutzer ein Administrator ist, hat er automatisch die Erlaubnis. Es wird überprüft, ob die Benutzer-ID der Person, die die Aktion ausführt, nicht mit der ID des Autors der Nachricht übereinstimmt. Wenn die IDs nicht übereinstimmen, bedeutet das, dass die Person nicht der Autor der Nachricht ist. Wenn mindestens eine dieser Bedingungen erfüllt ist, wird die Aktion nicht erlaubt, was bedeutet, dass der Benutzer die Nachricht nicht löschen darf.

#### Authentifizierung
Der erste Codeabschnitt überprüft, ob der Benutzer die Zwei-Faktor-Authentifizierung (2FA) aktiviert hat und authentifiziert den Benutzer basierend auf dem eingegebenen 2FA-Schlüssel.

Der zweite Codeabschnitt ermöglicht die Aktivierung der 2FA für einen Benutzer, indem ein neuer geheimer Schlüssel generiert und ein QR-Code erstellt wird. Im Erfolgsfall gibt er den QR-Code zurück.

### Kritische Beurteilung



