# MySQL

## Was ist MySQL?

MySQL ist eine beliebte relationale Datenbank die von vielerlei großen Softwareunternehmen eingesetzt wird.  
Dazu gehören zum Beispiel [Facebook](https://www.mysql.de/customers/view/?id=757), [YouTube ](https://www.mysql.de/customers/view/?id=750)und [Wikipedia](https://www.mysql.de/customers/view/?id=663).

Zu ihren großen Stärken gehören neben der hohen Reife auch die Tatsache, dass die Datenbank eine starke Open Source Community hat und [der Quelltext frei vorliegt](https://github.com/mysql/mysql-server "Die Repository vom MySQL-Server").

Eine solche Datenbank ist spätestens dann sehr wichtig, wenn du mit mehreren Applikationen gleichzeitig auf Datensätze zugreifen und diese unter Umständen sogar verarbeiten musst.

## Was ist eine relationale Datenbank?

Eine relationale Datenbank speichert seine Daten in sogenannten Relationen, die häufig auch Tabellen genannt werden.  
Jeder Datensatz wird als Zeile in dieser Tabelle gespeichert.  
Die Spalten der Tabelle stellen hierbei die Attribute der Datenbank dar.

Stell dir vor du möchtest für jeden Spieler des Servers seine Rechte speichern.  
Wie würdest du das am ehesten machen?

Ich würde mehrere Tabellen erstellen in denen du vollständig unterschiedliche Datensätze speicherst.  
In der ersten Tabelle würde ich Beispielsweise die Nutzer und ihre Gruppen speichern und sie "Users" nennen.  
Die zweite Tabelle erhält dann die Informationen zur Gruppe wie zum Beispiel eine einmalige ID und ihren Namen \("Groups"\).  
Und zu guter letzt gibt es noch eine dritte Tabelle, in der die einzelnen Rechte der Gruppen liegen \("Permissions"\).

In der Praxis sähe das zum Beispiel so aus:

### Users

| uuid | group |
| :--- | :--- |
| bb66bd0c-a8c0-478d-afac-449c44f57da2 | 1 |
| 873c5315-1d81-48d4-b01c-d6e2c7d5b977 | 2 |
| baae8c3d-4f66-418f-afab-881cea0dc412 | 2 |

### Groups

| group | name |
| :--- | :--- |
| 1 | Administrator |
| 2 | Spieler |

### Permissions

| group | permission |
| :--- | :--- |
| 1 | \* |
| 2 | essentials.msg |
| 2 | essentials.spawn |

Fassen wir mal zusammen:  
Wir haben hier nun die Gruppe "Administrator" und "Spieler".

Der Spieler mit der UUID "bb66bd0c-a8c0-478d-afac-449c44f57da2" aka. Xhadius ist Administrator auf diesem System und hat die Berechtigung "\*" was eine Wildcard ist... sprich er darf alles.

> Das ist nur ein Beispiel, verwende bitte niemals die Berechtigung "\*", sondern gebe die Berechtigungen lieber sehr präzise für den jeweiligen benötigten Bedarf aus!

Die anderen beiden Spieler sind in der Gruppe "Spieler" und dürfen über die vergebenen Berechtigungen den Befehl /msg und /spawn mit dem Plugin Essentials durchführen.

Selbstverständlich sind auch deutlich komplexere Konstruktionen möglich die Beispielsweise untereinander vererben... das würde jedoch den Rahmen dieses Tutorials ein wenig sprengen.

Es geht mir lediglich darum die Mentalität einer relationalen Datenbank zu zeigen.

