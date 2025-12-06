---
cover: >-
  https://images.unsplash.com/photo-1504890001746-a9a68eda46e2?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw2fHxEcm9uZXxlbnwwfHx8fDE3NjUwMjAwOTV8MA&ixlib=rb-4.1.0&q=85
coverY: 256.5
layout:
  width: default
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
  metadata:
    visible: false
---

# README

## Timeline

```mermaid
---
config:
  logLevel: 'debug'
  theme: 'base'
  themeVariables:
    darkMode : false
    fontSize : 40px
    fontFamily : verdana
---
timeline 2017
    title Quadrocopter Hovering@Home
    13.03 : Start of summer semester
    03.04 : Under<br>standing the requir<br>ements
    08.05 : First Delivery
    12.06 : Second Delivery
    28.06 : End of summer semester
    03.07 until 14.07  : Exams
    19.07 : Final Presen<br>tation
```

## Topic and Teams

{% columns %}
{% column %}
<figure><img src=".gitbook/assets/Quadrocopter VR.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src=".gitbook/assets/QuadrocopterTeam.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

#### Team Tasks Technical

<figure><img src=".gitbook/assets/team tasks quadrocopter.png" alt=""><figcaption></figcaption></figure>

#### Team Tasks Managing

<figure><img src=".gitbook/assets/team_management.png" alt=""><figcaption></figcaption></figure>

**TEAM Embedded Software**

Develop a real-time Linux kernel named **Raspbian.img** and port it to the Raspberry Pi. Run the application software to read sensor values and control the quadrocopter

* Before porting the Linux image (**kernel.img**) to the Raspberry Pi, a bootloader must be installed to load the kernel during the startup process.
* Once the kernel is running, the embedded software team should be able to debug it using **GDB**. For this purpose, the kernel must be compiled with the **-ggdb3** option (debugging enabled).
* An IMU, gyroscope, and magnetometer are integrated as a peripheral board connected to the main Raspberry Pi motherboard.
* Communication between the Raspberry Pi and the sensor board takes place via the **I2C bus**.
* The application software (**HElikopter.bin**) and the I2C device drivers are already provided.
* The application software is capable of reading acceleration, magnetic field, and gyroscope values.
* The team should be able to set breakpoints at any point during execution of the application software on the hardware to inspect internal variables.

**TEAM Control Application**

Develop a MATLAB model that stabilizes the quadcopter during hovering, ensuring roll, pitch, and yaw angles remain at zero.

* The core quadcopter MATLAB model incorporates static parameters such as **weight**, **arm length**, and **number of rotors**, which are essential for emulating quadcopter dynamics.
* **Initial values** for angles, accelerations, and rotor speeds are provided as inputs to the model.
* The model then predicts the **roll, pitch, and yaw angles**, along with the **linear accelerations** in all directions.
* These predicted angles and accelerations are fed into the hovering control model, which calculates the required rotor angular speeds.
* The calculated rotor speeds are fed back into the quadcopter model, creating a **closed-loop iterative process** that continues throughout the simulation.
* The control team must generate the hovering model using the **MATLAB Real-Time Code Generator** to ensure real-time execution.
* Verification of the software is performed through **Software-in-the-Loop (SiL) testing**, validating the correctness and stability of the hovering control system.

**Team Android Application and Virtual Reality**

Visualize the quadcopter in **Google Cardboard VR** and enable flight control through head movements.

* **Head movement signals** are transmitted via **UDP** to the quadcopter.
* The virtual reality device used is an **Android smartphone** equipped with **Google Cardboard**.
* A dedicated Google Cardboard application will be developed using **Unreal Engine 4** and the **Google VR Plugin**.
* The system can later be adapted for other VR platforms such as **Oculus Rift** or **HTC Vive**.
* Communication between the smartphone, the **Simulink simulation**, and eventually the real quadcopter is established through **UDP protocols**.

**Team Web Application and Database Management**

