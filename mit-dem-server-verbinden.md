## 4.1 Mit dem Server verbinden

Je nach Hoster und bestehender Serverkonfiguration sieht das für euch unterschiedlich aus.  
Ich für meinen Teil nutze wie erwähnt DigitalOcean und PuTTY.

Die IP meines Droplets lautet 207.154.206.43, der Nutzername ist hier Standardmäßig root und das Passwort... ist für euch in diesem Fall ziemlich irrelevant :\)

Also gut, geben wir mal bei PuTTY die IP ein, drücken unten auf "Open" und sehen mal was passiert.

![](/assets/putty-login-1.png)

Beim ersten Verbinden werdet ihr von eurem SSH-Client gefragt, ob ihr dem Fingerprint des Servers vertraut.  
Manche Hoster senden euch bei der Konfiguration des Servers den richtigen Fingerprint, damit ihr identifizieren könnt, ob ihr euch mit dem richtigen Server verbindet.

Ihr wollt drauf und euch den Server merken? Dann wählt ihr nun "Ja".

![](/assets/putty-login-2.png)

Weiter geht es, indem ihr nun ein schwarzes Fenster \(das sogenannte Terminal\) angezeigt bekommt, welches von euch verlangt dass ihr euch authentifiziert.  
Es fragt zunächst den Benutzernamen ab, in meinem Fall ist es root.  
Tippt euren Nutzernamen ein und bestätigt mit der Eingabetaste.

![](/assets/putty-login-3.png)

Je nachdem ob und wie ihr [Public-Key-Authentifizierung](https://de.wikipedia.org/wiki/Public-Key-Authentifizierung "Hier ist ein kleiner Wikipedia-Artikel zur Grundidee von PKA.") verwendet müsstet ihr davor noch eine andere Datei in PuTTY verlinken und euch dann noch mit einem Kennwort authentifizieren.  
Da ich nur die Standardeinstellungen meines Droplets verwende, habe ich nun einfach noch ein root-Kennwort einzugeben.

> Protip: Ihr könnt euch in Windows alles rauskopieren und es mit einem Rechtsklick in PuTTY einfügen.

Erschreckt euch übrigens nicht, wenn ihr bei der Kennwort-Eingabe keine Zeichen seht.  
Das ist bei auf Linux basierenden Systemen standardmäßig so konfiguriert, um zu verhindern dass man eure Passwörter erraten kann... auch die Länge der Kennwörter kann somit nicht durch das Zählen von Sternchen oder ähnlichem erraten werden :\)

![](/assets/putty-login-4.png)

Nachdem ihr das geschafft habt, seid ihr endlich drin!  
Die verschlüsselte Verbindung zu eurem Server existiert nun und wir können nun alle möglichen Befehle auf unserem Server durchführen.

![](/assets/putty-login-5.png)

## Links:

* Vorheriger Kapitel: [MySQL installieren](/mysql-installieren.md)
* Nächster Kapitel: Mit dem Server verbinden



