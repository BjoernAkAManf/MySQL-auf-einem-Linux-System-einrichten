# 5.3 mysqld.cnf

Früher waren die Standard-Einstellungen von MySQL ziemlich unangenehm und mussten ziemlich stark modifiziert werden, damit man die Datenbank überhaupt "sicher" verwenden kann.

Mittlerweile hat sich da ziemlich viel verändert, da die Datenbank zum Beispiel standardmäßig nur lokal zu erreichen ist.

[Jedoch erlaubt unsere Datenbank aktuell noch den Zugriff auf das lokale Dateisystem, was meistens nicht benötigt wird aber z.B. bei einer SQL-Injection ziemlich fatale Folgen haben kann.](https://blog.tarq.io/insecure-defaults-exploiting-load-data-local-infile/)

Wir werden also die Konfiguration von MySQL ein wenig anpassen müssen, indem wir die Datei _/etc/mysql/mysql.conf.d/mysqld.cnf_ ein wenig verändern.

Normalerweise würde ich hierfür den Texteditor [vim](https://wiki.ubuntuusers.de/VIM/) benutzen, da sich dieses Tutorial jedoch an Anfänger richtet und ich nicht erst [eine Stunde lang erklären muss wie man aus vim entkommt](https://twitter.com/iamdevloper/status/435555976687923200?lang=de).

Deshalb nutzen wir hierfür das einsteigerfreundliche [Nano](https://wiki.ubuntuusers.de/Nano/).

Also gut, fangen wir mal im Terminal an, indem wir mit nano die genannte Datei öffnen.

```
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

![](/assets/sql-config-1.png)

Wir scrollen nun mit unseren Pfeiltasten bis hinter das letzte Zeichen von der Zeile

```
bind-address            = 127.0.0.1
```

![](/assets/sql-config-2.png)

und fügen nun nach einer neuen Zeile folgenden Text ein:

```
local-infile            = 0
```

> local-infile ist die Option, die es erlaubt in unserem Dateisystem zu arbeiten.  
> Die 0 steht für false, also deaktivieren wir mit dieser Zeile die Funktion das Dateisystem über die Datenbank anzurühren.
>
> Die Anzahl der Leerzeichen ist hier irrelevant, jedoch versuche ich das hier schön zu formatieren, so dass man die Einstellung wieder schnell findet.

![](/assets/sql-config-3.png)

Zum Schluss wollen wir natürlich unsere Änderungen speichern und Nano beenden.

Um den Texteditor zu schließen, müssen wir zunächst einmal Strg + X betätigen.

![](/assets/sql-config-4.png)

Hiernach werden wir gefragt, ob wir unsere Änderungen speichern möchten.  
Das dies der Fall ist, geben wir direkt ein Y ein.

![](/assets/sql-config-5.png)

Zum Schluss müssen wir den Dateinamen festlegen.  
Da wir die geöffnete Datei überschreiben wollen bestätigen wir dies einfach über die Eingabetaste.

Ihr landet wieder im Terminal, in dem ihr nur noch den folgenden Befehl ausführen solltet:

```
sudo service mysql restart
```