1. **Web Application Team**
   * Responsible for overseeing the overall progress of the project.
   * Key tasks include:
     * Monitoring project milestones and deliverables.
     * Maintaining documentation.
     * Defining and managing the team structure.
     * Tracking progress and ensuring deadlines are met.
     * Providing an easy-to-use, login-based website developed in **PHP** for project access and coordination.
2. **Database Management Team**
   * Handles all tasks related to data storage and retrieval.
   * Responsibilities include:
     * Collecting and organizing data in a **SQL database**.
       * Developing SQL commands that can be executed from the **Android application** to control the quadcopter.

## Interfaces

This section outlines the key interfaces between the control application and two major system components: the embedded software and the virtual reality environment. These interfaces are essential for validating and operating the quadcopter system in both simulated and real-world conditions.

* Interface between Control Application and Embedded Software
* Interface between Control Application and Virtual Reality

**Interfaces Between Control Application and System Components**

Even with the availability of the Raspberry Pi and control simulations, the physical quadcopter body (or complete vehicle) may not be accessible for testing. While this is not a limitation in our current setup, Tier II suppliers often face delays in receiving the actual hardware. Therefore, we assume the quadcopter body is currently unavailable.

To validate the embedded software without the physical plant (in this case, the quadcopter), we employ **Hardware-in-the-Loop (HiL) testing**. This method ensures that the communication between the embedded environment and the control application is functioning correctly.

**Interface Between Control Application and Virtual Reality**

The MATLAB-based **Hovering@Home** model is actively running and integrates with the Virtual Reality system. In this setup, the quadcopter's position is controlled by head movements captured by the VR team. The target hovering position is always at coordinates (0, 0, 0) with an altitude of 1 meter.

Any external disturbance—such as a physical push or wind—should trigger the quadcopter to autonomously return to its default position. To ensure this behavior, the VR team must develop a **verification software**. One of its key use cases involves altering the quadcopter’s (x, y, z) position and validating whether the system correctly recalculates and restores it to (0, 0, 0). These positional changes should be **visually represented in a 3D environment** for effective analysis.

## **Repositories and Submodules**

Disclaimer: Software has been written by students of various batches under supervision of Prof. Friedrich and Lecturer M Sc. Vikas Agrawal. Students are free to contact me, if they would like their names to be publically visible.

The project is a combination of following respositores

