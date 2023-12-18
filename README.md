# VincentRobertThikalvannan_LB_183

## HZ1

### Ransomware
Ransomware ist eine bösartige Software, die darauf abzielt, die Daten eines Benutzers zu verschlüsseln oder den Zugriff darauf zu blockieren, um dann Lösegeld für die Wiederherstellung anzufordern.

#### Massnahmen 
- Erstellen Sie regelmässig eine Sicherungskopie (Backup) Ihrer Daten.
- Schulen Sie die Mitarbeitenden im Umgang mit E-Mails
- Vorsicht beim Öffnen von E-Mails
- Software-Updates

### DDoS (Distributed Denial of Service)
DDOS bezeichnet eine Art von Cyberangriff, bei dem eine Vielzahl von vernetzten Geräten verwendet wird, um gleichzeitig auf ein Ziel zuzugreifen und es so zu überlasten, dass es nicht mehr normal funktionieren kann

#### Massnahmen
- Firewalls und Sicherheitssoftware, um den Datenverkehr zu überwachen und ungewöhnliche Aktivitäten zu erkennen.
- Intrusion Prevention Systeme (IPS)

### Anrufe im Namen von Fake-Behörden (Phishing)
Phishing  bezeichnet eine betrügerische Methode, bei der sich Angreifer als Polizeibehörde ausgeben, Opfer per Telefonanruf dazu auffordern, ein Fernzugriffstool herunterzuladen, um dann unberechtigt auf den Computer zuzugreifen und Zahlungen über das E-Banking-Konto des Opfers auszulösen

#### Massnahmen
- Telefonanrufe sofort abrechnen.
- Nummern blockieren
- Falls Kreditdaten gesagt --> Karte speren. 

### Betrügerische Jobangebote
Fake Stellenangebote locken über soziale Netzwerke und E-Mails mit unrealistischen Verdienstversprechen, führen die Kommunikation im Einstellungsprozess über Instant Messaging und leiten die Bewerber auf gefälschte Websites weiter, um vermeintliche 'Lohnzahlungen' und 'Prämien' abzurechnen. Meine Freunde und ich haben das selbst bekommen.

#### Massnahmen
- Ignorieren Sie diese Art von Nachrichten mit betrügerischen Stellenangeboten
- Seien Sie vorsichtig bei Jobangeboten, die eine Vorauszahlung verlangen

Quellen: https://www.ncsc.admin.ch/ncsc/de/home/cyberbedrohungen.html 


## HZ2

### SQL Injection
 In der Insecure App kann man mit Sql Injection sich als adminsator ausgeben ohne den Passwort zu kennen.

Wenn man beim Einloggen den Benutzernamen nach "administrator" noch die Eingabe von "'--admin" erweitert und ein beliebiges Passwort eingibt, kann man sich als Administrator anmelden.

![image](https://github.com/FruitNinja69/VincentRobertThikalvannan_LB_183/assets/89131450/24290165-e643-49d2-8b5e-e1e9776850a2)



Der Code mit SQL Injection:

![image](https://github.com/FruitNinja69/VincentRobertThikalvannan_LB_183/assets/89131450/d51cc87e-e0f5-47a4-8feb-e53aa6c6ac02)


Der Code ohne SQL Injection:

![image](https://github.com/FruitNinja69/VincentRobertThikalvannan_LB_183/assets/89131450/5cb8c06f-b269-4f36-b405-0691fcdfd7d2)


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

![image](https://github.com/FruitNinja69/VincentRobertThikalvannan_LB_183/assets/89131450/56d218a9-503f-445f-95c0-764ee40b675f)

![image](https://github.com/FruitNinja69/VincentRobertThikalvannan_LB_183/assets/89131450/48a51c58-dd41-4a94-842c-31114ec1c338)

Im Beginn des Anmeldevorgangs erfolgt die Zwei-Faktor-Authentifizierung (2FA). Wenn ein Nutzer über einen 2FA-Schlüssel verfügt, wird geprüft, ob der eingegebene Benutzerschlüssekorrekt ist. Bei Misserfolg wird eine "Unauthorized" (401)-Meldung zurückgegeben.

### Autoriserung




