# Gertboard Tutorial

[Einleitung](#1)
[Inbetriebnahme des Pi](#2)
[Erste Programme mit Python](#3)
[Gertboard](#4)

## 1. Einleitung
Der Raspberry Pi ist ein Mini-Computer, der vieles von dem, was ein normaler Computer auch kann: Er hat eine graphische Oberfläche1, einen Internetbrowser und andere Programme. 
Es gibt aktuell drei Versionen des Pi, die Funktionen sind größtenteils gleich. Das neueste Modell hat auch WLAN und Bluetooth an Board.

## 2. Inbetriebnahme des Pi
Der Pi besitzt keine Festplatte oder anderweitige interne Speicher (außer den Arbeitsspeicher natürlich), weshalb wir einen „basteln“ mussten: Das ging ganz einfach mit einer SD-Karte die über mindestens 8GB verfügt.
Als erstes haben wir das Betriebssystem für den Pi herunterladen, welches [hier](https://downloads.raspberrypi.org/raspbian_latest) verfügbar ist: Es heißt Raspbian und ist kostenlos. 
Nun hatten wir eine Zip-Datei, die wir entpacken mussten: Jetzt haben wir anstatt der Zip Datei eine IMG Datei. 
Die SD-Karte haben nun in unseren Computer gesteckt um die IMG-Datei darauf zu installieren. 

### Windows 
Wir haben nun das Program [Win32DiskImager](http://sourceforge.net/projects/win32diskimager/). Wieder erhalten wir eine Zip-Datei die wir entpacken und das Programm ausführen. Mit Hilfe des Programmes haben wir Raspian auf dem Pi installiert. 

### Mac 
Anschließend haben wir es mit einem Mac installiert: Als erstes haben wir sichergestellt, dass die SD-Karte im Format MS-DOS (FAT) formatiert ist:  Dafür nutzten wir das Festplattendienstprogramm. Dort klickt man auf die SD-Karte an der linken Seite: Wichtig ist das man auf die obere klickt, nicht die untere.  ![alt text](bild)  
Jetzt wählt man aus der oberen Leiste Löschen aus und dann einen Namen (Ohne Titel), das Format (MS-DOS-Dateisytem (FAT)), und das Schema (GUID). Nun klickt man auf Löschen. 
Jetzt merken wir uns die Zahl die unten rechts im Feld Gerät steht diskx.
Anschließend öffnen wir das Terminal (Programme -> Terminal) und geben den Befehl: sudo dd bs=1m if=path_of_your_image.img of=/dev/rdiskx ein.
Statt path_of_your_image.img geben wir den Pfad der IMG Datei ein. Diesen können wir aus dem Finder kopiert. Dafür wählen wir die IMG-Datei aus und rechts-klicken auf die Datei und wählen Informationen aus. Für x setzen wir die Zahl aus dem Festpalttendienstprogramm ein und führen den Befehl aus. 
Schlägt der Befehl fehl, kann man statt rdisk auch nur disk verwenden.
Ist der Befehl ausgeführt, kann die SD-Karte ausgeworfen werden und wir stecken sie in den Pi. 

## Der erste Start
Dann  haben wir die SD-Karte, auf der das Raspbian installiert ist, in den Pi gesteckt und  über ein Micro-USB-Kabel mit Strom versorgt. 
Nun beginnt der Pi den Startvorgang. In der Zeit können wir ein LAN-Kabel zur Versorgung mit Internet anschließen. (die Pis der Schule müssen nur angeschlossen werden, sie haben schon Internet. Eigene Pi's müssen erst registriert werden.

### Zugriff auf den Pi 
Der Pi ist nach etwa 2 Minuten bereit um mit ihm zu arbeiten und auf ihn zuzugreifen. Das machen wir mittels SSH:
___Das Herstellen einer SSH-Verbindung zum Rasperry Pi ist sehr nützlich zum Ausführen von Befehlen. Man kann sich dann das anschließen von Monitor und Tastatur an den Pi sparen und vom eigenem Laptop oder Schulrecher aus den Pi steuern.

### Verbindung aufbauen

#### Linux, macOS

macOS basiert auf Linux und da Linux einen SSH-Klienten mitbringt, gelten diese Schritte auch für macOS.  

Wir öffnen das Terminal und führen folgenen Befehlen aus:   

ssh pi@ip  
ip ist die Adresse unter der wir den Pi erreichen. Sie finden wir zuhause über den Router und in der Schule mittels  
Wir sind nun auf dem Raspberry Pi eingewehlt und können Befehle und Programme direkt auf dem Pi ausführen. 
Falls wir die Verbindung beenden wollen senden wir entweder den Befehl exit oder schließen das Terminal.
