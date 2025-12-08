# README Android

#### Repository **:** [https://github.com/parabola-x2/Quadrocopter\_Android](https://github.com/parabola-x2/Quadrocopter_Android)

The project contains a AndroidStudio based Java Android application to steer a quadrocopter. The project also contains a QT based C++ desktop application to steer a quadrocopter.

<figure><img src=".gitbook/assets/AppVorlage1.png" alt="" width="139"><figcaption></figcaption></figure>

Author : Christoph Weik

![](.gitbook/assets/unknown.png)

PiSense mit Quadrocopter 2016&#x20;

Android Applikation&#x20;

Vorwort&#x20;

In allen Informatikstudiengängen der Universität Tübingen ist die Teilnahme an einem Softwareprojekt verpflichtend. Das Team-Projekt PiSense mit Quadrocopter, handelte rund um die Anpassung der Low-Level-Treiber, um das Speichern sowie Auslesen von Sensordaten&#x20;

in Datenbank und GUI zu ermöglichen. Der folgenden Unterabschnitt des Projekts hatte zum Ziel, die Entwicklung einer Applikation zur Steuerung der Rotorgeschwindigkeit und Senden vorgegebener Befehlsketten an den Raspberry Pi. Diese wurde von Grund auf neu entworfen und beruht nicht auf Arbeiten vorheriger Semester.

Inhaltsverzeichnis\
1 Getting Started (mit Windows 7)&#x20;

1 1.1 Java 8 installieren\
1.1.1 Installation des Java Development Kit 8\
1.1.2 Installation der Java-Dokumentation\
1.1.3 Installation der Java-Quelltexte\
1.1.4 Eintragen des Path in die Umgebungsvariable\
1.2 Android Studio installieren\
1.2.1 Installation des Hauptprogramms\
1.2.2 Prüfung der installieren Packages\
1.2.3 Installation von Intel HAXM\
1.3 Android Virtual Device und Android Debugging Bridge\
1.3.1 AVD in Android Studio einrichten\
1.3.2 Einrichten der Android Debugging Bridge (ADB)\
1.4 Git\
1.4.1 Installation von Git\
1.4.2 Git in Android Studio\
2 Android Applikation 23 2.1 Einleitung\
2.1.1 Ressourcen\
2.1.2 Activity\
2.1.3 Fragment\
2.2 Layout\
2.3 Funktion\
Abbildungsverzeichnis I\
1.1 Aktuelle Portierungen des JDK 8\
1.1 Aktuelle Portierungen des JDK 8 0.\
Abbildungsverzeichnis II\
1.2 Ausgabe der aktuell installierten Java Version in der Kommandozeile\
1.3 Kopieren des Docs-Verzeichnis in das JDK-Verzeichnis\
1.4 Lesezeichen Dokumentation Java 8 SE\
1.5 Entpacken der Archivdatei\
1.6 Ausgeben der Versionsnummer des Java Compilers\
1.7 Android Studio Setup > Komponenten auswählen\
1.8 Android Studio Dialog > Import Settings\
1.9 Android Studio Dialog > SDK Components Setup\
1.10 Android Studio: Updaten über Quick Start-Menü\
1.11 Android Studio: Installierte Packages der SDK Platforms\
1.12 Android Studio: Installierte Packages der SDK Tools\
1.13 Intel HAXM Setup\
1.14 Arbeitsspeicherzuweisung an Intel HAXM\
1.15 Intel HAXM: Prüfung auf Systemausführung\
1.16 Android Virtual Device Manager über AVD Manager-Icon\
1.17 AVD Manager über Menü\
1.18 Your Virtual Device Dialog\
1.19 AVD Device Selection\
1.20 AVD System Image Selection\
1.21 Emuliertes Nexus 4 mit Android 6.0\
1.22 Android Entwickleroptionen aktivieren\
1.23 USB-Debugging und wach bleiben aktivieren\
1.24 Angeschlossene Geräte mit Hilfe der ADB anzeigen lassen\
1.25 RSA-Schlüssel-Fingerabdruck\
1.26 ADB Server Neustart\
1.27 Android Gerät erfolgreich als device gelistet\
1.28 Help Dokumentation in Atreus\
1.29 Version Control Settings\
1.30 Git erfolgreich ausgeführt\
1.31 Menü Navigation „Create Git Repository“\
1.32 Starten von Git BASH im Projektverzeichnis\
1.33 SSH Adresse des Repositories in Atreus\
1.34 Hinzufügen eines Remote Repositories in Git BASH\
1.35 Ein Projekt mit Android Studio von Git klonen\
1.36 Menü Navigation zu Add, Commit und Push\
2.1 Beispielhafte Darstellung der String Ressource unserer App\
2.2 Callback-Methoden des Activity Lifecyle in Android\
2.3 Activity wird vollständig mit Fragment Layout ausgefüllt\
Abbildungsverzeichnis III\
2.4 Callback-Methoden des Fragment Lifecyle in Android\
2.5 GUI Editor in Android Studio\
2.6 For-Schleife zur Bindung von Listenern an View-Objekte\
2.7 Innere Arbeiterklasse ClientSend\
2.8 Methode udpSend\
2.9 Abspeicherung des Seekbarforschritts in der OnProgressChanged-Methode\
2.10 Auslesen der SharedPreferences XML und Prüfen auf Darstellungsmodus