<table data-view="cards"><thead><tr><th align="center"></th><th data-type="content-ref"></th><th data-hidden data-card-cover data-type="image">Cover image</th></tr></thead><tbody><tr><td align="center">Embedded</td><td><a href="readme-embedded.md">readme-embedded.md</a></td><td><a href="https://images.unsplash.com/photo-1610812387871-806d3db9f5aa?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwxfHxSYXNwYmVycnklMjBQSXxlbnwwfHx8fDE3NjUwMTk5NzF8MA&#x26;ixlib=rb-4.1.0&#x26;q=85">https://images.unsplash.com/photo-1610812387871-806d3db9f5aa?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwxfHxSYXNwYmVycnklMjBQSXxlbnwwfHx8fDE3NjUwMTk5NzF8MA&#x26;ixlib=rb-4.1.0&#x26;q=85</a></td></tr><tr><td align="center">Realtime Kernel</td><td><a href="readme-kernel.md">readme-kernel.md</a></td><td><a href="https://images.unsplash.com/photo-1629654291663-b91ad427698f?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw1fHxMaW51eHxlbnwwfHx8fDE3NjUwMTk5ODB8MA&#x26;ixlib=rb-4.1.0&#x26;q=85">https://images.unsplash.com/photo-1629654291663-b91ad427698f?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw1fHxMaW51eHxlbnwwfHx8fDE3NjUwMTk5ODB8MA&#x26;ixlib=rb-4.1.0&#x26;q=85</a></td></tr><tr><td align="center">Matlab Control Simulation</td><td><a href="readme-simulation.md">readme-simulation.md</a></td><td><a href="https://images.unsplash.com/photo-1580642135909-a59e2b8805c6?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw2fHxGbGlnaHQlMjBjb250cm9sfGVufDB8fHx8MTc2NTAyMDA2MXww&#x26;ixlib=rb-4.1.0&#x26;q=85">https://images.unsplash.com/photo-1580642135909-a59e2b8805c6?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw2fHxGbGlnaHQlMjBjb250cm9sfGVufDB8fHx8MTc2NTAyMDA2MXww&#x26;ixlib=rb-4.1.0&#x26;q=85</a></td></tr><tr><td align="center">Android Application</td><td><a href="readme-android.md">readme-android.md</a></td><td><a href="https://images.unsplash.com/photo-1607252650355-f7fd0460ccdb?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwxfHxhbmRyb2lkfGVufDB8fHx8MTc2NTAyMDEzNHww&#x26;ixlib=rb-4.1.0&#x26;q=85">https://images.unsplash.com/photo-1607252650355-f7fd0460ccdb?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwxfHxhbmRyb2lkfGVufDB8fHx8MTc2NTAyMDEzNHww&#x26;ixlib=rb-4.1.0&#x26;q=85</a></td></tr><tr><td align="center">Virtual Reality</td><td><a href="readme-virtual-reality.md">readme-virtual-reality.md</a></td><td><a href="https://images.unsplash.com/photo-1593508512255-86ab42a8e620?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwzfHxWaXJ0dWFsJTIwUmVhbGl0eXxlbnwwfHx8fDE3NjUwMjAxNTN8MA&#x26;ixlib=rb-4.1.0&#x26;q=85">https://images.unsplash.com/photo-1593508512255-86ab42a8e620?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwzfHxWaXJ0dWFsJTIwUmVhbGl0eXxlbnwwfHx8fDE3NjUwMjAxNTN8MA&#x26;ixlib=rb-4.1.0&#x26;q=85</a></td></tr><tr><td align="center">Database</td><td><a href="readme-database.md">readme-database.md</a></td><td><a href="https://images.unsplash.com/photo-1529078155058-5d716f45d604?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw2fHxEYXRhJTIwY29sbGVjdGlvbnxlbnwwfHx8fDE3NjUwMjc5NTJ8MA&#x26;ixlib=rb-4.1.0&#x26;q=85">https://images.unsplash.com/photo-1529078155058-5d716f45d604?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw2fHxEYXRhJTIwY29sbGVjdGlvbnxlbnwwfHx8fDE3NjUwMjc5NTJ8MA&#x26;ixlib=rb-4.1.0&#x26;q=85</a></td></tr><tr><td align="center">Website</td><td><a href="readme-web-development.md">readme-web-development.md</a></td><td><a href="https://images.unsplash.com/photo-1573867639040-6dd25fa5f597?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw4fHx3ZWJzaXRlfGVufDB8fHx8MTc2NTAyNzkyNHww&#x26;ixlib=rb-4.1.0&#x26;q=85">https://images.unsplash.com/photo-1573867639040-6dd25fa5f597?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw4fHx3ZWJzaXRlfGVufDB8fHx8MTc2NTAyNzkyNHww&#x26;ixlib=rb-4.1.0&#x26;q=85</a></td></tr><tr><td align="center">Visualization</td><td><a href="readme-visualization.md">readme-visualization.md</a></td><td><a href="https://images.unsplash.com/photo-1535016120720-40c646be5580?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwxfHx2aXN1YWx8ZW58MHx8fHwxNzY1MDYwOTA2fDA&#x26;ixlib=rb-4.1.0&#x26;q=85">https://images.unsplash.com/photo-1535016120720-40c646be5580?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwxfHx2aXN1YWx8ZW58MHx8fHwxNzY1MDYwOTA2fDA&#x26;ixlib=rb-4.1.0&#x26;q=85</a></td></tr></tbody></table>



####
