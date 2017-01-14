# 4.3 Das Paket installieren

Wir haben nun den Paketmanager die neusten Pakete gegeben und auch alle vorhandenen Pakete aktualisiert.  
Da wir nun einen MySQL-Server installieren wollen, tun wir dies nun indem wir folgenden Befehl in unserem Terminal ausführen:

```
sudo apt install mysql-server
```

> install befiehlt apt alle nachfolgenden Pakete herunterzuladen und zu installieren  
> mysql-server ist der Name des Paketes, das wir für unseren Einsatzzweck brauchen... praktisch, nicht wahr? :\)

![](/assets/installation-1.png)

Uns wird wieder aufgelistet welche Pakete installiert werden und wir werden erneut gefragt, ob wir das wirklich wollen.  
Da wir uns da ziemlich sicher sind, bestätigen wir auch hier mit einem Y.

> Pro-Tipp: Uns wird die Wahl zwischen \[Y/n\] gegeben.  
> Da Y groß geschrieben ist, heißt dass das es unsere Standardoption ist.  
> Wir können uns also das Y sparen und schlichtweg Enter drücken.

Jetzt wird das ganze ziemlich abenteuerlich, es ändert sich sogar die Farbe unseres Terminals.  
Denn wir werden nun gefragt, ob wir unseren root-Account ein Passwort geben wollen.  
Achtung: Es wird nicht nach dem root-Account vom Betriebssystem gefragt, sondern nach einem neuen einmaligen Passwort für den Administrator-Account eurer MySQL-Datenbank!

![](/assets/installation-2.png)

