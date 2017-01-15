# 7.2 Auf einem anderen Server

## Vorwort

Wenn ihr eure Datenbank auf einem anderen Server haben möchtet \(z.B. weil ihr mehrere Anwendungsserver habt, die auf die selbe Datenbank zugreifen\), dann müsst ihr euch etwas anderes einfallen lassen.

Wir haben die MySQL-Instanz nach außen hin abgeschottet, spricht es geht weder was raus, noch was rein.  
Und bevor ihr euch nun überlegt das Rückgängig zu machen, solltet ihr mal genau drüber nachdenken was das bedeuten würde.

MySQL verwendet [TCP/IP](https://tools.ietf.org/html/rfc793) als Standardprotokoll... nur leider ist TCP/IP völlig unverschlüsselt.  
Das kann man dem Protokoll auch nicht übel nehmen, immerhin ist sein [RFC ](https://de.wikipedia.org/wiki/Request_for_Comments)schon fast 35 Jahre \(!!!\) alt.

Jeder Hacker kann nun über die Leitung eigene Anfragen senden und/oder deine Anfragen abhören.

Wenn du dich nun fragen solltest, warum wir ganz entspannt über PuTTY Anfragen und Passwörter gesendet haben, dann hast du schonmal auf dem richtigen Gedanken.  
Den PuTTY ist wie Anfangs im Tutorial erwähnt ein [SSH](https://tools.ietf.org/html/rfc4253)-Client mit dem man eben eine SSH-Verbindung zum Server aufbaut.

SSH ist kurz für Secure Shell, was wie der Zufall so will verschlüsselt ist.

Und wenn du dich jetzt fragst, ob wir vielleicht SSH mit MySQL koppeln können, dann hast du 100/100 Punkten erreicht!  
Dieses Verfahren nennt sich [SSH-Tunneling](https://de.wikipedia.org/wiki/Tunnel_(Rechnernetz)\) und kapselt die TCP/IP-Pakete in einer SSH-Verbindung.

## Umsetzung

> Für mein Beispiel habe ich mir nun einen zweiten Droplet auf DigitalOcean erstellt.  
> Über diesen versuche ich meine Anfragen zur MySQL-Instanz zu tunneln.

Wenn wir auf unserer Tunnel-Instanz nun versuchen auf eine lokale Datenbank zuzugreifen, bemerken wir, dass das schlichtweg nicht geht.

![](/assets/connect-extern-1.png)

Gut, das liegt daran, dass wir auf dieser Instanz keinen MySQL-Client installiert haben.  
Dieser MySQL-Client ist hier nur für Demonstrationszwecke notwendig, da wir den nur brauchen um hiermit MySQL Befehle in unserem Terminal durchführen zu können.

Deshalb installiere ich nun für mich das Paket MySQL-Client durch folgenden Befehl:

```
sudo apt install mysql-client
```

Nachdem das Paket nun vollständig installiert ist, können wir das ganze nochmal versuchen.

![](/assets/connect-extern-2.png)

Okay, wir werden sogar nach dem Passwort gefragt, es sieht gut au...

![](/assets/connect-extern-3.png)

... oder auch nicht.

Warum? Ganz einfach: Wir haben noch keinen Tunnel und haben lediglich den MySQL-Client auf dem Server, der nun einfach versucht auf einen lokalen, nicht existierenden MySQL-Server zuzugreifen.

Also gut, was genau wollen wir erreichen.  
Wir möchten eine SSH-Verbindung zum MySQL-Server über die einfach nur die MySQL-Datenbank erreicht werden kann.  
Diese soll im Hintergrund stattfinden, diese soll möglichst nichts in der Konsole ausgeben und das wichtigste: Sie soll keine Befehle akzeptieren.

Das alles lässt sich mit folgendem Befehl zusammenfassen:

```
ssh -f ssh-nutzername@externe-ip-von-mysql-instanz -L 3306:127.0.0.1:3306 -N
```

> Woah, ruhig mit den jungen Pferden.  
> Erstmal wird der Befehl hier auseinander genommen!
>
> ssh ist der SSH-Client über den wir den Tunnel starten.  
> -f verlangt, dass SSH in den Hintergrund wandert.  
> ssh-nutzername@externe-ip-von-mysql-instanz sind eben die Zugangsdaten.  
> -L bindet den lokalen Port bei dem angegebenen Host an den hinten stehenden Port.  
> 3306:127.0.0.1:3306 ist die von uns gewünschte Konfiguration, da 3306 der Standardport von MySQL ist.  
> -N ist notwendig für Tunneling, da ssh normalerweise davon ausgeht, dass am Ende noch ein auszuführender Befehl kommt.

![](/assets/connect-extern-4.png)

> Auch hier nochmal der Hinweis: Verwendet niemals, unter gar keinen Umständen den SSH-root.  
> Ich darf das in diesem Fall, da das hier nur ein kleines Tutorial ist, bei dem ich die Instanzen im Nachhinein ohnehin wieder lösche!
>
> Ich empfehle es hierfür einen eigenen SSH-Account zu erstellen und den auch entsprechen zu benennen.

Wir werden nun gefragt, ob wir dem Fingerprint des Servers vertrauen.  
Was es mit diesem Fingerprint auf sich hat, habe ich bereits in [Kapitel 4.1](/mit-dem-server-verbinden.md) erläutert.

![](/assets/connect-extern-5.png)

Ist das erledigt wird der Fingerabdruck permanent auf dem Server gespeichert.  
Als nächstes wird noch das SSH-Passwort vom entfernten Server abgefragt, was wir nun auch eingeben.

![](/assets/connect-extern-6.png)

Fertig. Das wars.  
Der Tunnel steht und läuft nun im Hintergrund.

Jeder Traffic über den Port 3306 wird nun automatisch an die MySQL-Instanz weitergeleitet!

Also gut, probieren wir es aus! :\)

![](/assets/connect-extern-7.png)

Wir geben also unseren Befehl ein...

![](/assets/connect-extern-8.png)

... authentifizieren uns mit unserem Passwort...

![](/assets/connect-extern-9.png)

... und erleben die größte Enttäuschung seit der Erfindung des [Bibi-Phones](https://youtu.be/wNmEAaPndLo)!

Packt die Mistgabeln wieder ein, denn die Erklärung ist ziemlich simpel: Standardmäßig versucht MySQL sich nicht übers Loopback-Interface mit einem MySQL-Server zu verbinden, sondern hat einen eigenen Socket... da hier aber lokal keine MySQL-Instanz läuft, müssen wir den MySQL-Client dazu anweisen sich mit 127.0.0.1 zu verbinden.

Um den Host festzulegen erweitert ihr den Befehl durch folgenden Parameter:

```
-h 127.0.0.1
```

![](/assets/connect-extern-10.png)

Uuuuuuuund...

![](/assets/connect-extern-11.png)

Tadaaaa! Wir haben es geschafft! :\)

> In der Praxis macht das ohnehin keinen Unterschied, da mir keine Anwendung bekannt ist, in der man nicht selbst den DB-Host angeben muss.
>
> Jedoch war es nötig für dieses Tutorial.

Herzlichen Glückwunsch!  
Wenn du ebenfalls Erfolg hattest würde ich mich sehr über Feedback zu meinem Guideline freuen.

Und falls du nun so viel Stress hattest und erstmal eine Pause brauchst, kannst du auch gerne bei mir auf meinem [Let's Play Kanal](https://www.youtube.com/Xhadius) vorbeischauen.

## Links:

* Vorheriger Kapitel: [Auf dem selben Server](/auf-dem-selben-server.md)

Uuuuuuuund...

![](/assets/connect-extern-11.png)

Tadaaaa! Wir haben es geschafft! :\)

> In der Praxis macht das ohnehin keinen Unterschied, da mir keine Anwendung bekannt ist, in der man nicht selbst den DB-Host angeben muss.
>
> Jedoch war es nötig für dieses Tutorial.

Herzlichen Glückwunsch!  
Wenn du ebenfalls Erfolg hattest würde ich mich sehr über Feedback zu meinem Guideline freuen.

Und falls du nun so viel Stress hattest und erstmal eine Pause brauchst, kannst du auch gerne bei mir auf meinem [Let's Play Kanal](https://www.youtube.com/Xhadius) vorbeischauen.

## Links:

* Vorheriger Kapitel: [Auf dem selben Server](/auf-dem-selben-server.md)



