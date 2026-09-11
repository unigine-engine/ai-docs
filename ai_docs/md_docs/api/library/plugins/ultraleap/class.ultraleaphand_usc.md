# Unigine::Plugins::UltraleapHand Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


> **Notice:** [Ultraleap](../../../../code/plugins/ultraleap/index_usc.md) plugin must be loaded.


[Hands](../../../../code/plugins/ultraleap/index_usc.md#hands) are the main entity tracked by the Ultraleap controller. The controller maintains an inner model of the human hand and validates the data from its sensors against this model. This allows the controller to track finger positions even when a finger is not completely visible.


> **Notice:** It is possible for movement or changes in position to be lost when a finger is behind or directly in front of the hand (from the point of view of the controller).


The Ultraleap software matches the internal model against the existing data. In some cases, the software can make an incorrect match � for example, identifying a right hand as a left hand.


The *Hand* class represents a physical hand detected by the Leap and provides access to its attributes describing the hand position, orientation, and movement.


## UltraleapHand Class

### Members

## int getType () const

Returns the current type of the hand. One of the [TYPE_*](#TYPE_LEFT) values.
### Return value

Current type of the hand
## int isVisible () const

Returns the current value indicating if the hand is visible to the Ultraleap Controller.
### Return value

Current the hand is visible to the Ultraleap Controller
## long getVisibleTime () const

Returns the current duration of time this hand has been visible to the Ultraleap Controller.
### Return value

Current duration of time this hand has been visible to the Ultraleap Controller
## float getPinchDistance () const

Returns the current distance between the thumb and index finger of a pinch hand pose. The distance is computed by looking at the shortest distance between the last 2 phalanges of the thumb and those of the index finger. This pinch measurement only takes thumb and index finger into account.
### Return value

Current distance between the thumb and index finger of a pinch hand pose
## float getPinchStrength () const

Returns the current holding strength of a pinch hand pose. The strength is 0 for an open hand, and blends to 1 when a pinching hand pose is recognized. Pinching can be done between the thumb and any other finger of the same hand.
### Return value

Current holding strength of a pinch hand pose
## float getGrabStrength () const

Returns the current strength of a grab hand pose. The strength is 0 for an open hand, and blends to 1 when a grabbing hand pose is recognized.
### Return value

Current strength of a grab hand pose
## float getGrabAngle () const

Returns the current angle between the fingers and the hand of a grab hand pose. The angle is computed by looking at the angle between the direction of the 4 fingers and the direction of the hand. Thumb is not considered when computing the angle. The angle is 0 radian for an open hand, and reaches π radians when the pose is a tight fist.
### Return value

Current angle between the fingers and the hand of a grab hand pose
## double getPalmWidth () const

Returns the current width of the palm when the hand is in a flat position, in meters.
### Return value

Current width of the palm when the hand is in a flat position, in meters
## Vec3 getPalmPosition () const

Returns the current coordinates of the position of the palm.
### Return value

Current coordinates of the position of the palm
## Vec3 getPalmStabilizedPosition () const

Returns the current modified palm position with some additional smoothing and stabilization applied. Smoothing and stabilization is performed in order to make this value more suitable for interaction with 2D content. The stabilized position lags behind the palm position by a variable amount, depending primarily on the speed of movement.
### Return value

Current modified palm position with some additional smoothing and stabilization applied
## dvec3 getPalmVelocity () const

Returns the current rate of change of the palm position, in m/s.
### Return value

Current rate of change of the palm position, in m/s
## vec3 getPalmNormal () const

Returns the current coordinates of the normal vector to the palm. If a hand is flat, this vector will point downward, or "out" of the front surface of your palm.
### Return value

Current coordinates of the normal vector to the palm
## vec3 getDirection () const

Returns the current normalized direction from the palm position toward the fingers.
### Return value

Current normalized direction from the palm position toward the fingers
## UltraleapArm getArm () const

Returns the current object for the arm.
### Return value

Current object for the arm
## UltraleapFinger getFingerThumb () const

Returns the current object for the thumb.
### Return value

Current object for the thumb
## UltraleapFinger getFingerIndex () const

Returns the current object for the index finger.
### Return value

Current object for the index finger
## UltraleapFinger getFingerMiddle () const

Returns the current object for the middle finger.
### Return value

Current object for the middle finger
## UltraleapFinger getFingerRing () const

Returns the current object for the ring finger.
### Return value

Current object for the ring finger
## UltraleapFinger getFingerPinky () const

Returns the current object for the pinky finger.
### Return value

Current object for the pinky finger
