# 6. Neue Datenbank erstellen

Ihr habt ein Programm welches Zugriff auf eine MySQL-Datenbank braucht?  
Perfekt, denn jetzt können wir unseren MySQL-Server benutzen!

> Damit ihr eine höchstmögliche Sicherheit gewährleisten könnt, gilt es als Best-Practise für jede Applikation eine eigene Datenbank mit einem eigenen Nutzer zu erstellen.  
> Das klingt auf dem ersten Blick nach viel Arbeit, ist in der Praxis aber ziemlich simpel und verhindert dass eine bösartige Anwendung die gesamte Datenbank ausliest!  
> Der Kosten-/Nutzenfaktor ist hier unermesslich hoch.

Wir melden uns also in unserem Terminal an und gehen zu unserem DBMS.

```
mysql -u Nutzername -p
```

![](/assets/create-database-1.png)

Nutzername ist in diesem Fall der root-Nutzername, den wir ja in [Kapitel 5.2](/der-root-user.md) umbenannt haben.  
Hiernach sollen wir natürlich noch unser Passwort eingeben.

Der erste Schritt für uns ist es eine neue Datenbank zu erstellen.  
Das geht ziemlich simpel durch:

```
CREATE DATABASE datenbankName;
```

> Ich würde empfehlen datenbankName an den Namen der Applikation anzupassen.  
> So wird die Verwaltung der Datenbank auf jeden Fall deutlich leichter fallen :\)

![](/assets/create-database-2.png)

> In meinem Beispiel gehe ich davon aus, dass wir [WordPress ](https://de.wordpress.com/)installieren wollen, weshalb ich die Datenbank auch wordpress nenne.

Jetzt benötigen wir einen unabhängigen Benutzer, da man unter gar keinen Umständen einer Anwendung root-Rechte geben sollte!

Das machen wir durch foigenden SQL-Query:

```
CREATE USER 'nutzername'@'localhost' IDENTIFIED BY 'passwort'
```

![](/assets/create-database-3.png)

> Ich nenne den Nutzernamen meist genau wie die Datenbank, da dies meiner Meinung nach am übersichtlichsten zu administrieren ist.

Wir haben nun eine MySQL-Datenbank ohne Nutzer.  
Und einen Nutzer ohne MySQL-Datenbank.

Der nächste Schritt sollte von daher ziemlich offensichtlich sein :\)  
Wir müssen unserem Nutzer die Rechte für die soeben erstelle Datenbank geben.

Hierfür gibt es folgenden Befehl:

```
GRANT SELECT,INSERT,DELETE ON datenbankName.* TO 'nutzername'@'localhost';
```

> SELECT,INSERT,DELETE ist nur eine Beispielskonfiguration!  
> Es handelt sich hierbei um eine Auflistung an Berechtigungen die selbstverständlich an die eigene Applikation angepasst werden muss!  
> Eine offizielle Übersicht an möglichen Berechtigungen gibt es auch wieder in der [offiziellen Documentation](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html).
>
> Benötigt die Anwendung alle Rechte, so kann man auch einfach ALL angeben.  
> Jedoch empfehle ich wirklich dringend nur die Rechte zu vergeben, die benötigt werden.

![](/assets/create-database-4.png)

Herzlichen Glückwunsch, du hast auch diese Aufgabe gemeistert!

Jedoch stellst du dir nun vielleicht die Frage, wie du dich nun mit deiner Datenbank verbinden kannst.  
Dies werde ich im letzten Kapitel genauer erläutern.

## Links:

* Vorheriger Kapitel: [Der root-User](/der-root-user.md)
* Nächster Kapitel: [Die Datenbank verwenden](/die-datenbank-verwenden.md)



