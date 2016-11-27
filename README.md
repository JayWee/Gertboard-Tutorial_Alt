# Gertboard Tutorial

1. **[Einleitung](#1)**  
1. **[Inbetriebnahme des Pi](#2)**  
1. **[Erste Programme mit Python](#3)**  
1. **[Gertboard](#4)**  

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
