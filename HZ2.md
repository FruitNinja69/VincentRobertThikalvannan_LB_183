## HZ2
Sicherheitslücken und ihre Ursachen in einer Applikation erkennen können. Gegenmassnahmen vorschlagen und implementieren können.

### SQL Injection
 In der Insecure App kann man mit Sql Injection sich als adminsator ausgeben ohne den Passwort zu kennen.

Wenn man beim Einloggen den Benutzernamen nach "administrator" noch die Eingabe von "'--admin" erweitert und ein beliebiges Passwort eingibt, kann man sich als Administrator anmelden.

![image](https://github.com/FruitNinja69/VincentRobertThikalvannan_LB_183/assets/89131450/24290165-e643-49d2-8b5e-e1e9776850a2)



Der Code mit SQL Injection:

``` csharp 
public ActionResult<User> Login(LoginDto request)
        {
            if (request == null || request.Username.IsNullOrEmpty() || request.Password.IsNullOrEmpty())
            {
                return BadRequest();
            }

            string sql = string.Format("SELECT * FROM Users WHERE username = '{0}' AND password = '{1}'", 
                request.Username, 
                MD5Helper.ComputeMD5Hash(request.Password));

            User? user= _context.Users.FromSqlRaw(sql).FirstOrDefault();
            if (user == null)
            {
                return Unauthorized("login failed");
            }
            return Ok(user);
        }

```

Der Code ohne SQL Injection:

``` csharp
 public ActionResult<User> Login(LoginDto request)
        {
            if (request == null || request.Username.IsNullOrEmpty() || request.Password.IsNullOrEmpty())
            {
                return BadRequest();
            }

            string username = request.Username;
            string passwordHash = MD5Helper.ComputeMD5Hash(request.Password);

            // Lösungsansatz
            User? user = _context.Users
                .Where(u => u.Username == username)
                .Where(u => u.Password == passwordHash)
                .FirstOrDefault();


            if (user == null)
            {
                return Unauthorized("login failed");
            }
            return Ok(user);
        }

```


Daher ist es wichtig, seinen Code auf SQL-Injection zu überprüfen.

### Auswahl und Beschreibung der Artefakts
Als Artefakt habe ich einen Teil des Codes aus der Insecure App genommen, der zeigt, wie die App auf SQL-Injection geschützt ist.

### Nachweis der Zielreichung 
Ich habe dieses Ziel erreicht,indem ich Sicherheitslücken und ihre Ursachen in einer Applikation erkennt habe und  Gegenmassnahmen implementiert habe ich mit SQL-Injection gezeigt.

### Erklärung des Artefakts
Der erste Code (mit SQL Injection) mischt Benutzereingaben direkt in die SQL-Abfrage, was gefährlich sein kann, weil böswillige Benutzer die Eingabe manipulieren können, um unerwünschte Dinge zu tun.

Der zweite Code (ohne SQL Injection) benutzt sicherere Wege, um die Datenbank abzufragen. Er schützt vor solchen Angriffen, indem er kluge Methoden verwendet, die sicherer sind und die Anwendung besser vor möglichen Gefahren schützen.

### Kritische Beurteilung
Ich habe SQL-Injection erklärt und Maßnahmen dagegen implementiert, aber es gibt auch Cross-Site Scripting (XSS), das im Modul 183 behandelt wird und ähnlich funktioniert. Man kann in den Eingabefeldern JavaScript-Befehle eingeben, was eine häufige Sicherheitslücke darstellt.
