# 6 Neue Datenbank erstellen

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
CREATE DATABASE nameDerDatenbank;
```

> Ich würde empfehlen nameDerDatenbank an den Namen der Applikation anzupassen.  
> So wird die Verwaltung der Datenbank auf jeden Fall deutlich leichter fallen :\)

![](/assets/create-database-2.png)

> In meinem Beispiel gehe ich davon aus, dass wir [WordPress ](https://de.wordpress.com/)installieren wollen, weshalb ich die Datenbank auch wordpress nenne.

Jetzt benötigen wir einen unabhängigen Benutzer, da man unter gar keinen Umständen einer Anwendung root-Rechte geben sollte!

Das machen wir durch foigenden SQL-Query:

```
CREATE USER 'nutzername'@'localhost' IDENTIFIED BY 'passwort'
```

## Links:

* Vorheriger Kapitel: [mysqld.cnf](/mysqldcnf.md)
* Nächster Kapitel: Existiert noch nicht :\)



