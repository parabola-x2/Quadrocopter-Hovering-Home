# README Simulation

#### Repository **:** [https://github.com/parabola-x2/Quadrocopter\_Simulation](https://github.com/parabola-x2/Quadrocopter_Simulation)

<figure><img src="/broken/files/TmFQeQWyDKy1xqL529Qd" alt=""><figcaption></figcaption></figure>

Create a simulation environment of a Quadrocopter in Matlab and validate the system on a real microcontroller like Raspberry Pi. Different state estimation filter coefficients for example, filter coefficients of Kalman Filters are to be tested during the simulation, so that their optimum value could be evaluated.&#x20;

A simulink model ( see picture above ) is available for a quick start on the thesis. The\
goal of the thesis is to simulate the hovering and landing skills of the Quadrocopter.&#x20;

Further, the task is to generate source code from the simulink model, so that it can be ported to the real hardware.

### 1. Development with Simulink

Existing Helicopter model can simulate a Hovering at a particular point from ground if the axes coordinate is provided. The idea is implement a Path follower simulation. The new model could follow a given path (the path itself given as coordinates in time series). Copter follows linear path in between the coordinates.

New development:

* Path command: Previous Model has Step inputs for x,y,z and Altitude. This is replaced with inputs from Path.mat file which loads time series from work space.
* Position Controller: Since the new model can change position dynamically, a controller is required to adjust the offset and errors. Implementation for Rotation error correction, Phi and Theta controllers (Here PD controllers are enough). Psi is considered as constant.

### 2. Software in loop

Simulink provides an option to generate C-code which is ANSI-C (C90 compliance – LCC compiler) which can be used to flash with Hardware. The software can also be tested with Simulink model itself by replacing the Simulink subsystem with help of generated code. This generated S functions are more compact with less run time compared to the Simulink blocks itself.

How to generate c-code:

* Right click over the subsystem (which has to be coded)
* Select C/C++code
* Select Generate s –function
* Select the Path Model (parameter set- calibration)

Expected error : If the required prerequisite not met. For example, IC.mat or Path\_model or Path\_xxx not loaded.

### 3. GUI development with MATLAB

The physical parameters of a helicopter are fixed during the run-time simulation. However, GUI is made available with help of which physical parameters can be changed and new Helicopter model can be visualized. With new physical parameters, Attitude controllers have to be fine-tuned. Current tuning of controllers are done with ‘Trial and Error method’ but there is also development opportunity to evaluate the poles and zeros of the whole system and estimate the Kp,KI and KD values with the changes in Physical parameters.

How To:

* MATLAB HomenewappGuide
* Create a new GUI –if new GUI has to be developed from scratch
* Open Existing GUI – changes to be done with existing GUI (if \*.fig and\*.m exist, then it can be edited with this option).

### 4. Verification and Validation with Simulink

With Simulink, there are opportunities to self-correct the implementations with Verification and Validation option. For example, the Simulink crosschecks the run-time configurations like solver and other parameters, evaluates the feasibility of it. Then it provides the alternate feasible solutions.

How to :

1. Analyisis tab in Simulink has Model Advisor Option
2. Select a subsystem to be verified.
3. Select the verification ‘by task’.
4. Specific options can be selected (example MISRA, ISO 26262 etc.,)

***

**TEAM Control Application**

Develop a MATLAB model that stabilizes the quadcopter during hovering, ensuring roll, pitch, and yaw angles remain at zero.

* The core quadcopter MATLAB model incorporates static parameters such as **weight**, **arm length**, and **number of rotors**, which are essential for emulating quadcopter dynamics.
* **Initial values** for angles, accelerations, and rotor speeds are provided as inputs to the model.
* The model then predicts the **roll, pitch, and yaw angles**, along with the **linear accelerations** in all directions.
* These predicted angles and accelerations are fed into the hovering control model, which calculates the required rotor angular speeds.
* The calculated rotor speeds are fed back into the quadcopter model, creating a **closed-loop iterative process** that continues throughout the simulation.
* The control team must generate the hovering model using the **MATLAB Real-Time Code Generator** to ensure real-time execution.
* Verification of the software is performed through **Software-in-the-Loop (SiL) testing**, validating the correctness and stability of the hovering control system.



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
