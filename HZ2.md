## HZ2

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

            /*
            // Lösungsansatz 1: Sauber interpoliertes SQL
            User? user = _context.Users.FromSql($"SELECT * FROM Users WHERE username = {username} AND password = {passwordHash}")
                .FirstOrDefault();
            */

            // Lösungsansatz 2: EntityFramework Where
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

### Security Code Review

#### Motivation:

- Security Code Review bezieht sich auf die Überprüfung von Softwareanwendungen, um Sicherheitslücken zu identifizieren und zu beheben. Dies umfasst den Code, die Architektur und andere potenzielle Risiken.

#### Manueller Code Review:

- Regelmässige manuelle Code Reviews sind entscheidend für die Sicherheitsüberprüfung.
- Sie können Teile oder die gesamte Applikation abdecken.
- Statische Testmethode, bei der Entwickler und Sicherheitsexpert potenzielle Schwachstellen, Eingabevalidierung, Authentifizierungsmethoden usw. überprüfen.
- Die Reviewer sollte die Applikation, den Kontext, die Programmiersprache und Sicherheitsaspekte gut kennen.

#### Automatisierte Sicherheitsprüfungen:

- Neben manuellen Reviews sollten automatisierte Sicherheitsprüfungen durchgeführt werden
- Tools und Scanner identifizieren bekannte Schwachstellen und Konfigurationsfehler.
- Ergebnisse müssen genau überprüft werden, da nicht alle Hinweise korrekt sein könnten (false positive).
  
#### Architektur Reviews

- Architektur ist wichtig für die Sicherheitsüberprüfung
- Experten prüfen die Gesamtarchitektur auf Schwachstellen und sicherheitsrelevante Designentscheidungen.
- Der Datenfluss innerhalb der Anwendung wird verfolgt, um sicherzustellen, dass sensible Daten angemessen geschützt sind.

#### Best Practices:

- Sicherheitsreviews sollten regelmässig im Entwicklungszyklus durchgeführt werden
- Checklisten gewährleisten ein konsistentes Vorgehen und verhindern das Vergessen von wichtigen Aspekten.
- Alle gefundenen Sicherheitsprobleme müssen dokumentiert und verfolgt werden.

### Pentest

Pentesting, kurz für "Penetrationstests" ist, wo Experten nach Sicherheitsproblemen in Webapplikationen suchen. Ob das gut klappt, hängt davon ab, wie schlau die Experten sind. Aber hier ist die Sache: Wenn die nix finden, heisst das nicht, dass da wirklich keine Lücken sind.

Vor dem eigentlichen Test liest man sich erstmal alles durch: das Pflichtenheft, den Code alles. Dann setzt man sich Ziele und fängt an zu analysieren. Das bedeutet Scans machen, um Schwachstellen zu finden. Was man findet, wird aufgeschrieben und dem Kunden gezeigt. Nachdem die Probleme gefixt wurden, macht man nochmal einen Test.

Und ganz wichtig: Tools, aber die können Expertenwissen nicht ersetzen. Es gibt so Security-Scanner, die automatisch nach Lücken suchen.

