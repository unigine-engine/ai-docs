# Unigine::Plugins::ARTTracker Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


## ARTTracker Class

### Members

## getLastDataError () const

Returns the current data on the last received error.
### Return value

Current Last received error, one of the [A_R_T_TRACKER_ERROR_](#ERROR_NONE) values.
## int getNumInertial () const

Returns the current Returns the number of all tracked standard 6DOF bodies (i.e. all 6DOF bodies except Flysticks, Measurement Tools, etc.) and all hybrid bodies.
### Return value

Current number of all tracked standard 6DOF bodies and all hybrid bodies.
## int getNumHuman () const

Returns the current number of human models.
### Return value

Current number of human models.
## int getNumHand () const

Returns the current number of tracked hand bodies.
### Return value

Current number of tracked hand bodies.
## int getNumMarker () const

Returns the current number of tracked additional Markers.
### Return value

Current number of additional Marker bodies.
## int getNumMeaRef () const

Returns the current number of defined reference bodies of the Measurement Tool.
### Return value

Current number of defined reference bodies of the Measurement Tool.
## int getNumMeaTool () const

Returns the current number of defined (calibrated) Measurement Tools.
### Return value

Current number of defined (calibrated) Measurement Tools.
## int getNumFlyStick () const

Returns the current number of defined (calibrated) Flystick bodies.
### Return value

Current number of Flystick bodies.
## int getNumBody () const

Returns the current number of DTrack bodies.
### Return value

Current number of defined (calibrated) DTrack bodies.
## double getTimeStamp () const

Returns the current time at the measurement of the current frame, i.e. the time when the infrared flash of the cameras is fired. the timestamp uses the internal clock of the controller, giving back the seconds (with an accuracy of 1μs) since 00:00 UTC (midnight). this implies that the timestamp value is reset to zero when passing midnight (UTC).
### Return value

Current time at the measurement of the current frame.
## int getFrameCounter () const

Returns the current frame counter (counting with synchronization frequency).
### Return value

Current frame counter value (counting with synchronization frequency).
---

## int engine.dtrack. receive ( )

Receives and processes one DTrack data packet.
### Return value

**1** if a DTrack data packet is received successfully, otherwise **0**.
## int engine.dtrack. init ( string ip = "192.168.1.100" , int port = 5000 )

Initializes communication with DTrack.
### Arguments

- *string* **ip** - DTrack IP address.
- *int* **port** - DTrack UDP port.

### Return value

1 if initialization was successful, otherwise 0.
## int engine.dtrack. start ( )

Starts communication with DTrack.
### Return value

**1** if communication started successfully, otherwise **0**.
## int engine.dtrack. stop ( )

Stops communication with DTrack.
### Return value

**1** if communication stopped successfully, otherwise **0**.
## int engine.dtrack. getBodyID ( int index )

Returns DTrack body ID.
### Arguments

- *int* **index** - DTrack body index.

### Return value

DTrack body ID (starting from 0).
## double engine.dtrack. getBodyQuality ( int index )

Returns the quality value of DTrack body, the value within the interval [0;1], or -1, if not tracked.
### Arguments

- *int* **index** - DTrack bodyindex.

### Return value

Quality, the value within the interval [0;1], or -1, if not tracked.
## dvec3 engine.dtrack. getBodyLocation ( int index )

Returns the specified DTrack body location.
### Arguments

- *int* **index** - DTrack body index.

### Return value

Body location (in mm).
## dmat4 engine.dtrack. getBodyRotation ( int index )

Returns the specified DTrack body rotation matrix.
### Arguments

- *int* **index** - DTrack body index.

### Return value

Body rotation matrix (column-wise).
## int engine.dtrack. getFlyStickID ( int index )

Returns the specified Flystick ID.
### Arguments

- *int* **index** - Flystick body index.

### Return value

Flystick ID (starting from 0).
## double engine.dtrack. getFlyStickQuality ( int index )

Returns the tracking quality value within the range [0; 1], or -1 if the Flystick is not tracked.
### Arguments

- *int* **index** - Flystick body index.

### Return value

Tracking quality value within the range [0; 1], or -1 if the Flystick is not tracked.
## int engine.dtrack. getFlyStickNumButton ( int index )

Returns the number of available buttons and controllers for the indicated Flystick. Information about buttons and controllers is valid as long as the wireless transmission is active.
### Arguments

- *int* **index** - Flystick button index.

### Return value

Number of available buttons and controllers.
## int engine.dtrack. getFlyStickButton ( int index , int button_index )

Returns the status of the given Flystick button.
### Arguments

- *int* **index** - Flystick index.
- *int* **button_index** - Flystick button index.

### Return value

Button state: 1 - if the button is pressed, 0 � if not pressed.
## int engine.dtrack. getFlyStickNumJoyStick ( int index )

Returns the number of joystick values of a specified Flystick.
### Arguments

- *int* **index** - Flystick body index.

### Return value

Number of joystick values.
## double engine.dtrack. getFlyStickJoyStick ( int index , int joystick_index )

Returns the joystick value.
### Arguments

- *int* **index** - Flystick body index.
- *int* **joystick_index** - Joystick index.

### Return value

Joystick value [-1;1]; 0 horizontal, 1 vertical.
## dvec3 engine.dtrack. getFlyStickLocation ( int index )

Returns the Flystick body location (in mm).
### Arguments

- *int* **index** - Flystick body index.

### Return value

Body location (in mm).
## dmat4 engine.dtrack. getFlyStickRotation ( int index )

Returns the FlyStick rotation matrix (column-wise).
### Arguments

- *int* **index** - Flystick body index.

### Return value

Rotation matrix (column-wise).
## int engine.dtrack. getMeaToolID ( int index )

Returns the Measurement Tool ID (starting from 0).
### Arguments

- *int* **index** - Measurement Tool body index.

### Return value

Measurement Tool ID (starting from 0).
## double engine.dtrack. getMeaToolQuality ( int index )

Returns the value specifying the measurement quality.
### Arguments

- *int* **index** - Measurement Tool index.

### Return value

1.0 if the target of the Measurement Tool is visible at the moment, or −1.0 if it is invisible.
## int engine.dtrack. getMeaToolNumButton ( int index )

Returns the number of available buttons for the specified Measurement Tool.
### Arguments

- *int* **index** - Measurement Tool index.

### Return value

Number of available buttons.
## int engine.dtrack. getMeaToolButton ( int index , int button_index )

Returns the button state for the specified Measurement Tool.
### Arguments

- *int* **index** - Measurement Tool index.
- *int* **button_index** - Index of the Measurement Tool button.

### Return value

Button state: 1 � pressed, 0 � not pressed.
## dvec3 engine.dtrack. getMeaToolLocation ( int index )

Returns the Measurement Tool location.
### Arguments

- *int* **index** - Measurement Tool index.

### Return value

Location (in mm).
## dmat4 engine.dtrack. getMeaToolRotation ( int index )

Returns the Measurement Tool rotation matrix.
### Arguments

- *int* **index** - Measurement Tool index.

### Return value

Rotation matrix (column-wise).
## double engine.dtrack. getMeaToolTipRadius ( int index )

Returns the radius of the Measurement Tool tip sphere.
### Arguments

- *int* **index** - Measurement Tool index.

### Return value

Radius of the Measurement Tool tip sphere.
## dmat4 engine.dtrack. getMeaToolCovariance ( int index )

Returns the covariance of the tool tip location, in mm2.
### Arguments

- *int* **index** - Measurement Tool index.

### Return value

Covariance matrix of the position of the tool tip.
## int engine.dtrack. getMeaRefID ( int index )

Returns the ID of the reference body of the Measurement Tool.
### Arguments

- *int* **index** - Index of the reference body of the Measurement Tool.

### Return value

ID of the Measurement reference (starting with 0).
## double engine.dtrack. getQuality ( int index )

Returns the value specifying the measurement quality.
### Arguments

- *int* **index** - Index of the reference body of the Measurement Tool.

### Return value

1.0 if the target of the Measurement Tool is visible at the moment, or −1.0 if it is invisible.
## dvec3 engine.dtrack. getMeaRefLocation ( int index )

Returns the position of the reference body of the Measurement Tool.
### Arguments

- *int* **index** - Index of the reference body of the Measurement Tool.

### Return value

Location coordinates.
## dmat4 engine.dtrack. getMeaRefRotation ( int index )

Returns the rotation matrix of the reference body of the Measurement Tool.
### Arguments

- *int* **index** - Measurement Tool reference index.

### Return value

Rotation matrix.
## int engine.dtrack. getMarkID ( int index )

Returns the marker ID number.
### Arguments

- *int* **index** - Marker index.

### Return value

ID number (id, starting with 1).
## double engine.dtrack. getMarkQuality ( int index )

Returns the value specifying the measurement quality.
### Arguments

- *int* **index** - Marker index.

### Return value

Quality value.
## dvec3 engine.dtrack. getMarkLocation ( int index )

Returns the marker location.
### Arguments

- *int* **index** - Marker index.

### Return value

Marker location (in mm).
## int engine.dtrack. getHandID ( int index )

Returns the hand ID number.
### Arguments

- *int* **index** - Hand index.

### Return value

Hand ID number (starting with 0).
## double engine.dtrack. getHandQuality ( int index )

Returns the value specifying the measurement quality.
### Arguments

- *int* **index** - Hand index.

### Return value

Quality value.
## int engine.dtrack. getHandLeft ( int index )

Returns the value to distinguish between the left and right hand.
### Arguments

- *int* **index** - Hand index.

### Return value

The value to distinguish between the left (0) and right (1) hand.
## int engine.dtrack. getHandNumFinger ( int index )

Returns the number of fingers for the specified hand. The maximum number of fingers is 5.
> **Notice:** Based on this number, each finger can be addressed using its index starting from the thumb � 0, index finger � 1, etc.


### Arguments

- *int* **index** - Hand index.

### Return value

Number of fingers.
## dvec3 engine.dtrack. getHandLocation ( int index )

Returns location (in mm) of the specified hand.
### Arguments

- *int* **index** - Hand index.

### Return value

Hand location (in mm).
## dmat4 engine.dtrack. getHandRotation ( int index )

Returns the rotation matrix of the specified hand.
### Arguments

- *int* **index** - Hand index.

### Return value

Hand rotation matrix (column-wise).
## dvec3 engine.dtrack. getHandFingerLocation ( int index , int finger_index )

Returns the location (in mm) for the specified hand finger.
### Arguments

- *int* **index** - Hand index.
- *int* **finger_index** - [Index](#getHandNumFinger_int_int) of a finger.

### Return value

Finger location (in mm).
## dmat4 engine.dtrack. getHandFingerRotation ( int index , int finger_index )

Returns the rotation matrix (column-wise) for the specified hand finger.
### Arguments

- *int* **index** - Hand index.
- *int* **finger_index** - [Index](#getHandNumFinger_int_int) of a finger.

### Return value

Finger rotation matrix (column-wise).
## double engine.dtrack. getHandFingerTipRadius ( int index , int finger_index )

Returns the radius of the finger tip.
### Arguments

- *int* **index** - Hand index.
- *int* **finger_index** - [Index](#getHandNumFinger_int_int) of a finger.

### Return value

Radius of the finger tip.
## dvec3 engine.dtrack. getHandFingerLengthPhalanx ( int index , int finger_index )

Returns the length of a all phalanxes or the specified finger.
### Arguments

- *int* **index** - Hand index.
- *int* **finger_index** - [Index](#getHandNumFinger_int_int) of a finger.

### Return value

Length of phalanxes in the order: outermost, middle, innermost.
## dvec2 engine.dtrack. getHandFingerAnglePhalanx ( int index , int finger_index )

Returns the angles between the phalanxes of a finger.
### Arguments

- *int* **index** - Hand index.
- *int* **finger_index** - [Index](#getHandNumFinger_int_int) of a finger.

### Return value

Angles between phalanxes of a finger.
## int engine.dtrack. getHumanID ( int index )

Returns the ID of the human model (starting with 0).
### Arguments

- *int* **index** - Human model index.

### Return value

ID of the human model.
## int engine.dtrack. getHumanNumJoints ( int index )

Returns the number of joints of the human model.
### Arguments

- *int* **index** - Human model index.

### Return value

Number of joints of the human model.
## int engine.dtrack. getHumanJointID ( int index , int joint_index )

Returns the ID of the joint (starting with 0).
### Arguments

- *int* **index** - Human model index.
- *int* **joint_index** - Index of the joint.

### Return value

ID of the joint.
## double engine.dtrack. getHumanJointQuality ( int index , int joint_index )

Returns the tracking quality value within the range [0; 1], or -1 if the joint is not tracked.
### Arguments

- *int* **index** - Human model index.
- *int* **joint_index** - Index of the joint.

### Return value

Tracking quality value within the range [0; 1], or -1 if the joint is not tracked.
## dvec3 engine.dtrack. getHumanJointLocation ( int index , int joint_index )

Returns the location of the joint (in mm).
### Arguments

- *int* **index** - Human model index.
- *int* **joint_index** - Index of the joint.

### Return value

Location of the joint (in mm).
## dvec3 engine.dtrack. getHumanJointAngle ( int index , int joint_index )

Returns the angle of the selected joint in relation to the joint coordinate system.
### Arguments

- *int* **index** - Human model index.
- *int* **joint_index** - Index of the joint.

### Return value

Angle in relation to the joint coordinate system.
## dmat4 engine.dtrack. getHumanJointRotation ( int index , int joint_index )

Returns the rotation matrix of the joint (column-wise) in relation to room coordinate system.
### Arguments

- *int* **index** - Human model index.
- *int* **joint_index** - Index of the joint.

### Return value

Rotation matrix of the joint (column-wise) in relation to room coordinate system.
## int engine.dtrack. getInertialID ( int index )

Returns the ID number of the standard 6DOF body.
### Arguments

- *int* **index** - Standard 6DOF body index.

### Return value

Standard 6DOF body ID number (starting with 0).
## int engine.dtrack. getInertialState ( int index )

Returns the data tracking status.
### Arguments

- *int* **index** - Standard 6DOF body index.

### Return value

Tracking status of the sensor:
- 0 � no tracking.
- 1 � inertial tracking.
- 2 � optical tracking.


## double engine.dtrack. getInertialError ( int index )

Returns the current drift error estimation, in degrees, estimate rising by 10 degree per minute when tracking inertially.
### Arguments

- *int* **index** - Standard 6DOF body index.

### Return value


- For the [inertial state](#getInertialState_int_int) 1: current drift error estimation, in degrees [0;360].
- For the [inertial states](#getInertialState_int_int) 0 and 2: 0.


## dvec3 engine.dtrack. getInertialLocation ( int index )

Returns the position (in mm) of the Body.
### Arguments

- *int* **index** - Standard 6DOF body index.

### Return value

Position of the Body.
## dmat4 engine.dtrack. getInertialRotation ( int index )

Returns the rotation matrix of the Body's orientation.
### Arguments

- *int* **index** - Standard 6DOF body index.

### Return value

Rotation matrix (column-wise) of the Body's orientation.
