# 5. MySQL absichern

Standardmäßig ist der MySQL Server nur lokal aufrufbar... zu unserem Glück.  
Denn das was wir soeben erschaffen haben, ist noch sehr anfällig für jederlei Angriffsszenarien die es um jeden Preis zu vermeiden gilt.

Sicherheit ist kein Status sondern ein Prozess.  
Jede einzelne Schicht an Sicherheit erschwert es einem potenziellen Angreifer immens seine gewünschten Resultate zu erzielen.

Um unser System abzuhärten, liefert MySQL direkt das Skript [mysql\_secure\_installation](https://dev.mysql.com/doc/refman/5.7/en/mysql-secure-installation.html), welches uns \(grob übersetzt\) folgende Optionen anbietet:

* Du kannst ein root-Passwort festlegen
* Du kannst root-Accounts löschen, die vom Internet aus aufrufbar sind
* Du kannst anonyme Accounts \(Accounts ohne Kennwortschutz und ohne Identität\) löschen
* Du kannst die Test-Datenbank löschen \(da die für alle Nutzer aufrufbar ist\)

Den ersten Schritt haben wir ja bereits während der Installation erledigt, also sollten wir noch die letzten drei Schritte erledigen.  
Hierfür nutzen wir den bereits erwähnten Skript, indem wir folgenden Befehl ins Terminal geben:

```
sudo mysql_secure_installation
```

![](/assets/secure-mysql-1.png)

Wir werden direkt nach dem root-Passwort für unsere MySQL-Datenbank gefragt, da wir uns ja authentifizieren müssen... also gut, dann machen wir das mal.

![](/assets/secure-mysql-2.png)

Danach fragt uns das Skript, ob wir das [validate\_password](https://dev.mysql.com/doc/refman/5.7/en/validate-password-plugin.html) Plugin aktivieren wollen, welches uns erlaubt eine Password Policy festzulegen, um schwache Passwörter für Datenbanknutzer zu verhindern.

Natürlich wollen wir das, weshalb wir das mit einem Y bestätigen.

![](/assets/secure-mysql-3.png)  
Wir werden noch gefragt welche Sicherheitsstufe von 0 \(das schwächste\) bis 2 \(das stärkste\) wir wollen.  
Ich habe mich für die 2 entschieden, da ich ohnehin einen Passwort-Manager verwende.

![](/assets/secure-mysql-4.png)

MySQL zeigt uns nun die Stärke von unserem root-Passwort an.  
Was der Wert bedeutet ist freundlicherweise auch [dokumentiert ](https://dev.mysql.com/doc/refman/5.7/en/encryption-functions.html#function_validate-password-strength):\)

Sollte euer Wert nicht bei hundert liegen, so würde ich mir überlegen vielleicht Y auszuwählen um das Kennwort zu ändern.  
Da wir brav die volle Punktzahl haben, wählen wir einen beliebigen Buchstaben... ich nehme das N für No.

![](/assets/secure-mysql-5.png)



## Links:

* Vorheriger Kapitel: Das Paket installieren
* Nächster Kapitel: Noch nicht verfasst.



