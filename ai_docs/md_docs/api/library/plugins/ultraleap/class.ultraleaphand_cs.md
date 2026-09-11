# Unigine::Plugins::UltraleapHand Class (CS)


> **Notice:** [Ultraleap](../../../../code/plugins/ultraleap/index_cs.md) plugin must be loaded.


[Hands](../../../../code/plugins/ultraleap/index_cs.md#hands) are the main entity tracked by the Ultraleap controller. The controller maintains an inner model of the human hand and validates the data from its sensors against this model. This allows the controller to track finger positions even when a finger is not completely visible.


> **Notice:** It is possible for movement or changes in position to be lost when a finger is behind or directly in front of the hand (from the point of view of the controller).


The Ultraleap software matches the internal model against the existing data. In some cases, the software can make an incorrect match � for example, identifying a right hand as a left hand.


The *Hand* class represents a physical hand detected by the Leap and provides access to its attributes describing the hand position, orientation, and movement.


## UltraleapHand Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **LEFT** = 0 | Left hand. |
| **RIGHT** = 1 | Right hand. |
| **NUM_TYPES** = 2 | Total number of hand types. |

### Properties

## 🔒︎ UltraleapHand.TYPE Type

The type of the hand. One of the [TYPE_*](#TYPE_LEFT) values.
## 🔒︎ bool IsVisible

The value indicating if the hand is visible to the Ultraleap Controller.
## 🔒︎ long VisibleTime

The duration of time this hand has been visible to the Ultraleap Controller.
## 🔒︎ float PinchDistance

The distance between the thumb and index finger of a pinch hand pose. The distance is computed by looking at the shortest distance between the last 2 phalanges of the thumb and those of the index finger. This pinch measurement only takes thumb and index finger into account.
## 🔒︎ float PinchStrength

The holding strength of a pinch hand pose. The strength is 0 for an open hand, and blends to 1 when a pinching hand pose is recognized. Pinching can be done between the thumb and any other finger of the same hand.
## 🔒︎ float GrabStrength

The strength of a grab hand pose. The strength is 0 for an open hand, and blends to 1 when a grabbing hand pose is recognized.
## 🔒︎ float GrabAngle

The angle between the fingers and the hand of a grab hand pose. The angle is computed by looking at the angle between the direction of the 4 fingers and the direction of the hand. Thumb is not considered when computing the angle. The angle is 0 radian for an open hand, and reaches π radians when the pose is a tight fist.
## 🔒︎ double PalmWidth

The width of the palm when the hand is in a flat position, in meters.
## 🔒︎ vec3 PalmPosition

The coordinates of the position of the palm.
## 🔒︎ vec3 PalmStabilizedPosition

The modified palm position with some additional smoothing and stabilization applied. Smoothing and stabilization is performed in order to make this value more suitable for interaction with 2D content. The stabilized position lags behind the palm position by a variable amount, depending primarily on the speed of movement.
## 🔒︎ dvec3 PalmVelocity

The rate of change of the palm position, in m/s.
## 🔒︎ vec3 PalmNormal

The coordinates of the normal vector to the palm. If a hand is flat, this vector will point downward, or "out" of the front surface of your palm.
## 🔒︎ vec3 Direction

The normalized direction from the palm position toward the fingers.
## 🔒︎ UltraleapArm Arm

The object for the arm.
## 🔒︎ UltraleapFinger FingerThumb

The object for the thumb.
## 🔒︎ UltraleapFinger FingerIndex

The object for the index finger.
## 🔒︎ UltraleapFinger FingerMiddle

The object for the middle finger.
## 🔒︎ UltraleapFinger FingerRing

The object for the ring finger.
## 🔒︎ UltraleapFinger FingerPinky

The object for the pinky finger.
