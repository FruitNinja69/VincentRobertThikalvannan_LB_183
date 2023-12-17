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
 In der Insecure App kann man mit Sql Inkection sich als adminsator ausgeben ohne den Passwort zu kennen.

Wenn man beim Einloggen den Benutzernamen nach "administrator" noch die Eingabe von "'--admin" erweitert und ein beliebiges Passwort eingibt, kann man sich als Administrator anmelden.
![image](https://github.com/FruitNinja69/VincentRobertThikalvannan_LB_183/assets/89131450/24290165-e643-49d2-8b5e-e1e9776850a2)


Das Code ohne SQL Injection:
![image](https://github.com/FruitNinja69/VincentRobertThikalvannan_LB_183/assets/89131450/d51cc87e-e0f5-47a4-8feb-e53aa6c6ac02)

Das Code mit SQL Injection:
![image](https://github.com/FruitNinja69/VincentRobertThikalvannan_LB_183/assets/89131450/5cb8c06f-b269-4f36-b405-0691fcdfd7d2)