1 Getting Started (mit Windows 7)&#x20;

1 1.1 Java 8 installieren\
1.1.1 Installation des Java Development Kit 8<br>

Die aktuellste Version des JDK findet man auf der Herstellerwebsite unter: • http://www.oracle.com/technetwork/java/javase/downloads/index.html&#x20;

![](<.gitbook/assets/unknown (1).png>)

Abbildung 1.1: Aktuelle Portierungen des JDK 8.&#x20;

Die benötigte Java-Installationsdatei heißt im Falle von Microsoft Windows 7 (64 Bit) jdk 8u101-windows-x64.exe.&#x20;

Vor der Installation ist es jedoch sinnvoll zu Prüfen, ob bereits die aktuellste Version vorliegt. Die geschieht in Windows 7 folgendermaßen:&#x20;

1\. Öffne zuerst die Kommandozeile (Windowstaste + R → im Eingabefeld cmd eingeben). 2. In der Kommandozeile java -version eingeben.&#x20;

&#x20;![](<.gitbook/assets/unknown (2).png>)

Abbildung 1.2: Ausgabe der aktuell installierten Java Version in der Kommandozeile.&#x20;

In diesem Beispiel ist die Java Version 1.7.0\_45 bereits veraltet und eine neuere Version sollte installiert werden.&#x20;

1.1.2 Installation der Java-Dokumentation&#x20;

Die folgenden Links führen zur Online Dokumentation von Java 8 SE und der Download-Seite: • http://docs.oracle.com/javase/8/docs/index.html&#x20;

• http://www.oracle.com/technetwork/java/javase/documentation/jdk8-doc-downloads-2html&#x20;

Für uns ist nur die obere mit der Bezeichnung „Java SE Development Kit 8u101 Documenta tion“ relevant. Diese entpacken wir und kopieren sie anschließend in das JDK-Verzeichnis.&#x20;

![](<.gitbook/assets/unknown (3).png>)

Abbildung 1.3: Kopieren des Docs-Verzeichnis in das JDK-Verzeichnis.&#x20;

Die Java-Dokumentation wird über einen Browser betrachtet. Es bietet sich daher an ein Lesezeichen anzulegen, welches auf das Hauptdokument verweist. Wie bspw.: file://localhost/C:/Program%20Files/Java/jdk1.8.0\_101/docs/index.html&#x20;

![](<.gitbook/assets/unknown (4).png>)

Abbildung 1.4: Lesezeichen Dokumentation Java 8 SE.&#x20;

1.1.3 Installation der Java-Quelltexte&#x20;

Die Quelltexte befinden sich bereits im Installationsverzeichnis des JDK 8 und müssen nur noch entpackt werden.&#x20;

![](<.gitbook/assets/unknown (5).png>)

Abbildung 1.5: Entpacken der Archivdatei.&#x20;

1.1.4 Eintragen des Path in die Umgebungsvariable&#x20;

