# 5.2 Der root-User

Wie ich anfangs erwähnt habe besteht Sicherheit nicht aus einer monolithischen Mauer, sondern besteht aus vielen einzelnen Schichten die jeweils die Aufgabe erfüllen den Angreifer auszubremsen.

Wir haben dem root-User im vorherigen Schritt bereits ein starkes Kennwort gegeben, doch wir könnten die Präsenz des root-Users verbergen und somit bestimmten Tools die Arbeit erschweren.

In diesem Schritt werden wir den root-User umbenennen und erhalten somit auch erste Erfahrungen von der Datenbank-Administration... zwei Fliegen mit einer Klappe :\)

Also gut, da wir ja noch frisch in unserem Terminal sind, können wir uns direkt mal die MySQL-Konsole öffnen.

Hierzu geben wir folgenden Befehl in unser Terminal ein:

```
mysql -u root -p
```

> mysql ist unser Datenbanksystem bei dem wir uns einloggen wollen.
>
> Mit -u spezifiziere ich den Nutzer der danach kommt als den User, mit dem ich mich einloggen möchte.  
> In diesem Fall ist das \(noch\) root.
>
> Mit -p spezifiziere ich noch, dass ich gleich noch ein Passwort zur Authentifizierung eingeben möchte.  
> Gebt auf gar keinen Fall das Kennwort ungeschützt im Terminal ein!

![](/assets/change-root-1.png)

Wir geben nun schlichtweg unser root-Kennwort für MySQL ein und schon sind wir drin in unserem DBMS \(kurz für: Datenbank-Management-System\).

![](/assets/change-root-2.png)

Der nächste Schritt ist zwar im Prinzip ziemlich simpel, aber ungewohnt.  
Denn der nächste Befehl den wir dieses mal im DBMS eingeben endet mit einem Semikolon!

Warum das so ist, ist ziemlich einleuchtend: Wir arbeiten aktuell direkt auf der Datenbank.  
Diese wird über [SQL](https://de.wikipedia.org/wiki/SQL) gesteuert, was eine vollwertige Programmiersprache ist.

SQL ist zwar egal ob wir außerhalb von Anführungszeichen Groß schreiben oder nicht, aber die meisten Hilfestellungen online verwenden eben das dauerhafte Capslock, weshalb ich mich mal dem Gruppenzwang anschließe :\)

Wir geben also folgenden Befehl ein, und ändern entsprechend den Nutzernamen:

```
RENAME USER 'root'@'localhost' TO 'neuerNutzername'@'localhost';
```

> Der Befehl an sich sollte ziemlich klar verständlich sein:  
> Benenne den Nutzer 'root' \(der nur von localhost aufgerufen werden darf\) in 'neuerNutzername' \(der nur von localhost aufgerufen werden darf\) um.
>
> Ich habe hier nun für meinNutzername eine 32 Buchstaben und Zahlen lange Zeichenkette gewählt.  
> Ob das wirklich sinnvoll ist, kann ich nicht direkt beurteilen.  
> Mein persönlicher Verwaltungsaufwand erhöht sich immerhin nicht, da ich ja einen Passwortmanager verwende.  
> Wichtig ist hier eigentlich nur zu verhindern, dass eben Standard-Nutzernamen wie "admin", "root" oder ähnliches vermieden werden.

![](/assets/change-root-3.png)

Nachdem das erledigt ist, sollten wir natürlich die Verwaltungsdatenbank wieder dazu bringen die neusten Änderungen auszulesen.

Das machen wir durch den folgenden Befehl:

```
FLUSH PRIVILEGES;
```

![](/assets/change-root-4.png)

Um nun das DBMS zu verlassen und zurück zum Terminal zu gehen, müssen wir nun einfach den folgenden Befehl eingeben:

```
EXIT;
```

## Links:

* Vorheriger Kapitel: [Setup](/setup.md)
* Nächster Kapitel: [mysqld.cnf](/mysqldcnf.md)
* [Inhaltsverzeichnis](https://www.gitbook.com/book/xhadius/mysql-auf-einem-linux-system-einrichten/edit#)



