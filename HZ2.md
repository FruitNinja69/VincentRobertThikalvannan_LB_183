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