Unter Windows 7 kann die Systemvariable Path folgendermaßen geändert werden: 1. Windowstaste + Pause, dann erweiterte Systemeinstellungen.&#x20;

2\. Auf dem Reiter Erweitert wählen wir Umgebungsvariablen. . . .&#x20;

3\. Füge den Pfad des bin-Ordners der JDK-Installation in die Systemvariable Path ein.&#x20;

Die Path Variable könnte dann beispielsweise so aussehen:&#x20;

C:\WINDOWS\system32;C:\WINDOWS;C:\ProgramFiles\Java\jdk1.8.0\_101\bin Nun sollte es auch möglich sein durch den Befehl javac -version die Version des Java Compilers auszugeben.&#x20;

![](<.gitbook/assets/unknown (6).png>)

Abbildung 1.6: Ausgeben der Versionsnummer des Java Compilers.&#x20;

1.2 Android Studio installieren&#x20;

1.2.1 Installation des Hauptprogramms&#x20;

Die Installationsdatei von Android Studio findet ihr auf der Android Entwickler Webseite. Über die Reiter Develop > Android Studio gelangt ihr zum Download-Bereich.&#x20;

• http://developer.android.com/&#x20;

Nach dem Starten des Wizards werdet ihr kurze Zeit später gebeten die gewünschten Komponenten auszusuchen. Hierbei wählen wir alles außer das Android Virtual Device, da wir später unser eigenes AVD in Android Studio anlegen werden.&#x20;

![](<.gitbook/assets/unknown (7).png>)

Abbildung 1.7: Android Studio Setup > Komponenten auswählen.&#x20;

Nach der Beendigung des Wizards erscheint noch der Dialog „Complete Installation“ , den wir noch durchlaufen müssen. Da wir von einer erstmaligen Installation von Android Studio ausgehen, wählen wir die untere Option „I do not have a previous version of Studio or I do not want to import my settings“.&#x20;

![](<.gitbook/assets/unknown (8).png>)

Abbildung 1.8: Android Studio Dialog > Import Settings.&#x20;

Am SDK Components Setup Dialog angelangt, setzen wir Häkchen bei Android SDK, Android SDK Platform, API 23: Android 6.0 (Marschmallow). Die fehlenden Komponenten werden wir später manuell einrichten.&#x20;

Wichtig! Bei Android SDK Location den selben Pfad angeben, wie auch schon bei der Android SDK Installation Location.&#x20;

![](<.gitbook/assets/unknown (9).png>)

Abbildung 1.9: Android Studio Dialog > SDK Components Setup.&#x20;

Nach Abschluss der Installation wählen wir im Willkommensbildschirm aus dem Quick Start Menü „Configure“ und klicken auf den vorletzten Menüeintrag Check for Updates. Ist das Updaten abgeschlossen steht dem Entwickeln einer App nicht mehr viel im Weg.&#x20;

![](<.gitbook/assets/unknown (10).png>)

Abbildung 1.10: Android Studio: Updaten über Quick Start-Menü.&#x20;

1.2.2 Prüfung der installieren Packages&#x20;

In der Bildserie folgenden werden alle Packages aufgeführt die zur Entwicklung der App verwendet wurden. Es wird empfohlen diese zu installieren, um so maximale Kompatibilität zu gewährleisten. Ihr öffnet den SDK Manager über das Quick Start-Menü. Die jeweiligen Packages werden mit Hilfe des Standalone SDK Managers installiert (siehe Abb. 1.11)&#x20;

![](<.gitbook/assets/unknown (11).png>)

Abbildung 1.11: Android Studio: Installierte Packages der SDK Platforms.&#x20;

&#x20;![](<.gitbook/assets/unknown (12).png>)

Abbildung 1.12: Android Studio: Installierte Packages der SDK Tools.&#x20;

1.2.3 Installation von Intel HAXM&#x20;

Die Installationsdateien des INTEL HAXM (Hardware Accelerated Execution Manager) wurden bei der Installation von Android Studio bereits in das Verzeichnis des Android SDKs kopiert. Das Verzeichnis befindet sich unter folgendem Pfad:&#x20;

