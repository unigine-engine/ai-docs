# Unigine::Plugins::ARTTracker Class (CS)

> **Notice:** This class is a singleton.


## ARTTracker Class

### Enums

## ERROR

| Name | Description |
|---|---|
| **NONE** = 0 | No error. |
| **TIMEOUT** = 1 | Timeout while receiving data. |
| **NET** = 2 | UDP receive error. |
| **PARSE** = 3 | Error in UDP packet. |

## DTRACKSDK

| Name | Description |
|---|---|
| **FLYSTICK_MAX_BUTTON** = 16 | FlyStick data: maximum number of buttons. |
| **FLYSTICK_MAX_JOYSTICK** = 8 | FlyStick data: maximum number of joystick values. |
| **MEATOOL_MAX_BUTTON** = 16 | Measurement tool data: maximum number of buttons. |
| **HAND_MAX_FINGER** = 5 | Fingertracking hand data: maximum number of fingers. |
| **HUMAN_MAX_JOINTS** = 200 | A.R.T human model (maximum number of joints + fingertracking). |

### Properties

## 🔒︎ ARTTracker.ERROR LastDataError

The data on the last received error.
## 🔒︎ int NumInertial

The Returns the number of all tracked standard 6DOF bodies (i.e. all 6DOF bodies except Flysticks, Measurement Tools, etc.) and all hybrid bodies.
## 🔒︎ int NumHuman

The number of human models.
## 🔒︎ int NumHand

The number of tracked hand bodies.
## 🔒︎ int NumMarker

The number of tracked additional Markers.
## 🔒︎ int NumMeaRef

The number of defined reference bodies of the Measurement Tool.
## 🔒︎ int NumMeaTool

The number of defined (calibrated) Measurement Tools.
## 🔒︎ int NumFlyStick

The number of defined (calibrated) Flystick bodies.
## 🔒︎ int NumBody

The number of DTrack bodies.
## 🔒︎ double TimeStamp

The time at the measurement of the current frame, i.e. the time when the infrared flash of the cameras is fired. the timestamp uses the internal clock of the controller, giving back the seconds (with an accuracy of 1μs) since 00:00 UTC (midnight). this implies that the timestamp value is reset to zero when passing midnight (UTC).
## 🔒︎ int FrameCounter

The frame counter (counting with synchronization frequency).
### Members

---

## bool Receive ( )

Receives and processes one DTrack data packet.
### Return value

true if a DTrack data packet is received successfully, otherwise false.
## int Init ( string ip = "192.168.1.100" , int port = 5000 )

Initializes communication with DTrack.
### Arguments

- *string* **ip** - DTrack IP address.
- *int* **port** - DTrack UDP port.

### Return value

1 if initialization was successful, otherwise 0.
## bool Start ( )

Starts communication with DTrack.
### Return value

true if communication started successfully, otherwise false.
## bool Stop ( )

Stops communication with DTrack.
### Return value

true if communication stopped successfully, otherwise false.
## int GetBodyID ( int index )

Returns DTrack body ID.
### Arguments

- *int* **index** - DTrack body index.

### Return value

DTrack body ID (starting from 0).
## double GetBodyQuality ( int index )

Returns the quality value of DTrack body, the value within the interval [0;1], or -1, if not tracked.
### Arguments

- *int* **index** - DTrack bodyindex.

### Return value

Quality, the value within the interval [0;1], or -1, if not tracked.
## dvec3 GetBodyLocation ( int index )

Returns the specified DTrack body location.
### Arguments

- *int* **index** - DTrack body index.

### Return value

Body location (in mm).
## dmat4 GetBodyRotation ( int index )

Returns the specified DTrack body rotation matrix.
### Arguments

- *int* **index** - DTrack body index.

### Return value

Body rotation matrix (column-wise).
## int GetFlyStickID ( int index )

Returns the specified Flystick ID.
### Arguments

- *int* **index** - Flystick body index.

### Return value

Flystick ID (starting from 0).
## double GetFlyStickQuality ( int index )

Returns the tracking quality value within the range [0; 1], or -1 if the Flystick is not tracked.
### Arguments

- *int* **index** - Flystick body index.

### Return value

Tracking quality value within the range [0; 1], or -1 if the Flystick is not tracked.
## int GetFlyStickNumButton ( int index )

Returns the number of available buttons and controllers for the indicated Flystick. Information about buttons and controllers is valid as long as the wireless transmission is active.
### Arguments

- *int* **index** - Flystick button index.

### Return value

Number of available buttons and controllers.
## int GetFlyStickButton ( int index , int button_index )

Returns the status of the given Flystick button.
### Arguments

- *int* **index** - Flystick index.
- *int* **button_index** - Flystick button index.

### Return value

Button state: 1 - if the button is pressed, 0 � if not pressed.
## int GetFlyStickNumJoyStick ( int index )

Returns the number of joystick values of a specified Flystick.
### Arguments

