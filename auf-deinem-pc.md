# 7.3 Auf deinem PC

## Vorwort

Du möchtest deine Datenbank nun überprüfen, hast aber keine Lust im Terminal nun über SQL-Queries deine Datenbank auszulesen?  
Verständlich, denn das ist natürlich möglich, aber ziemlich unbequem.

Und bevor du auch nur einen Schritt wagst dir sowas wie [phpMyAdmin ](https://www.phpmyadmin.net/)auf deinen Server zu installieren \(was aus irgendeinem Grund von sehr vielen Tutorials vorgeschlagen wird\), möchte ich auch hier wieder dass wir eine Sekunde darüber nachdenken was das bedeuten würde.

Wir haben uns nun unser Datenbanksystem so abgesichert, dass man nur über SSH hinein kommt und haben somit mehrere Faktoren, die unseren Server abriegeln.

Nun wollen wir all das wegwerfen indem wir ein öffentliches Webinterface eröffnen, für das man schlussendlich nur noch das SQL-Passwort braucht?  
Wir wollen erreichen dass wir einen weiteren Point of Failure haben, der bei einer möglicherweise noch unbekannten Sicherheitslücke von PHP oder eben phpMyAdmin die gesamte Sicherheit zunichte macht?

Nein, das sollen wir definitiv nicht, denn hierfür gibt es auch deutlich bessere Lösungen!  
Was ist wenn wir uns einfach einen MySQL-Client \(mit einer Nutzeroberfläche\) auf den Desktop laden und von dort aus nun die Schritte von dem vorherigen Kapitel ein wenig modifiziert anwenden...?

Genau: Wir sabotieren hiermit **nicht **unsere eigene Sicherheit und verlieren **keinerlei **Komfort!

## Umsetzung

Wie es bereits klar sein sollte, verwende ich für mein Tutorial auf meinem Client Windows 10.  
Ich lade mir als MySQL-Client nun [MySQL Workbench](https://www.mysql.de/products/workbench/) runter.  
Hierfür gibt es selbstverständlich auch kostenfreie Alternativen wie zum Beispiel [DBeaver](http://dbeaver.jkiss.org/), jedoch habe ich mir vorgenommen für dieses Tutorial nur offizielle Software zu verwenden.

> An dieser Stelle noch eine kleine Anmerkung: Ich habe mir für dieses Tutorial einen neuen MySQL-Server erstellt auf dem ich bereits nach der Methode von Kapitel 7.1 eine WordPress-Installation durchgeführt habe.
>
> Deshalb wird sich die IP-Adresse und der Fingerprint von dem bisherigen Server unterscheiden.

![](/assets/connect-windows-1.png)

Die Installationsschritte spare ich mir für dieses Tutorial mal, stattdessen starte ich nun die Workbench.  
Wir werden nun von einem recht dunkel gehaltenen GUI begrüßt.

> Normalerweise sind in den Feldern "MySQL-Connections" und "Models" bereits Beispiels-Konfigurationen hinterlegt, die habe ich bei mir jedoch bereits entfernt.

Um nun unseren Server als Shortcut hinzuzufügen klicken wir nun auf das eingerahmte Plus rechts neben "MySQL Connections"

![](/assets/connect-windows-2.png).

Es öffnet sich dieses Fensterchen, in dem wir nun gefragt werden unsere Daten zur Datenbank einzugeben.  
Sollte bei dir die Alarmglocke schrillen, dass wir keine direkte Datenbankverbindung aufbauen dürfen, dann hast du sehr gut aufgepasst.

![](/assets/connect-windows-3.png)

Glücklicherweise bietet MySQL Workbench nativ die Möglichkeit des SSH-Tunneling an.  
Wir gehen dafür auf das Dropdown "Connection Method" und wählen dort dann entsprechend den Menüpunkt "Standard \(TCP/IP\) over SSH" wodurch sich im Reiter "Paramters" nun die Eingabeflächen verändern.

![](/assets/connect-windows-4.png)

Wir geben oben bei Connection Name einen Namen für unseren Shortcut ein.  
Am besten sollte dieser möglichst einprägsam sein :\)

Bei SSH Hostname gebt ihr nun die IP eures SSH-Servers an und schreibt dahinter ":PORT".

> Der Standardport lautet 22, welchen ich für dieses Tutorial auch so gelassen habe.

Als nächstes kommt der SSH Username.

> Ich habe es zwar schonmal erwähnt, mache es an dieser Stelle aber trotzdem nochmal: Um Himmels Willen, verwendet für einen SSH Tunnel \(und auch generell wo es zu vermeiden geht\) den root-Account.  
> Da es sich hierbei um ein Tutorial handelt, bei dem ich einen "Einweg-Server" verwende der danach wieder gelöscht wird mache ich das um mir bei der Konfiguration ein wenig Zeit zu sparen.
>
> Sowas ist in einem Produktivsystem suizid und sollte um jeden Preis vermieden werden!

Und eben unser SSH Passwort \(welches man über "Store in Vault ..." eingibt\).

> Interessanterweise bietet sich Workbench auch das [Public-Key-Authentifizierungsverfahren](https://de.wikipedia.org/wiki/Public-Key-Authentifizierung) durch die Option "SSH Key File" an, jedoch ist das für unser Beispiel vollends irrelevant.
>
> Darauf werde ich in einem anderen Buch eingehen, bei dem es um die generelle Absicherung eines Linux-Servers geht!

Zum Schluss kommen noch MySQL Hostname und Port die jeweils bei den Standardeinstellungen bleiben sollten \(da wir ja übers Tunneling direkt auf den Server zugreifen, auf dem die MySQL Instanz läuft\).

Dazu müssen wir noch den Username und das Passwort des gewünschten MySQL-Accounts eingeben.

Haben wir das alles gemacht können wir nun auf die Schaltfläche "Test Connection" drücken und

---

Herzlichen Glückwunsch!  
Wenn du ebenfalls Erfolg hattest würde ich mich sehr über Feedback zu meinem Guideline freuen.

Und falls du nun so viel Stress hattest und erstmal eine Pause brauchst, kannst du auch gerne bei mir auf meinem [Let's Play Kanal](https://www.youtube.com/Xhadius) vorbeischauen.

## Links

Vorheriger Kapitel: [Auf einem anderen Server](/auf-einem-anderen-server.md)

