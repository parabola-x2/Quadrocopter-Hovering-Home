# README Simulation

#### Repository **:** [https://github.com/parabola-x2/Quadrocopter\_Simulation](https://github.com/parabola-x2/Quadrocopter_Simulation)

**Kalman Filter**

\[\[http://www.convict.lu/htm/rob/imperfect\_data\_in\_a\_noisy\_world2.htm]] \[\[https://www.codeproject.com/Articles/865935/Object-Tracking-Kalman-Filter-with-Ease]]

**Simulations**

* 01\_Control\_one\_angle: Vereinfachtes Modell eines Winkels des Quadrocopters:
* 01\_PID\_Control\_one\_angle: Wie Control\_one\_angle mit der Erweiterung, dass die verwendeten Motoren einen ungleichen Schub erzeugen, und dass dieser mit einer PID Regler Kaskade geregelt wird.
* 02\_Control\_two\_angles: Vereinfachtes Modell bei dem Roll und Pitch geregelt mit einer P-Regler-kaskade geregelt werden.
* 03\_control\_2\_angles\_and\_yawrate: Wie 02\_Control\_two\_angles mit dem Unterschied, dass zusätzlich die Winkelgeschwindigkeit des YAW geregelt wird.
* 04\_discrete\_control\_phi\_theta\_rpsi: Die diskretisierte Regelung des Modells 03\_control\_2\_angles\_and\_yawrate
* 05\_discrete\_control\_with\_noise: Wie 04\_discrete\_control\_phi\_theta\_rpsi mit dem Unterschied, dass den Regelgrößen ein Rauschen überlagert wird.
* 06\_discrete\_noise\_Quantified: Wie 05\_discrete\_control\_with\_noise mit dem Unterschied, dass die Regelgrößen zusätzich quantifiziert werden, um die Abtastung eines Milrcontrollers zu simulieren
* 07\_discrete\_control\_angle\_from\_acc: Wie 06\_discrete\_noise\_Quantified mit dem Unterschied, dass die Winkel-information zuerst in eine Beschleunigung und anschließend wieder in einen Winkel zurückgerechnet wird.
* 07\_PID\_Discrete: Vollständiges Modell der Quadrocopterregelung unter Verwendung einer PID-Reglerkaskade.
* 08\_HIL: Vollständiges Modell der Quadrocopterregelung Regelung mit dem Block für den Modell in Loop test. Verwendet zusätzlich den Embedded MATLAB Block für die P-Reglerkaskade.
* 08\_PID\_HIL: Wie 08\_HIL mit dem Unterschied, dass der Embedded MATLAB Block die Regelung per PID-Regler beinhaltet.
* Final\_System: Enhält das Gesamtsystem für die P-Reglerkaskade/Zustandsregler. Finales System ist jedoch im Ordner 08\_PID\_HIL !!!
* scratch: Enthält MATLAB-Dateien für Versuche.

Matlab Files

* calc\_stability.m: Dieses M-File wertet das Modell Quadrocopter\_control bezüglich der Eigenwerte(Polstellen der Regelstrecke) aus.
* Control\_lib.mdl: Dieses M-File wertet das Modell Quadrocopter\_control bezüglich der Eigenwerte(Polstellen der Regelstrecke) aus.
* Control\_lib.mdl: Diese Bibliothek beinhaltet Simulink Blöcke, welche für die Regelung verwendet wurden.
* Copter\_Library.mdl: Diese Bibliothek beinhaltet Simulink Blöcke welche für die Regelstrecke, Animation und Sensoren verwendet wurden.
* Copter\_Animation.m: Level 1 S-Function welche die Animation des Quadrocopters beinhaltet, wird von einem S-Function Block verwendet( siehe Copter\_Library.mdl).
* crc16.c: Mex-Function zum Berechnen der CRC16-Prüfsumme für das Quadrocopter ZigBee Modell.
* crc16.mexw32: Compilierte Mex-Funktion aus crc16.c.
* double2uint8.c: Mex-Function zum konvertieren von double zu unsigned int8.
* double2uint8.mexw32: Compilierte Mex-Funktion aus double2uint8.mexw32.
* quadrocopter\_param.m: Diese Datei erzeugt die Parameter für den Quadrocopter im Workspace
* \_sfun.mexw32: Diese Dateien beinhalten die Compilierten Embedded MATLAB teile der Modelle mit dem Namen \*.mdl. !!! Anmerkung: Auf Grund von Pfadtiefen kann es erforderlich werden Modelle zuerst in diesem Pfad auszuführen und dort die \*\_sfunc.mexw32 Dateien erstellen zu lassen. Anschließend können diese in den entsprechenden Ordner kopiert/verschoben werden.

#### Hint

A native software similiar to the Matlab needs to be built in VREP. Here, the specifications are the same as for the Matlab Team. The only difference is that in VREP, the Quadrocopter Dynamics Model is readily available ( drag and drop ), whereas in MATLAB, a Quadrocopter Dynamics Model had to be built from scratch. Also, in V-REP one can attach the sensors ( drag and drop ) on the Virtual Quadrocopter and simply start acquiring the values, once the system is run.

\{{:hs\_esslingen:helikopter:architecture1.png?400|\}}

\{{hs\_esslingen:helikopter:images:interface-control-embedded.png \}}

\{{hs\_esslingen:helikopter:images:interface-control-vr.png \}}\{{hs\_esslingen:helikopter:images:virtualreality.png \}}
