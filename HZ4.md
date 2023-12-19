## HZ 4
Sicherheitsrelevante Aspekte bei Entwurf, Implementierung und Inbetriebnahme berücksichtigen.

### HumanFactor
Die meisten Menschen wählen ein einfaches Passwort wie zum Beispiel "1234". Dadurch wird der Mensch zur Sicherheitslücke, da er ein leicht zu erratendes Passwort verwendet. Um dies zu vermeiden, verfügt die Insecure App über eine Funktion, die bei der Passworterstellung Variationen verlangt, um das Passwort sicherer zu machen.

``` csharp
 private string validateNewPasswort(string newPassword)
 {
     // Check small letter.
     string patternSmall = "[a-zäöü]";
     Regex regexSmall = new Regex(patternSmall);
     bool hasSmallLetter = regexSmall.Match(newPassword).Success;

     string patternCapital = "[A-ZÄÖÜ]";
     Regex regexCapital = new Regex(patternCapital);
     bool hasCapitalLetter = regexCapital.Match(newPassword).Success;

     string patternNumber = "[0-9]";
     Regex regexNumber = new Regex(patternNumber);
     bool hasNumber = regexNumber.Match(newPassword).Success;

     List<string> result = new List<string>();
     if (!hasSmallLetter)
     {
         result.Add("keinen Kleinbuchstaben");
     }
     if (!hasCapitalLetter)
     {
         result.Add("keinen Grossbuchstaben");
     }
     if (!hasNumber)
     {
         result.Add("keine Zahl");
     }

     if (result.Count > 0)
     {
         return "Das Passwort beinhaltet " + string.Join(", ", result);
     }
     return "";
 }
```

### Auswahl und Beschreibung der Artefakts
Als Artefakt habe ich einen Teil des Codes aus der Insecure App genommen, der zeigt, wie die App gegen den menschlichen Faktor als Sicherheitslücke geschützt ist.

### Nachweis der Zielreichung 
Ich habe diese Handlungsziel umgesetzt, indem ich die Insecure App gegen den menschlichen Faktor geschützt habe.

### Erklärung des Artefakts
Der Code-Abschnitt zeigt, wie das Programm vor einfachen Passwörtern, wie zum Beispiel "1234", geschützt ist. So wurde die Anwendung gegen die Verwendung von schwachen Passwörtern abgesichert.

### Kritische Beurteilung

Ich habe den "Human Factor" bisher nur auf die Passwortwahl angewendet. Allerdings gibt es auch andere Aspekte, die berücksichtigt werden sollten, wie beispielsweise die Anfälligkeit für Phishing. Dabei könnten Benutzer auf gefälschte Websites gelockt werden und versehentlich ihre Anmeldeinformationen preisgeben.
