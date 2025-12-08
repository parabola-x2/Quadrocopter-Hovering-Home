# README Database

#### Repository **:** [https://github.com/parabola-x2/Quadrocopter\_Database](https://github.com/parabola-x2/Quadrocopter_Database)

<figure><img src=".gitbook/assets/DB-foto.png" alt="" width="375"><figcaption></figcaption></figure>

Quadrocopter Raspberry Pi 2016 Datenbank mit PythonMySQL\
Universität Tübingen\
Author: Jascha Petter\
Dienstag 20.08.16

Vorwort\
Als Student der Universität Tübingen, in einem der Informatikstudiengänge, ist die Teilnahme an einem Programmierprojekt vorgesehen. Aus den vielen angebotenen Projekten habe ich mich für das Projekt „PiSense mit Quadrocopter“ entschieden. In diesem Projekt waren die Anpassung der Low Level Treiber, das Darstellen der Sensordaten in einer GUI, eine App zum steuern der Motoren des Quadrocopters, sowie die gemessen Daten in einer Datenbank abzulegen als Ziele gegeben. Die folgende Dokumentation soll das erstellen und Verwalten einer Datenbank, sowie das Empfangen der Daten per UPD beschreiben.

Inhaltsverzeichnis\
1.1 MySQL\
1.2 Datenbank\
1.3 Python\
2 Anwendung 4 2.1 Struktur der Datenbank\
2.2 Auszug aus der Datenbank\
2.3 Python\
2.3.1 Verbindung zur Datenbank\
2.3.2 UDP Socket\
2.3.3 Empfangen und aufteilen der Daten\
2.3.4 Ablegen der Daten\
2.3.5 Ausführen des Skriptes\
2.4 Verwalten der Datenbank\
2.4.1 Adminer einrichten\
2.4.2 Adminer bedienen\
3 Zukünftige Arbeit&#x20;

Abbildungsverzeichnis

1.1 Passwort Alert\
2.1 Struktur der Datenbank\
2.2 Daten der Demo\
2.3 Connector\
2.4 UDP Socket\
2.5 Empfange der Message\
2.6 Trennen der Daten\
2.7 Query\
2.8 Anmelden in Adminer\
2.9 Adminer Übersicht\
2.10 SQL-Kommando\
2.11 Importieren einer Tabelle\
<br>

1.1 MySQL

Um auf Ihrem System einen MySQL Server laufen zu lassen, benötigen Sie den „MySQL Community Server“ Laden Sie sich hierzu den MySQL Community Server von der MySQL Homepage herunter. http://dev.mysql.com/downloads/mysql/1 Wählen Sie dort die dementsprechende Version für Ihr System. Sie müssen sich für den Download nicht anmelden, oder ein Konto erstellen. Klicken Sie einfach auf „No thanks, just start my download“ Nach der Installation wir Ihnen das Passwort für den Root User angezeigt. Abbildung 1.1: Passwort Alert Notieren Sie sich dieses, da es später noch gebraucht wird! 3. Öffen sie nun Ihren Terminal und geben folgende Befehle ein, um ein neues Passwort zu vergeben: $ cd /usr/local/mysql/bin $ ./mysqladmin -u root -p password ’’ Sie werden nun aufgefordert Ihr Root-Passwort, welches Sie vorhin notiert haben, einzugeben. $ exit Um zurückzukehren