...AndroidSDK\extras\intel\Hardware\_Accelerated\_Execution\_Manager&#x20;

Nachdem der HAXM-Installer gestartet wurde, öffnet sich der Willkommensbildschirm des Setup-Dialogs. Falls euer System die Systemvoraussetzungen nicht erfüllt, wird die Installation automatisch abgebrochen.&#x20;

![](<.gitbook/assets/unknown (13).png>)

Abbildung 1.13: Intel HAXM Setup.&#x20;

Im nächsten Schritt wird nun nach einer Obergrenze für den Arbeitsspeicher gefragt, die HAXM verwenden darf. Es kann die Hälfte des auf dem PC verfügbaren Arbeitsspeichers angegeben werden.&#x20;

Achtung! Dieser Wert sollte nicht zu hoch angesetzt werden, ansonsten könnten ande re Programme langsamer ausgeführt werden.&#x20;



&#x20;![](<.gitbook/assets/unknown (14).png>)

Abbildung 1.14: Arbeitsspeicherzuweisung an Intel HAXM.&#x20;

Nach abgeschlossener Installation gilt es noch zu Prüfen, ob Intel HAXM ordnungsgemäß auf dem System ausgeführt wird. Hierfür starten wir die Kommandozeile als Administrator und verwenden folgenden Befehl: sc query intelhaxm.&#x20;

Abbildung 1.15: Intel HAXM: Prüfung auf Systemausführung.&#x20;

Zeigt die Konsole STATE: 4 running oder ähnliches an, wird Intel HAXM korrekt auf dem Rechner ausgeführt.&#x20;

1.3 Android Virtual Device und Android Debugging Bridge&#x20;

1.3.1 AVD in Android Studio einrichten&#x20;

Zur Ausführung einer App auf dem PC benötigen wir einen Android Emulator. Android Studio stellt uns für diesen Zweck den Android Virtual Device Manager zur Verfügung. Die beiden Möglichkeiten auf diesen zuzugreifen werden in den Abbildungen 1.16 und 1.17 aufgeführt.&#x20;

Abbildung 1.16: Android Virtual Device Manager über AVD Manager-Icon.&#x20;

Abbildung 1.17: AVD Manager über Menü.&#x20;

Nachdem der AVD Manager das erste Mal gestartet wurde, öffnet sich der Your Virtual Devices-Dialog des Managers. An dieser Stelle besteht die Möglichkeit ein Android Virtual Device einzurichten.&#x20;

Abbildung 1.18: Your Virtual Device Dialog.&#x20;

In den folgenden Bildschirmen lassen sich zu emulierendes Gerät,System Image und Bild schirmorientierung bestimmen (Siehe Abb. 1.19 und 1.20). Weitere Images können nach belieben zusätzlich heruntergeladen werden.&#x20;

Abbildung 1.19: AVD Device Selection.&#x20;

Abbildung 1.20: AVD System Image Selection.&#x20;

Anschließend lässt sich das emulierte Gerät entweder über den AVD Manager oder das Run-Icon starten. Dieser Vorgang benötigt unter Umständen einige Minuten.&#x20;

Abbildung 1.21: Emuliertes Nexus 4 mit Android 6.0.&#x20;

1.3.2 Einrichten der Android Debugging Bridge (ADB)&#x20;

Das Aufbauen einer Android Debugging Bridge, benötigt zunächst das Aktivieren der Ent wicklereinstellungen auf dem Smartphone (Siehe Abb. 1.22). Diese sind auf Geräten mit Android 4.2 oder neuer standardmäßig versteckt.&#x20;

Abbildung 1.22: Android Entwickleroptionen aktivieren.&#x20;

Nachdem die Android Entwickleroptionen aktiviert wurden. Müssen zwingend bei „wach bleiben“ und „USB-Debugging“ Häkchen gesetzt werden (Siehe Abb. 1.23). USB-Debugging erlaubt dem angeschlossenen Rechner die Kommunikation mit dem Android Gerät.&#x20;

Abbildung 1.23: USB-Debugging und wach bleiben aktivieren.&#x20;

Damit eine Verbindung des PCs mit dem Android Gerät möglich ist, muss der passende USB Treiber für das Smartphone oder Tablet auf unserem System installiert werden:&#x20;