- *int* **index** - Flystick body index.

### Return value

Number of joystick values.
## double GetFlyStickJoyStick ( int index , int joystick_index )

Returns the joystick value.
### Arguments

- *int* **index** - Flystick body index.
- *int* **joystick_index** - Joystick index.

### Return value

Joystick value [-1;1]; 0 horizontal, 1 vertical.
## dvec3 GetFlyStickLocation ( int index )

Returns the Flystick body location (in mm).
### Arguments

- *int* **index** - Flystick body index.

### Return value

Body location (in mm).
## dmat4 GetFlyStickRotation ( int index )

Returns the FlyStick rotation matrix (column-wise).
### Arguments

- *int* **index** - Flystick body index.

### Return value

Rotation matrix (column-wise).
## int GetMeaToolID ( int index )

Returns the Measurement Tool ID (starting from 0).
### Arguments

- *int* **index** - Measurement Tool body index.

### Return value

Measurement Tool ID (starting from 0).
## double GetMeaToolQuality ( int index )

Returns the value specifying the measurement quality.
### Arguments

- *int* **index** - Measurement Tool index.

### Return value

1.0 if the target of the Measurement Tool is visible at the moment, or −1.0 if it is invisible.
## int GetMeaToolNumButton ( int index )

Returns the number of available buttons for the specified Measurement Tool.
### Arguments

- *int* **index** - Measurement Tool index.

### Return value

Number of available buttons.
## int GetMeaToolButton ( int index , int button_index )

Returns the button state for the specified Measurement Tool.
### Arguments

- *int* **index** - Measurement Tool index.
- *int* **button_index** - Index of the Measurement Tool button.

### Return value

Button state: 1 � pressed, 0 � not pressed.
## dvec3 GetMeaToolLocation ( int index )

Returns the Measurement Tool location.
### Arguments

- *int* **index** - Measurement Tool index.

### Return value

Location (in mm).
## dmat4 GetMeaToolRotation ( int index )

Returns the Measurement Tool rotation matrix.
### Arguments

- *int* **index** - Measurement Tool index.

### Return value

Rotation matrix (column-wise).
## double GetMeaToolTipRadius ( int index )

Returns the radius of the Measurement Tool tip sphere.
### Arguments

- *int* **index** - Measurement Tool index.

### Return value

Radius of the Measurement Tool tip sphere.
## dmat4 GetMeaToolCovariance ( int index )

Returns the covariance of the tool tip location, in mm2.
### Arguments

- *int* **index** - Measurement Tool index.

### Return value

Covariance matrix of the position of the tool tip.
## int GetMeaRefID ( int index )

Returns the ID of the reference body of the Measurement Tool.
### Arguments

- *int* **index** - Index of the reference body of the Measurement Tool.

### Return value

ID of the Measurement reference (starting with 0).
## double GetQuality ( int index )

Returns the value specifying the measurement quality.
### Arguments

- *int* **index** - Index of the reference body of the Measurement Tool.

### Return value

1.0 if the target of the Measurement Tool is visible at the moment, or −1.0 if it is invisible.
## dvec3 GetMeaRefLocation ( int index )

Returns the position of the reference body of the Measurement Tool.
### Arguments

- *int* **index** - Index of the reference body of the Measurement Tool.

### Return value

Location coordinates.
## dmat4 GetMeaRefRotation ( int index )

Returns the rotation matrix of the reference body of the Measurement Tool.
### Arguments

- *int* **index** - Measurement Tool reference index.

### Return value

Rotation matrix.
## int GetMarkID ( int index )

Returns the marker ID number.
### Arguments

- *int* **index** - Marker index.

### Return value

ID number (id, starting with 1).
## double GetMarkQuality ( int index )

Returns the value specifying the measurement quality.
### Arguments

- *int* **index** - Marker index.

### Return value

Quality value.
## dvec3 GetMarkLocation ( int index )

Returns the marker location.
### Arguments

- *int* **index** - Marker index.

### Return value

Marker location (in mm).
## int GetHandID ( int index )

Returns the hand ID number.
### Arguments

- *int* **index** - Hand index.

### Return value

Hand ID number (starting with 0).
## double GetHandQuality ( int index )

Returns the value specifying the measurement quality.
### Arguments

- *int* **index** - Hand index.

### Return value

Quality value.
## int GetHandLeft ( int index )

Returns the value to distinguish between the left and right hand.
### Arguments

- *int* **index** - Hand index.

### Return value

The value to distinguish between the left (0) and right (1) hand.
## int GetHandNumFinger ( int index )

Returns the number of fingers for the specified hand. The maximum number of fingers is 5.
> **Notice:** Based on this number, each finger can be addressed using its index starting from the thumb � 0, index finger � 1, etc.


### Arguments

- *int* **index** - Hand index.

### Return value

Number of fingers.
## dvec3 GetHandLocation ( int index )

Returns location (in mm) of the specified hand.
### Arguments

