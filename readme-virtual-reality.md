# README Virtual Reality

### Project to bring a Simulink-based quadrocopter model to Google Cardboard VR

#### Repository **:** [https://github.com/parabola-x2/Quadrocopter\_VirtualReality](https://github.com/parabola-x2/Quadrocopter_VirtualReality)

#### Description:

A quadrocopter-model based on MATLAB/Simulink will be used to show the behaviour of a quadrocopter in a virtual reality environment. The control of the object will be the movement of the head.<br>

The virtual reality device is a android smartphone with google cardboard. A google cardboard app will be developed with Unreal Engine 4 and the Google VR Plugin. This can be adapted to an Oculus Rift or HTC Vive device later.

The communication between the smartphone and the Simulink simulation goes via UDP communication.

#### Architecture:

<figure><img src=".gitbook/assets/Architecture1.png" alt=""><figcaption></figcaption></figure>

\-

#### Milestones and Tasks:

| **Tasks**              | **Details**                                                                | **Done?**                                                                                                                         |
| ---------------------- | -------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| C++ Model for Position | Create model to calculate position based on sensor data                    | This is done using blueprint in Unreal Engine, the accelerations is being received and using tick to calculate the velocity in 3D |
| UDP connection         | Receive data from Simulink model                                           | Done using python, can received data from any sender...                                                                           |
| UDP connection         | Send data to Simulink model                                                | In Progress...                                                                                                                    |
| UDP connection         | Control Simulink model from C++                                            | Frame format already defined and agreed with Simulink Team                                                                        |
| UDP connection         | Establish protocol based connection between Simulink model and C++ program | This is not overlapped with the previous tasks                                                                                    |
| UDP connection         | Receive data from the quadcopter                                           | C++ functions are provided by Markus, the integration to UE4 blueprint is in progress                                             |
| Android App            | Create first Android VR app running on a Smartphone (Unreal Engine 4)      | Done                                                                                                                              |
| Quadrocopter model     | Create new Quadrocopter model (CAD)                                        | Basic Model done, the model is created using unreal                                                                               |
| Quadrocopter model     | Include Quadrocopter model to VR app                                       | Basic Model done, including animations of the quadcopter propellers                                                               |
| UDP connection VR      | Establish communication between VR app(using C++) and Simulink             | In Progress...                                                                                                                    |
| Include C++ model      | Include the C++ model into the VR app                                      | In Progress...                                                                                                                    |
| ...                    | ---                                                                        |                                                                                                                                   |

### Unreal Model:

#### -Block Diagram-

<figure><img src=".gitbook/assets/Unreal_BlockDiagram.png" alt=""><figcaption></figcaption></figure>

The block diagram describes the architecture of the visual simulation of Unreal Engine 4. The environment(or level in Unreal Engine) contains a representation of the user, which will provide basic movements such as go forward, turn left, turn right... Beside that, the level also contains Actors, which is interactable objects. The interacting function such as collitions or control or user's actions will create an event that triggers the movement of the object according to physical principles.\
Moreover, Unreal can also send/receive UDP/TCP data packages from outside with the help of local C++ functions.

#### -Enviroment-

<figure><img src=".gitbook/assets/Unreal_EnvLevel.PNG" alt=""><figcaption></figcaption></figure>

The image shows how the environment looks like.

#### -Character-

<figure><img src=".gitbook/assets/Unreal_CharLevel.PNG" alt=""><figcaption></figcaption></figure>

The image shows how the environment looks like.

### Real Time Path Plot:

#### -Block Diagram-

<figure><img src=".gitbook/assets/RealTime_Path.PNG" alt=""><figcaption></figcaption></figure>

The block diagram depicts the architecture of the model for printing the current Quadracopter path.

The code is showed bellow:

<figure><img src=".gitbook/assets/PathPlot.png" alt=""><figcaption></figcaption></figure>

####

<figure><img src=".gitbook/assets/PathPlot_Header.png" alt=""><figcaption></figcaption></figure>

#### Build Info

Project created with Visual Studio 2013\
Packages: CppUnit - CppUnit test toolkit for C++\
Libraries: boost\_1\_63\_0 - For UDP Server and Client boost library is needed