• Android Developer Phones, wie Nexus One oder Nexus S, benötigen die Google USB Treiber: http://developer.android.com/sdk/win-usb.html&#x20;

• Einer Liste anderer Hersteller mit Treiber URL findet man hier:&#x20;

http://developer.android.com/tools/extras/oem-usb.html#Drivers&#x20;

Das Ansteuern des Android Gerätes erfolgt über die Konsole im Verzeichnis ..\AndroidSDK\ platform-tools oder das Terminal in Android Studio. Mit dem Befehl adb devices lassen sich angeschlossene Geräte anzeigen.&#x20;

Abbildung 1.24: Angeschlossene Geräte mit Hilfe der ADB anzeigen lassen.&#x20;

Das Gerät ist zu diesem Zeitpunkt noch nicht autorisiert und eine Verbindung unmöglich. Hierbei handelt es sich um einen Schutzmechanismus aller Android Geräte ab Android 4.2.2, um vor unberechtigten Zugriff zu schützen. Die Autorisierung erfolgt über das Android Gerät, in einem Dialog bittet es um einen RSA-Handshake.&#x20;

Abbildung 1.25: RSA-Schlüssel-Fingerabdruck.&#x20;

Um den oben beschriebenen USB-Debugging Dialog anzeigen zu lassen und eine Verbindung zum Android Gerät anzufordern, verwenden wir folgende ADB-Befehle in der Konsole (die Dateiendung .exe ist nicht zwingend erforderlich):&#x20;

• Beenden des ADB Servers mit: adb.exe kill-server&#x20;

• Starten des ADB Servers mit: adb.exe start-server&#x20;

Achtung! Sicher stellen, dass der Bildschirm des Android Gerätes entriegelt ist! Abbildung 1.26: ADB Server Neustart.&#x20;

Nach erfolgreicher Ausführung, sollte der Befehl adb devices das Android Gerät als device führen. Eine Installation der App auf dem Zielgerät, ist nun mit Hilfe des Run-Icons in Android Studio möglich.&#x20;

Abbildung 1.27: Android Gerät erfolgreich als device gelistet.&#x20;

1.4 Git&#x20;

1.4.1 Installation von Git&#x20;

Die Verwendung von Git auf Windows 7 erfordert zunächst die Installation einer Git Shell, wie beispielsweise Git BASH.&#x20;

• https://git-for-windows.github.io/&#x20;

Mit Hilfe der Help Dokumentation im Atreus lassen sich schnell Probleme, wie die Initia lisierung des global user.names, der global user.email und das Generieren eines SSH-Keys bewerkstelligen (Siehe Abb 1.28).&#x20;

Abbildung 1.28: Help Dokumentation in Atreus.&#x20;

1.4.2 Git in Android Studio&#x20;

Im Folgenden handelt es sich um eine Step-by-Step Anleitung zur Einrichtung von Git als Version Control in Android Studio. Zu Beginn navigieren wir zu den Git Version Control Settings über File > Settings > Version Control > Git (Siehe Abb. 1.29). In Windows 7 ist default Pfad der git.exe C:\ProgramFiles\Git\cmd\git.exe diesen tragen wir in „Path to executable“ ein. Ein erfolgreicher Test sollte eine Rückmeldung wie in Abbildung 1.30 geben.&#x20;

Wichtig! SSH-executable auf Built-in lassen.&#x20;

Abbildung 1.29: Version Control Settings.&#x20;

Abbildung 1.30: Git erfolgreich ausgeführt.&#x20;

Anschließend schließen wir das aktuelle Fenster wieder und erstellen mit den nächsten Schritten ein lokales Git Repository in Android Studio. Dazu navigieren wir über VCS > Import into Version Control > Create Git Repository (Siehe Abb. )&#x20;

Abbildung 1.31: Menü Navigation „Create Git Repository“&#x20;

Als nächstes designieren wir das Verzeichnis, welches von Git initialisiert werden soll. Hier bietet es sich an das Projektverzeichnis zu wählen. Im Folgenden öffnen wir den Pfad unseres Projektverzeichnisses und starten über das Rechtsklickmenü Git BASH (Siehe Abb. 1.32)&#x20;