- *int* **index** - Hand index.

### Return value

Hand location (in mm).
## dmat4 GetHandRotation ( int index )

Returns the rotation matrix of the specified hand.
### Arguments

- *int* **index** - Hand index.

### Return value

Hand rotation matrix (column-wise).
## dvec3 GetHandFingerLocation ( int index , int finger_index )

Returns the location (in mm) for the specified hand finger.
### Arguments

- *int* **index** - Hand index.
- *int* **finger_index** - [Index](#getHandNumFinger_int_int) of a finger.

### Return value

Finger location (in mm).
## dmat4 GetHandFingerRotation ( int index , int finger_index )

Returns the rotation matrix (column-wise) for the specified hand finger.
### Arguments

- *int* **index** - Hand index.
- *int* **finger_index** - [Index](#getHandNumFinger_int_int) of a finger.

### Return value

Finger rotation matrix (column-wise).
## double GetHandFingerTipRadius ( int index , int finger_index )

Returns the radius of the finger tip.
### Arguments

- *int* **index** - Hand index.
- *int* **finger_index** - [Index](#getHandNumFinger_int_int) of a finger.

### Return value

Radius of the finger tip.
## dvec3 GetHandFingerLengthPhalanx ( int index , int finger_index )

Returns the length of a all phalanxes or the specified finger.
### Arguments

- *int* **index** - Hand index.
- *int* **finger_index** - [Index](#getHandNumFinger_int_int) of a finger.

### Return value

Length of phalanxes in the order: outermost, middle, innermost.
## dvec2 GetHandFingerAnglePhalanx ( int index , int finger_index )

Returns the angles between the phalanxes of a finger.
### Arguments

- *int* **index** - Hand index.
- *int* **finger_index** - [Index](#getHandNumFinger_int_int) of a finger.

### Return value

Angles between phalanxes of a finger.
## int GetHumanID ( int index )

Returns the ID of the human model (starting with 0).
### Arguments

- *int* **index** - Human model index.

### Return value

ID of the human model.
## int GetHumanNumJoints ( int index )

Returns the number of joints of the human model.
### Arguments

- *int* **index** - Human model index.

### Return value

Number of joints of the human model.
## int GetHumanJointID ( int index , int joint_index )

Returns the ID of the joint (starting with 0).
### Arguments

- *int* **index** - Human model index.
- *int* **joint_index** - Index of the joint.

### Return value

ID of the joint.
## double GetHumanJointQuality ( int index , int joint_index )

Returns the tracking quality value within the range [0; 1], or -1 if the joint is not tracked.
### Arguments

- *int* **index** - Human model index.
- *int* **joint_index** - Index of the joint.

### Return value

Tracking quality value within the range [0; 1], or -1 if the joint is not tracked.
## dvec3 GetHumanJointLocation ( int index , int joint_index )

Returns the location of the joint (in mm).
### Arguments

- *int* **index** - Human model index.
- *int* **joint_index** - Index of the joint.

### Return value

Location of the joint (in mm).
## dvec3 GetHumanJointAngle ( int index , int joint_index )

Returns the angle of the selected joint in relation to the joint coordinate system.
### Arguments

- *int* **index** - Human model index.
- *int* **joint_index** - Index of the joint.

### Return value

Angle in relation to the joint coordinate system.
## dmat4 GetHumanJointRotation ( int index , int joint_index )

Returns the rotation matrix of the joint (column-wise) in relation to room coordinate system.
### Arguments

- *int* **index** - Human model index.
- *int* **joint_index** - Index of the joint.

### Return value

Rotation matrix of the joint (column-wise) in relation to room coordinate system.
## int GetInertialID ( int index )

Returns the ID number of the standard 6DOF body.
### Arguments

- *int* **index** - Standard 6DOF body index.

### Return value

Standard 6DOF body ID number (starting with 0).
## int GetInertialState ( int index )

Returns the data tracking status.
### Arguments

- *int* **index** - Standard 6DOF body index.

### Return value

Tracking status of the sensor:
- 0 � no tracking.
- 1 � inertial tracking.
- 2 � optical tracking.


## double GetInertialError ( int index )

Returns the current drift error estimation, in degrees, estimate rising by 10 degree per minute when tracking inertially.
### Arguments

- *int* **index** - Standard 6DOF body index.

### Return value


- For the [inertial state](#getInertialState_int_int) 1: current drift error estimation, in degrees [0;360].
- For the [inertial states](#getInertialState_int_int) 0 and 2: 0.


## dvec3 GetInertialLocation ( int index )

Returns the position (in mm) of the Body.
### Arguments

- *int* **index** - Standard 6DOF body index.

### Return value

Position of the Body.
## dmat4 GetInertialRotation ( int index )

Returns the rotation matrix of the Body's orientation.
### Arguments

- *int* **index** - Standard 6DOF body index.

### Return value

Rotation matrix (column-wise) of the Body's orientation.
