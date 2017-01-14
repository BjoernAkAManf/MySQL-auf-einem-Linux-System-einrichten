# 4.2 Den Server updaten

So, ihr seid nun im Server drin.  
Doch bevor ihr loslegt, solltet ihr die Pakete mal auf den neusten Stand bringen.

Wir geben also in unserem Terminal den folgenden Befehl ein:

```
sudo apt update
```

> sudo bedeutet "Superuser do" und sorgt dafür, dass der nachfolgende Befehl als Administrator ausgeführt wird.  
> apt ist der Paketmanager "Advanced Packaging Tool" dem wir den Befehl geben.  
> update ist der auszuführende Befehl, mit dem nun die Paketquellen neu eingelesen werden.

Jetzt warten wir mal ein wenig ab, bis dieser Vorgang abgeschlossen ist.  
Das ist meistens innerhalb von weniger als 10 Sekunden erledigt.

![](/assets/update-1.png)

Weiter geht es mit

```
sudo apt upgrade
```

> upgrade befiehlt apt nun alle auf dem Server befindlichen Pakete auf den neusten Stand zu bringen.

![](/assets/update-2.png)

Nun werden euch die Pakete genannt die aktualisiert werden.  
Ihr werdet nun also gefragt, ob ihr nun fortfahren möchtet oder nicht.

Wir wollen alles auf den neusten Stand bringen, also geben wir "Y" ein und bestätigen mit der Eingabetaste.  
Hiernach werden alle verfügbaren Updates installiert und wir müssen je nach Hardware und Anbindung des Servers einige Sekunden bis Minuten abwarten.

Sobald alles erledigt sind wandern wir automatisch zurück in das Terminal.

![](/assets/update-3.png)

## Links:

* Vorheriger Kapitel: [Mit dem Server verbinden](/mit-dem-server-verbinden.md)
* Nächster Kapitel: [Das Paket installieren](/das-paket-installieren.md)
* [Inhaltsverzeichnis](/SUMMARY.md)
* Sonstiges:
  * [Informationen zu sudo](https://wiki.ubuntuusers.de/sudo/)
  * [Informationen zu apt](https://wiki.ubuntuusers.de/apt/apt/)