Abbildung 1.32: Starten von Git BASH im Projektverzeichnis&#x20;



Im Git BASH angekommen möchten wir das gewünschte Remote Repository hinzufügen. Dies geschieht über den Befehl:&#x20;

git remote add origin ssh://\[user]@\[server\_address]/\[git\_repo\_url] In unserem Fall wäre die gewünschte Adresse (aus Atreus):&#x20;

git@atreus.informatik.uni-tuebingen.de:Programmierprojekt2016/QuadrocopterAndroid. git.&#x20;

Abbildung 1.33: SSH Adresse des Repositories in Atreus.&#x20;

Abbildung 1.34: Hinzufügen eines Remote Repositories in Git BASH.&#x20;

Um nun erfolgreich an der bereits gestellten App weiter programmieren zu können muss das Projekt erst von Git geklont werden. Dies ist möglich über VCS > Checkout from Version Control > Git. Im folgenden Fenster tragen wir die Ziel URL ein, sowie den Namen des Branches den wir klonen wollen (Siehe Abb. 1.35).&#x20;

Abbildung 1.35: Ein Projekt mit Android Studio von Git klonen.&#x20;

Der Ablauf eines erfolgreichen Commits ist wie folgt: Hinzufügen der Daten zum Git Reository > Committen des Verzeichnisses und hinterlassen einer Commit Nachricht > Pushen aller Änderungen auf das Remote Repository und angegebenen Branch.&#x20;

(a) Add (b) Commit&#x20;

(c) Push.&#x20;

Abbildung 1.36: Menü Navigation zu Add, Commit und Push.&#x20;

2.1 Einleitung&#x20;

2.1.1 Ressourcen&#x20;

Effektives Ressourcen-Management in Android Studio gestaltet die Entwicklung einer App sehr unkompliziert und übersichtlich. Sämtliche Informationen über GUI Elemente, Strings, Menübausteine oder auch Präferenzen werden in XML Dokumente leicht zugänglich abgelegt und kommen der Lesbarkeit des Codes zugute.&#x20;

Abbildung 2.1: Beispielhafte Darstellung der String Ressource unserer App.&#x20;



2.1.2 Activity&#x20;

Eine Activity ist ein Bestandteil einer Anwendung, die einen Bildschirm zur Verfügung stellt, mit dem der Benutzer interagieren kann. Im Regelfall besteht eine App aus mehreren Activities die lose miteinander verbunden sind. Jede Activity besitzt die Fähigkeit eine andere Activity zu starten, dabei wird die Aktuelle gestoppt und die Gestartete rückt in den Fokus. Der Zustand der gestoppten Activity bleibt jedoch im Android System erhalten. Dies ist der Moment wenn sogenannte Lifecyle-Callbacks in Kraft treten. Diese informieren die Activity über eintretende Zustandsänderungen und geben die Gelegenheit bestimmte, notwendige Arbeit zu verrichten, bevor diese Zustandsänderung eintritt.&#x20;

Abbildung 2.2: Callback-Methoden des Activity Lifecyle in Android.&#x20;

Achtung! Implementiert man eine dieser Lifecycle-Methoden, ist es zwingen notwendig zuerst die Implementierung der Basisklasse aufzurufen.&#x20;

protected void onPause() {&#x20;

super.onPause(); // Aufrufen der Implementierung der Superklasse // Hier folgt der eigene Code&#x20;

}&#x20;

2.1.3 Fragment&#x20;

Bei Fragmenten handelt es sich um Modulare Bereiche einer Activity. Diese verfügen über ihre eigenen Lifecycle und Callback-Methoden. Der übergeordnete Activity-Lifecycle beeinflusst den Fragment-Lifecycle direkt. Das heißt, pausiert bzw. wird die Activity zerstört, dann tut dies auch das zugehörige Fragment. Eine Activity kann über mehrere Fragmente verfügen und diese können auch in mehreren Activities wiederverwendet werden. Fragmente müssen nicht zwingend Teil des Activity Layouts sein, sie können auch als unsichtbare Arbeiter eingegliedert werden.&#x20;