Nun erstellen wir einen neuen Benutzer und geben diesem die notwendigen Rechte. $ ./mysql -u root -p mysql > CREATE USER ’PiSense’@’%’ IDENTIFIED BY ’somePW’; mysql > GRANT ALL PRIVILEGES ON _._ TO ’PiSense’@’%’; Dies ist nun der neue Benutzer, mit dem gearbeitet wird Nun muss noch der MySQL-Server gestartet werden. Dies ist wie folgt möglich. $ cd /usr/local/mysql/support-files/ $ sudo ./mysql.server start 1.2 Datenbank Da wir nun einen Benutzer zum arbeiten habe, fehlt nur noch die Datenbank und eine Tabelle Zu erst muss ein neues Schema erstellt werden: $ cd /usr/local/mysql/bin $ ./mysql -u PiSense -p mysql > CREATE DATABASE ‘SenseData‘ COLLATE ’latin1\_swedish\_ci’; 2. Nun können Sie eine Tabelle anlegen: mysql > CREATE TABLE ‘SenseData‘.‘DATA‘ ( ‘PITIME‘ timestamp(2) PRIMARY KEY NOT NULL, ‘ACC\_X‘ double NOT NULL, ‘ACC\_Y‘ double NOT NULL, ‘ACC\_Z‘ double NOT NULL, ‘MAG\_X‘ double NOT NULL, ‘MAG\_Y‘ double NOT NULL, ‘MAG\_Z‘ double NOT NULL, ‘G\_ROLL‘ double NOT NULL, ‘G\_PITCH‘ double NOT NULL, ‘G\_YAW‘ double NOT NULL, ‘TEMP‘ double NOT NULL, ‘PRESS‘ double NOT NULL, ‘M1‘ double NOT NULL, ‘M2‘ double NOT NULL, ‘M3‘ double NOT NULL, ‘M4‘ double NOT NULL ) ENGINE=’InnoDB’ COLLATE ’latin1\_swedish\_ci’; Zu den jeweiligen Einträgen später mehr. Jetzt ist die Datenbank vollständig erstellt und kann mit Daten gefüllt werden.&#x20;



1.3 Python&#x20;

Um später Daten empfangen zu könne und diese in der Datenbank abzulegen benötigen Sie Python. Da es sich um eine Skriptsprache handelt, ist eine IDE nicht vonnöten. Sie können in Ihrem lieblings Editor ein Skript schreiben. In meinem Fall habe ich mich für Atom entschieden Laden Sie sich hierzu Python 2.7 von der Python Homepage herunter. https://www.python.org/downloads/2 Nach der Installation, können Sie überprüfen ob es sich um die richtige Version handelt mit: $ python --version

Damit Sie MySQL unter Python verwenden können, benötigen Sie noch MySQL-Python. https://pypi.python.org/pypi/MySQL-python/3 Nun ist alles komplett und Sie können beginnen&#x20;

2. Anwendung

Aufgabe des Python Skriptes ist es die Daten, welche vom Quadrocopter gemessen und per UDP versendet werden, entgegenzunehmen und in einer Datenbank abzulegen. Hierbei stellt das Skript eine Verbindung zu der Datenbank her und legt dort per INSERTs die empfangenen Daten ab&#x20;

2.1 Struktur der Datenbank

Abbildung 2.1:&#x20;

Struktur der Datenbank&#x20;

• PITIME PITIME ist die Zeit, welche momentan auf dem Pi herscht. Sie wurde als Primary Key gewählt, da es zu jeder Zeit nur einen Messwert geben kann. Angegeben wird sie als Timestamp (YYYY-MM-DD HH:MM:SS:MS) mit einen Genauigkeit von 10ms.&#x20;

• ACC\_X/Y/Z Es werden alle drei Beschleunigungsachsen gespeichert, das Vorzeichen stellt hierbei die Richtung dar.&#x20;

• MAG\_X/Y/Z Für das Magnetfeld werden ebenfalls 3 Datensäzte abgelegt.&#x20;

• TEMP/PRESS Temperatur und der Luftdruck.

• M1/2/3/4 Für die jeweiligen Motoren werden vier Datensätze abgelegt, da diese sich unabhänging von einander drehen können&#x20;

2.2 Auszug aus der Datenbank&#x20;

Hier ist ein beispielhafter Auszug der Datenbank zu sehen, er zeigt einen Ausschnitt aus der Demo.&#x20;

Abbildung 2.2: Daten der Demo&#x20;

2.3 Python 2.3.1&#x20;

Verbindung zur Datenbank Um auf die vorhin erstelle Datenbank zuzugreifen, muss eine Verbindung hergestellt werden. Hierzu wird der neue Benutzer PiSense benötigt, natürlich könnten man auch Root benutzen das ist aber nicht Sinn der Sache.

Abbildung 2.3: Connector

2.3.2 UDP Socket&#x20;

Damit das Skipt eine Message vom Quadrocopter empfangen kann, muss ein UDP Socket auf einem bestimmten Port Lauschen. Python stellt uns hierbei einen Receive-Funktion zur verfügung. Es muss nur die IP und der Port and einen Socket gebindet werden.

