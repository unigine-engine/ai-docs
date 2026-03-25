# Unigine::Plugins::UltraleapHand Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


> **Notice:** [Ultraleap](../../../../code/plugins/ultraleap/index_usc.md) plugin must be loaded.


[Hands](../../../../code/plugins/ultraleap/index_usc.md#hands) are the main entity tracked by the Ultraleap controller. The controller maintains an inner model of the human hand and validates the data from its sensors against this model. This allows the controller to track finger positions even when a finger is not completely visible.


> **Notice:** It is possible for movement or changes in position to be lost when a finger is behind or directly in front of the hand (from the point of view of the controller).


The Ultraleap software matches the internal model against the existing data. In some cases, the software can make an incorrect match – for example, identifying a right hand as a left hand.


The Hand class represents a physical hand detected by the Leap and provides access to its attributes describing the hand position, orientation, and movement.


## UltraleapHand Class

### Members

---

## int getType ( )

Returns the type of the hand.
### Return value

The type of the hand:
- 0 - left hand
- 1 - right hand


## int isVisible ( )

Returns a value indicating if the hand is visible to the Ultraleap Controller.
### Return value

**1** if the hand is visible; otherwise, **0**.
## long getVisibleTime ( )

The duration of time this Hand has been visible to the Ultraleap Controller.
### Return value

The duration of time this Hand has been visible to the Ultraleap Controller.
## float getPinchDistance ( )

Returns the distance between the thumb and index finger of a pinch hand pose. The distance is computed by looking at the shortest distance between the last 2 phalanges of the thumb and those of the index finger. This pinch measurement only takes thumb and index finger into account.
### Return value

The distance between the thumb and index finger of a pinch hand pose.
## float getPinchStrength ( )

Returns the holding strength of a pinch hand pose. The strength is zero for an open hand, and blends to one when a pinching hand pose is recognized. Pinching can be done between the thumb and any other finger of the same hand.
### Return value

The holding strength of a pinch hand pose: 0 for an open hand, and blends to 1 when a pinching hand pose is recognized.
## float getGrabStrength ( )

The strength of a grab hand pose. The strength is zero for an open hand, and blends to one when a grabbing hand pose is recognized.
### Return value

The strength of a grab hand pose: 0 for an open hand, and blends to 1 when a grabbing hand pose is recognized.
## float getGrabAngle ( )

The angle between the fingers and the hand of a grab hand pose. The angle is computed by looking at the angle between the direction of the 4 fingers and the direction of the hand. Thumb is not considered when computing the angle. The angle is 0 radian for an open hand, and reaches pi radians when the pose is a tight fist.
### Return value

The angle between the fingers and the hand of a grab hand pose: 0 radian for an open hand, and reaches π radians when the pose is a tight fist.
## double getPalmWidth ( )

Returns the width of the palm when the hand is in a flat position, in meters.
### Return value

The width of the palm when the hand is in a flat position, in meters.
## Vec3 getPalmPosition ( )

Returns the coordinates of the position of the palm.
### Return value

The coordinates of the position of the palm.
## Vec3 getPalmStabilizedPosition ( )

Returns the modified palm position with some additional smoothing and stabilization applied. Smoothing and stabilization is performed in order to make this value more suitable for interaction with 2D content. The stabilized position lags behind the palm position by a variable amount, depending primarily on the speed of movement.
### Return value

The coordinates of the modified palm position with some additional smoothing and stabilization applied.
## dvec3 getPalmVelocity ( )

Returns the rate of change of the palm position, in m/s.
### Return value

The rate of change of the palm position, in m/s.
## vec3 getPalmNormal ( )

Returns the coordinates of the normal vector to the palm. If a hand is flat, this vector will point downward, or "out" of the front surface of your palm.
### Return value

The coordinates of the normal vector to the palm.
## vec3 getDirection ( )

Returns the normalized direction from the palm position toward the fingers.
### Return value

The normalized direction from the palm position toward the fingers.
## UltraleapArm getArm ( )

Returns the object for the arm.
### Return value

The object for the arm.
## UltraleapFinger getFingerThumb ( )

Returns the object for the thumb.
### Return value

The object for the thumb.
## UltraleapFinger getFingerIndex ( )

Returns the object for the index finger.
### Return value

The object for the index finger.
## UltraleapFinger getFingerMiddle ( )

Returns the object for the middle finger.
### Return value

The object for the middle finger.
## UltraleapFinger getFingerRing ( )

Returns the object for the ring finger.
### Return value

The object for the ring finger.
## UltraleapFinger getFingerPinky ( )

Returns the object for the pinky finger.
### Return value

The object for the pinky finger.