Abbildung 2.3: Activity wird vollständig mit Fragment Layout ausgefüllt.&#x20;



Abbildung 2.4: Callback-Methoden des Fragment Lifecyle in Android. Android&#x20;

2.2 Layout&#x20;

Das Layout der App wurde vollständig mithilfe des GUI Editors von Android Studio erstellt. Nach Erstellung der notwendigen layout.xml erzeugt dieser automatisch das passende XML Gegenstück zum jeweiligen GUI Element. Die in der App verwendete Oberfläche gestaltet sich wenig komplex, hierbei handelt es sich mehrere ineinander geschachtelte horizontale und vertikale Layouts. Eingefügt wurden jeweils die gewünschten Buttons, Textfelder und Seekbars.&#x20;

Achtung! Editiert wird indem Layouts und GUI-Elemente in den Component Tree rechts oben gezogen werden.&#x20;

Abbildung 2.5: GUI Editor in Android Studio.&#x20;



Eigenschaften der jeweiligen Elemente wird durch das Properties Menü unten rechts beeinflusst. Hier lassen sich Ausrichtung (gravity), Abstände (padding, margin...), Farbe und vieles mehr bestimmen. Eines der wichtigsten Attribute ist jedoch die id hiermit lassen sich Layout Elemente im Editor benennen und im Code auf deren Layout zugreifen. Buttons, TextViews und SeekBars werden mithilfe der ID Objekte auf denen dann Arbeit verrichtet werden kann. Für Buttons und SeekBars war es des Weiteren notwendig Listener zu implementieren, die auf Zustandsänderungen reagieren können (Siehe Abb. 2.6).&#x20;

Abbildung 2.6: For-Schleife zur Bindung von Listenern an View-Objekte.&#x20;

2.3 Funktion&#x20;

Die angedachte Funktion der Applikation ist es Befehlsketten auf Aktivierung der jeweiligen Buttons per UDP an den Raspberry Pi zu schicken. Dies geschieht mithilfe eines separa ten Threads der auf einem Objekt der inneren Klasse ClientSend ausgeführt wird. Diese implementiert das Interface Runnable und muss somit eine Run() Methode aufweisen, die später vom Thread aufgerufen wird. Die volatile String Variable task wird hierbei von der&#x20;

Abbildung 2.7: Innere Arbeiterklasse ClientSend.&#x20;

Hauptklasse so manipuliert, dass der gewünschte Befehl per UDP weiter gesendet werden kann. Die Befehlsketten sind jeweils in der String resource.xml abgespeichert und werden von der udpSend Methode in ihre Byte-Sequenz zerlegt bevor sie als packet weitergeschickt werden.&#x20;

Abbildung 2.8: Methode udpSend.&#x20;

Da es sich bei der Manipulation der Rotorgeschwindigkeit nicht um statische Daten handelt wurden Klassenvariablen eingeführt, die Veränderung des Seekbar Fortschritts unmittelbar abspeichern. Durch das verwenden der String.Format Methode werden Dezimalwerte nach träglich in die Befehlskette eingefügt und in einer loop gesendet. Auf diese Weise lassen sich die Rotoren bis zum Abschalten beliebig beeinflussen.&#x20;

Abbildung 2.9: Abspeicherung des Seekbarforschritts in der OnProgressChanged-Methode.&#x20;

Eine letzte Funktionalität der App ist das Abspeichern einer bevorzugten IP-Adresse, sowie eines Ports. Dies ermöglicht das Verbinden der App auch mit anderen Geräten. Es gibt auch einen Default Modus der fest auf die IP und den Port des im Projekt verwendeten Quadrocopters eingestellt ist. Hierbei handelt es sich um eine Checkbox zum de-/und aktivie ren. Im Gegensatz zu normalen Layouts bezieht die SettingsActivity ihr Aussehen aus einer preferences.xml. Diese SharedPreferences XML speichert die eingegebenen Einstellungen auch nach verlassen der App.&#x20;



Abbildung 2.10: Auslesen der SharedPreferences XML und Prüfen auf Darstellungsmodus.&#x20;