Abbildung 2.4: UDP Socket&#x20;

In diesem Fall lauschen wir auf dem Port 5000, benutzen IPv4 und natürlich UDP&#x20;

2.3.3 Empfangen und aufteilen der Daten

Abbildung 2.5: Empfange der Message&#x20;

Es wird so lange gewartet bis eine Message ankommt, falls diese der String ÄFAFïst, wird das Skript beendet. Da die Daten in einem einzigen String ankommen, müssen sie herausgefiltert werden. Um dies zu erreichen wird der String bei jedem Zeilenumbruch getrennt. Nun müssen noch die Bezeichner abgeschnitten werden. Auch hier liefert uns Python einen Lösung mit. Es werden die vier ersten Zeichen verworfen.

Abbildung 2.6: Trennen der Daten

2.3.4 Ablegen der Daten&#x20;

Damit die empfangenen Date jetzt nicht verloren gehen, werden sie in die Datenbank geschrieben. Dies erfolgt über einen INSERT. Hierbei werden die Daten in ihre jeweiligen Spalten der Tabelle gespeichert. Am ende muss das Query noch commited werden, an die Datenbank.

Abbildung 2.7: Query&#x20;

Um sicherzustellen, dass das Skript funktioniert kann mit dem udpSend.py Skipt ein Senden des Quadrocopters simuliert werden. Jedoch handelt es sich hierbei nur um Zufallswerte&#x20;

2.3.5 Ausführen des Skriptes&#x20;

Das Pythonscript lässt sich wie folgt ausführen. Wechseln Sie dazu in das Verzeichnis wo die udpReceive.py zu finden ist. $ python udpReceive.py Falls Sie nun das Skript beenden wollen senden Sie per UDP den String „AFAF“. $ echo "AFAF" | nc -4u localhost 5000&#x20;

2.4 Verwalten der Datenbank&#x20;

2.4.1 Adminer einrichten&#x20;

Adminer wurde zum verwalten der Datenbank verwendet&#x20;

1. Um mit Adminer zu arbeiten laden Sie dieses von der Adminer Homepage herunter. https://www.adminer.org/#download
2. Damit Sie Adminer starten könne müssen Sie die adminer-4.2.5.php Datei in ihr Apache verzeichnis verschieben. $ cd /Library/WebServer/Documents/
3. Jetzt müssen Sie Apache nur noch für php konfigurieren. Erstellen sie ein Backoup Ihrer alten Konfiguration. $ cd /etc/apache2/ $ cp httpd.conf httpd.conf.bak Nun editieren sie die httpd.conf Datei $ vi httpd.conf und kommentieren folgende Zeile wieder ein (die # enfernen). LoadModule php5\_module libexec/apache2/libphp5.so
4. Nun muss der Apache nur noch neugestartet werden. $ sudo apachectl restart&#x20;

2.4.2 Adminer bedienen

1. Navigieren sie Ihren Browser zu: localhost/adminer-4.2.5.php
2. Melden Sie sich mit dem Benutzer für die Datenbank an:

Abbildung 2.8: Anmelden in Adminer&#x20;

3\. Über das linke Menü könne Sie die Datenbank Verwalten.&#x20;

Abbildung 2.9: Adminer Übersicht&#x20;

4\. Unter SQL-Kommando können Sie eingene SQL Anfragen an die Datenbank stellen.

Abbildung 2.10: SQL-Kommando&#x20;

5\. Die Importfunktion ermöglicht es Ihnen einen Dump der Datenbank zu Imporieren. Wählen sie dazu einfach eine sql Datei aus und klicken auf ausführen.

Abbildung 2.11: Importieren einer Tabelle

3 Zukünftige Arbeit&#x20;

• Enwiklung einer GUI Eine GUI, damit die gesammten Skripte nicht mehr von Hand gestartet werden müssen.&#x20;

• Verwaltung der Datenbank über die Gui Verwaltungsmöglichkeit ohne eine externe Software benutzen zu müssen, sondern direkt in der GUI.&#x20;

• Erweitern der Datenbank Die von der Datenbank erfassten Messwerte um weiter ergänzen, z.B. durch Berechnung aus den aktuellen





