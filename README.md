# Gertboard Tutorial

1. **[Einleitung](#1)**  
1. **[Inbetriebnahme des Pi](#2)**  
1. **[Erste Programme mit Python](#3)**  
1. **[Gertboard](#4)**
  1. [Einführung](#5)
  1. [Nutzung der Buffer](#6)

## 1. Einleitung <a name="1"> </a>
Der Raspberry Pi ist ein Mini-Computer, der vieles von dem, was ein normaler Computer auch kann: Er hat eine graphische Oberfläche1, einen Internetbrowser und andere Programme. 
Es gibt aktuell drei Versionen des Pi, die Funktionen sind größtenteils gleich. Das neueste Modell hat auch WLAN und Bluetooth an Board.

## 2. Inbetriebnahme des Pi <a name="2"></a>
Der Pi besitzt keine Festplatte oder anderweitige interne Speicher (außer den Arbeitsspeicher natürlich), weshalb wir einen „basteln“ mussten: Das ging ganz einfach mit einer SD-Karte die über mindestens 8GB verfügt.
Als erstes haben wir das Betriebssystem für den Pi herunterladen, welches [hier](https://downloads.raspberrypi.org/raspbian_latest) verfügbar ist: Es heißt Raspbian und ist kostenlos. 
Nun hatten wir eine Zip-Datei, die wir entpacken mussten: Jetzt haben wir anstatt der Zip Datei eine IMG Datei. 
Die SD-Karte haben nun in unseren Computer gesteckt um die IMG-Datei darauf zu installieren. 

### Windows 
Wir haben nun das Program [Win32DiskImager](http://sourceforge.net/projects/win32diskimager/). Wieder erhalten wir eine Zip-Datei die wir entpacken und das Programm ausführen. Mit Hilfe des Programmes haben wir Raspian auf dem Pi installiert. 

### Mac 
Anschließend haben wir es mit einem Mac installiert: Als erstes haben wir sichergestellt, dass die SD-Karte im Format MS-DOS (FAT) formatiert ist:  Dafür nutzten wir das Festplattendienstprogramm. Dort klickt man auf die SD-Karte an der linken Seite: Wichtig ist das man auf die obere klickt, nicht die untere.    
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
***Das Herstellen einer SSH-Verbindung zum Rasperry Pi ist sehr nützlich zum Ausführen von Befehlen. Man kann sich dann das anschließen von Monitor und Tastatur an den Pi sparen und vom eigenem Laptop oder Schulrecher aus den Pi steuern.***

### Verbindung aufbauen

#### Linux, macOS

macOS basiert auf Linux und da Linux einen SSH-Klienten mitbringt, gelten diese Schritte auch für macOS.  

Wir öffnen das Terminal und führen folgenen Befehlen aus:   
ssh pi@ip  

ip ist die Adresse unter der wir den Pi erreichen. Sie finden wir zuhause über den Router und in der Schule mittels  
Wir sind nun auf dem Raspberry Pi eingewehlt und können Befehle und Programme direkt auf dem Pi ausführen. 
Falls wir die Verbindung beenden wollen senden wir entweder den Befehl exit oder schließen das Terminal.

## 3. Erste Programme mit Phyton <a name="3"></a>
Es ist uns nun möglich Programme direkt auf dem Pi zu schreiben in dem wir die Programmiersprache Python benutzen. 
Man kann aber auch auf dem Mac, auf dem wir auch das Terminal ausführen, Programme schreiben.
(Ich empfehle, zum Schreiben von Programmen Xcode zu benutzen, dieses Programm ist kostenfrei im [Mac-AppStore](https://itunes.apple.com/de/app/xcode/id497799835?mt=12) verfügbar. Auch TextWrangler eignet sich, ist aber ein wenig komplizierter. Im folgenen wird sich auf Xcode bezogen. )
![alt text](bild)  
  
### Anlegen eines Dokuments auf dem Pi  
Wir öffnen das Terminal und führen abermals den Befehl ssh pi@ip durch. Nun loggen wir uns mit dem Passwort ein und geben den Befehl nano Test.py ein. Jetzt öffnet sich der Python-Editor, mit dem man die Programme schreiben kann. Jetzt können wir hier den Code eigegben.

### Das erste Programm 
Wir wollen eine LED zum leuchten bringen. Dafür scließen wir eine LED über ein Jumper-Kabel und einen Widerstand am Pi an. Die Pins die wir benutzen sind der Ground-Pin und Pin 18

Als erstes müssen wir verschiedene Dinge importieren: Die Zeit (time), die Steuerung für die Pins (RPi.GPIO) und das Einlesen der Tastatur (curses). Das geschieht mit dem Befehl import.[Befehl].

#### Programme schreiben 
Der Anfang des Programmes sieht dann so aus:  
```
import RPi.GPIO as GPIO  
import time  
```
  
Nun definieren wir die Pins als Ausgang-Pins und den GPIO Modus:
```
GPIO.setmode(GPIO.BCM)  
GPIO.setwarnings(False)  
GPIO.setup(18,GPIO.OUT) #LED  
```

Um die LED zu aktivieren setzen wir den output auf HIGH:
```
GPIO.output(18,GPIO.HIGH)  
time.sleep(5) #wartet fuenf Sekunden  
GPIO.output(18,GPIO.LOW) #schaltet die LED wieder aus  
GPIO.cleanup() #setzt die Steuerung zurueck  
```

Mit crtl-x verlassen wir den Editor: Erst *crtl-x* dann *y* und dann *Enter* drücken. Nun geben wir den Befehl `sudo phyton Test.py` ein um das Programm auszuführen.

Jetzt habe ich eine Abfolge von LED leuchten erstellt:	
```
GPIO.setup(17,GPIO.OUT) #rot  
GPIO.setup(18,GPIO.OUT) #gelb   
GPIO.setup(27,GPIO.OUT) #gruen   
GPIO.setup(22,GPIO.OUT) #rotf  
GPIO.setup(23,GPIO.OUT) #gruenf  
```

Alle als output definiert und dann mittels time.sleep verschiedene Blitzlichter und Morse-Codes erstellt.  
Beispiel SOS:   
```
GPIO.output(18,GPIO.HIGH)  
time.sleep(0.5)  
GPIO.output(18,GPIO.LOW)  
time.sleep(0.5)  
GPIO.output(18,GPIO.HIGH)  
time.sleep(0.5)  
GPIO.output(18,GPIO.LOW)  
time.sleep(0.5)  
GPIO.output(18,GPIO.HIGH)  
time.sleep(0.5)  
GPIO.output(18,GPIO.LOW)  
time.sleep(0.5)  
GPIO.output(18,GPIO.HIGH)  
time.sleep(1)  
GPIO.output(18,GPIO.LOW)  
time.sleep(1)  
GPIO.output(18,GPIO.HIGH)  
time.sleep(1)  
GPIO.output(18,GPIO.LOW)  
time.sleep(1)  
GPIO.output(18,GPIO.HIGH)  
time.sleep(1)  
GPIO.output(18,GPIO.LOW)  
time.sleep(1)  
GPIO.output(18,GPIO.HIGH)  
time.sleep(0.5)  
GPIO.output(18,GPIO.LOW)  
time.sleep(0.5)  
GPIO.output(18,GPIO.HIGH)  
time.sleep(0.5)  
GPIO.output(18,GPIO.LOW)  
time.sleep(0.5)  
GPIO.output(18,GPIO.HIGH)  
time.sleep(0.5)  
GPIO.output(18,GPIO.LOW)  
time.sleep(0.5)  
```

Um daraus eine Schleife zu machen setzt kann man einen Counter einsetzen. Am Anfang des Programmes `count = 0` setzen und dann `while (count < x):` das sieht dann so aus:  
```
count = 0  
while (count < x):
```
darunter dann den Inhalt der Schleife setzen. Diese ist jetzt unendlich. Wenn man ans Ende ein `counter += 1` setzt wird der Counter nach jeden Durchlauf um 1 erhöht und das Programm endet nach x Durchläufen. 

`GPIO.setup(2,GPIO.IN)` definiert Pin 2 als Eingang. Das gegegebn kann man mit der Funktion `if GPIO.input(2) == GPIO.HIGH` und einem Schlater eine Ampel bauen. Das habe ich getan. Mit `print "text"` habe ich die einzelnen Schritte in der Konsole aus beschrieben.
```
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BCM)  
GPIO.setwarnings(False)  
  
GPIO.setup(17,GPIO.OUT) #rot  
GPIO.setup(18,GPIO.OUT) #gelb  
GPIO.setup(27,GPIO.OUT) #gruen  
GPIO.setup(22,GPIO.OUT) #rotf  
GPIO.setup(23,GPIO.OUT) #gruenf  
  
  
rotan = GPIO.output(17,GPIO.HIGH)  
rotaus = GPIO.output(17,GPIO.LOW)  
gelban = GPIO.output(18,GPIO.HIGH)  
gelbaus = GPIO.output(18,GPIO.LOW)  
greenan = GPIO.output(27,GPIO.HIGH)  
greenaus = GPIO.output(27,GPIO.LOW)  
rotfan = GPIO.output (22,GPIO.HIGH)  
rotfaus = GPIO.output (22,GPIO.LOW)  
greenfan = GPIO.output(23,GPIO.HIGH)  
greenfaus = GPIO.output(23,GPIO.LOW)  
  
count = 0  
while (count < 3):  
    GPIO.output (22,GPIO.HIGH)  
    GPIO.output(27,GPIO.HIGH)    
    if GPIO.input(2) == GPIO.HIGH:  
        print "Signal kommt"  
        GPIO.output(27,GPIO.LOW)  
        GPIO.output(18,GPIO.HIGH)  
        time.sleep(2)  
        GPIO.output(18,GPIO.LOW)  
        GPIO.output(17,GPIO.HIGH)  
        time.sleep(1)  
        GPIO.output (22,GPIO.LOW)  
        GPIO.output (23,GPIO.HIGH)  
        print "Bite gehen"  
        time.sleep(5)  
        print "Bitte nicht mehr gehen"  
        GPIO.output (23,GPIO.LOW)  
        GPIO.output (22,GPIO.HIGH)  
        time.sleep(1)  
        counter +=1  
GPIO.cleanup()
```

## 4. Gertboard <a name="4"></a>
![Gertboard Real](https://github.com/JayWee/Gertboard-Tutorial/blob/master/gertboard_real.png)
### Einführung <a name="5"></a>
Das Gertboard von element14 ist ein Erweiterungsboard für alle Versionen des Raspberry Pi. Das Gertboard ist für 26 GPIO-Pins gemacht, passt also perfekt auf die Pins des Raspberry Pi 1 und anderer Modelle des Models A. Bei den B Medelen dagegen sind auf dem Pi 14 Pins mehr, als mit dem Gertboard verbunden werden können.  
Das Gertboard ist mit s. g. Buffern ausgestattet. Diese schützen den Pi bei der benutzung der GPIO-Pins vor Kurzschlüssen. Weiterhin sind auf dem Gertboard noch anschlüsse für eine externe Energiequelle, um Motoren, die eine höhere Spannung brauchen als der Pi liefern kann (3,3V bzw. 5V), mit dem Pi zu betreiben.  

#### Aufbau
![Gertboard Real Blocks](https://github.com/JayWee/Gertboard-Tutorial/blob/master/gertboard_real_blocks.png)
Wie oben in der Graphik zu erkennen ist, ist das Gertboard in sechs Blöcke unterteilt. Diese haben keine Verbindung untereinander.  
Für dieses Tutoral sind nur der schwarze und der rote Block von Relevanz.
Der schwarz umrandete Block umfasst die Verbindung zum Pi (auf der Rückseite) und Pins, die direkt mit den GPIO-Pins auf dem Pi verbunden sind.  
Der rote Block enthält die oben schon erwähnten Buffer, Pins als Ausgänge von den Buffern, Pins zum Einstellen von Input und Output(dies muss im Programm für den Pi selber auch noch mal gemacht werden), 12 LEDs und 3 Druckknöpfe. 
Zusätzlich zu diesen Blöcken gibt es noch die Dauerstrom-Pins (3,3V bzw. 5V).

##### Aufbau der einzelnen Blöcke
Die Platine des Gertboards ist weiß beschriftet. Auf der folgenden Schematik sind nur die Beschriftung und die einzelnen Pins dargestellt:  
![Gertboard Schematisch](https://github.com/JayWee/Gertboard-Tutorial/blob/master/gertboard_shematic.png)  
Blöcke von mehreren Pins sind (Ausgenommen derer in dem Buffer-Block) mit *Jn* (n ist eine natürliche Zahl) beschriftet. Alle Chips auf der Platine sind mit *Un* beschriftet.  
Ganz unten liegt J1. Dies ist die Verbindung zum Pi. Knapp dadrüber liegt J2. Die Pins in diesem Block sind direkt mit den GPIO-Pins des Pi verbunden. 
Weiter wichtig für dieses Tutorial sind die Chips U3-U5. Dies sind die oben genannten Buffer. Ober- und Unterhalb dieser liegen jeweils 8 Pins. Diese sind zur Bestimmung des Modus (Input/Output) gedacht und deshalb mit *out* oder *in* beschrieben. Der Block J3 ist der Eingang zu den Buffern. Die Pins beschriftet mit BUF1-12 sind die Input-Eingänge der Buffer. Zusätzlich zu diesen Input-Pins ist an jeden Buffer-Pin noch eine LED geschaltet und dies ersten drei Buffer Pins (B1-3) sind mit den drei Knöpfen noch verbunden.
Die eben schon erwähnten Dauerstrom-Pins befinden sich in den kleine Böcken J7, J27 und oben links in der Ecke nur 3V3 beschriftet. 

### Nutzung der Buffer <a name="6"></a>

##### Verbindung mit dem Pi
Um das Gertboard mit dem Raspberry Pi zu verbinden, muss das Gertboard auf die linken (Der Pi ist so gedreht, dass die Pins oben links liegen) 26 GPIO-Pins gesteckt werden. Bei B Modelen des Pi sind somit die vierzehn rechten Pins nicht mit dem Gertboard verbunden und auf sie kann somit nicht auf dem Gertboard zugegriffen werden. Damit die Buffer-Ausgänge auch Signale senden können müssen bei J7 (3,3V Dauerstrom) zwei der drei Pins miteinander Verbunden werden (am besten mit einem [Jumper](https://github.com/JayWee/Gertboard-Tutorial/blob/master/Shunt-Jumpers2-1383815114.jpg)).    <!---(Für die, die es interessiert: [Warum hier](#10)) -->  

#### Arbeiten mit LEDs über die Buffer
Um auf die LEDs zuzugreifen muss erstmal eine Verbindung zwischen den GPIO-Pins (J2) und den Buffer-Eingangs-Pins (J3) hergestellt werden. Jetzt sollten alle LEDs rot leuchten.  
Dann muss der Hardware gesagt werden wie welcher Bufferpin genutzt werden soll (Input/Output). Dafür müssen bei einem Output die beiden Pins, die mit *Bx out* (x ist die Nummer des gewählten Buffereingangs) beschriftet sind, am besten mit einem Jumper verbunden werden, bei einem Input mit *Bx in*. Beim aufstecken der Jumper, sollte die entsprechende LED ausgehen. Falls nicht, sollte dies spätestens beim starten des Programms passieren.

#### Arbeiten mit externen Geräten über die Buffer
Wenn mit externen Geräten oder LEDs gearbeitet werden soll, werden nicht beide *Bx out* Pins miteinander verbunden, sondern einer von diesen mit der externen LED. Alle Pins mit dem Senkrecht-Zeichen (umgedrehtes T) oder GND beschriftet sind können als Ground-Pin verwendet werden. Wenn ein Pin als Input genutzt werden soll, wird ein Jumper bei *Bx in* gesetzt und die Input-Quelle mit einem der BUF-Pins. 
