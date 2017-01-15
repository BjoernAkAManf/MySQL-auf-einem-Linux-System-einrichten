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

![](/assets/connect-windows-5.png)

Haben wir das alles gemacht können wir nun auf die Schaltfläche "Test Connection" drücken und werden nun auch hier wieder nach dem Fingerprint \([siehe Kapitel 4.1](/mit-dem-server-verbinden.md)\) gefragt.

![](/assets/connect-windows-6.png)

Da wir dem Server vertrauen, drücken wir nun auf Continue und bekommen nun die Bestätigung, dass die Verbindung hergestellt werden kann.

> Lasst euch nicht von dem "SSL: not enabled" nicht verunsichert.  
> Wir verwenden in diesem Tutorial eben nicht die von MySQL mitgelieferte SSL-Funktionalität, da hierfür die Anwendungen umgeschrieben werden müssten um sich korrekt zu authentifizieren.  
> Stattdessen packen wir wie im [vorherigen Kapitel](/auf-einem-anderen-server.md) beschrieben unsere Pakete mit dem verschlüsselten SSH-Protokol ein und erhalten somit eine äquivalente Sicherheit!

![](/assets/connect-windows-7.png)

Jetzt bestätigen wir unsere Einstellungen indem wir das Bestätigungsfenster und das Setupfenster mit einem Druck auf den "OK"-Button schließen und landen wieder auf der Hauptseite von der MySQL Workbench... nur mit dem unterschied, dass unsere konfigurierte MySQL-Datenbank nun auf der Startseite zu erreichen ist.

![](/assets/connect-windows-8.png)

Wir klicken nun einmal auf unsere neue Schaltfläche und werden direkt verbunden.

![](/assets/connect-windows-9.png)

Unten links bei "SCHEMAS" sehen wir nun unsere Datenbank "wordpress", die wir ja damals in [Kapitel 6](/neue-datenbank-erstellen.md) erstellt haben.  
Klicken wir nun auf den dezenten Pfeil links daneben, so klappt sich eine Übersicht aus verschiedenen Elementen einer MySQL-Datenbank aus.

![](/assets/connect-windows-10.png)

Da wir uns in diesem Tutorial nur für die Tabellen interessieren, klicken wir nun auf den Pfeil links neben "Tables" und klappen diese Übersicht auf.

Wir werden begrüßt von allen Tabellen, die WordPress in seiner Standard-Installation erstellt.

> Nur zur Erinnerung: Das ist normalerweise nicht der Fall, nur habe ich wie schon oben in einer Anmerkung bereits erwähnt Wordpress auf dem Server installiert um ein praktisches Beispiel zu haben.

![](/assets/connect-windows-11.png)

Beim Mouseover über jede der Tabellen sieht man ganz rechts drei kleine Symbole: Ein "i" , ein Schraubenschlüssel und eine Tabelle.  
Da wir uns nun zum Beispiel den Inhalt von der Tabelle "wp\_comments" anschauen wollen, klicke ich nun auf die Tabelle und es öffnet sich ein neuer Tab.

> Tipp: MySQL Workbench ist ein Programm, bei dem ich defintiiv empfehlen würde den Vollbild-Modus zu aktivieren und möglicherweise einige Elemente vom UI zu verschieben.
>
> Oben rechts klicke ich gerne auf die Schaltfläche mit dem blauen Rechteck auf der rechten Seite, da dieses das Modul "SQLAdditions" ausblendet.

Interessanterweise wird uns oben der durchgeführte SQL-Query angezeigt während wir unten noch eine Übersicht über die ersten tausend Zeilen des Ergebnisses erhalten.

Dieses Limit kann man auch problemlos in der Menüleiste vom SQL-Fenster erhöhen oder sogar ganz deaktivieren.  
Und natürlich kann man hier auch die Einträge der Tabelle verändern \(ALTER\), löschen \(DROP\) oder neue Einträge \(CREATE\) hinzufügen.  
Und natürlich kann man hier auch Tabellen verändern, löschen oder neue Tabellen hinzufügen.  
Und natürlich kann man auch... naja, alles machen, was man mit phpMyAdmin auch kann.

Nur eben mit einem entscheidenden Unterschied: Wir sabotieren nicht unsere eigene Sicherheit!

---

Herzlichen Glückwunsch!  
Wenn du ebenfalls Erfolg hattest würde ich mich sehr über Feedback zu meinem Guideline freuen.

Und falls du nun so viel Stress hattest und erstmal eine Pause brauchst, kannst du auch gerne bei mir auf meinem [Let's Play Kanal](https://www.youtube.com/Xhadius) vorbeischauen.

## Links

Vorheriger Kapitel: [Auf einem anderen Server](/auf-einem-anderen-server.md)

