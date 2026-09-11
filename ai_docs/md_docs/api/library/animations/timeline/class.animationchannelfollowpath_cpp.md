# Unigine::AnimationChannelFollowPath Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationChannel


This channel carries a trajectory and an aim at once: three curves give the position of a node over time, and the channel turns that node to face the direction it travels in. It writes both the position and the rotation of its target, which is what sets it apart from an [AnimationChannelVec3](../../../../api/library/animations/timeline/class.animationchannelvec3_cpp.md) built on the same parameter.


The channel is created on a node position parameter. Everything the channels share, such as the binding, the custom name and the channel properties, comes from the [AnimationChannel](../../../../api/library/animations/timeline/class.animationchannel_cpp.md) base class. In the [Sequencer](../../../../editor2/tools/sequencer/index.md) it is offered as the **Follow Path** row of the cinematic half of the channel picker, and it is also what a legacy `*.track` follow parameter becomes on conversion.


Where the trajectory does not move the node at all, there is no direction to face and the rotation is left untouched.


## AnimationChannelFollowPath Class

### Members

## void setCurveX ( const Ptr < AnimationCurveScalar >& x )

Sets a new curve of the X component of the trajectory.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveScalar](../../../../api/library/animations/timeline/class.animationcurvescalar_cpp.md)>&* **x** - The curve of the X component of the trajectory

## Ptr < AnimationCurveScalar > getCurveX () const

Returns the current curve of the X component of the trajectory.
### Return value

Current curve of the X component of the trajectory
## void setCurveY ( const Ptr < AnimationCurveScalar >& y )

Sets a new curve of the Y component of the trajectory.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveScalar](../../../../api/library/animations/timeline/class.animationcurvescalar_cpp.md)>&* **y** - The curve of the Y component of the trajectory

## Ptr < AnimationCurveScalar > getCurveY () const

Returns the current curve of the Y component of the trajectory.
### Return value

Current curve of the Y component of the trajectory
## void setCurveZ ( const Ptr < AnimationCurveScalar >& z )

Sets a new curve of the Z component of the trajectory.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveScalar](../../../../api/library/animations/timeline/class.animationcurvescalar_cpp.md)>&* **z** - The curve of the Z component of the trajectory

## Ptr < AnimationCurveScalar > getCurveZ () const

Returns the current curve of the Z component of the trajectory.
### Return value

Current curve of the Z component of the trajectory
## void setForwardAxis ( const MathLib::AXIS& axis )

Sets a new axis of the node that is turned along the direction of travel, one of the AXIS_X, AXIS_Y, AXIS_Z, AXIS_NX, AXIS_NY and AXIS_NZ values. The default is AXIS_Y, the forward axis of a node; a camera is aimed along AXIS_NZ.
### Arguments

- *const MathLib::AXIS&* **axis** - The axis of the node turned along the direction of travel

## MathLib::AXIS getForwardAxis () const

Returns the current axis of the node that is turned along the direction of travel, one of the AXIS_X, AXIS_Y, AXIS_Z, AXIS_NX, AXIS_NY and AXIS_NZ values. The default is AXIS_Y, the forward axis of a node; a camera is aimed along AXIS_NZ.
### Return value

Current axis of the node turned along the direction of travel
## void setUp ( const Math:: vec3 & up )

Sets a new direction the node treats as up while it is aimed. The default is (0.0f, 0.0f, 1.0f). A stretch of the trajectory running straight along this vector leaves no side axis to build a rotation from: there the node keeps the rotation it already had rather than take a degenerate one.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **up** - The direction the node treats as up while it is aimed

## Math:: vec3 getUp () const

Returns the current direction the node treats as up while it is aimed. The default is (0.0f, 0.0f, 1.0f). A stretch of the trajectory running straight along this vector leaves no side axis to build a rotation from: there the node keeps the rotation it already had rather than take a degenerate one.
### Return value

Current direction the node treats as up while it is aimed
## void setLookahead ( float lookahead )

Sets a new distance ahead in time, in seconds, at which the channel samples a second point of the trajectory to work out which way the node is going. The default is 0.0f, which stands for the smallest step the curve can tell apart, so the aim follows the instant tangent. A larger value averages the direction over the stretch ahead, which steadies a jittery trajectory and cuts the corners of a tight one.
### Arguments

- *float* **lookahead** - The distance ahead in time the direction of travel is taken from, in seconds

## float getLookahead () const

Returns the current distance ahead in time, in seconds, at which the channel samples a second point of the trajectory to work out which way the node is going. The default is 0.0f, which stands for the smallest step the curve can tell apart, so the aim follows the instant tangent. A larger value averages the direction over the stretch ahead, which steadies a jittery trajectory and cuts the corners of a tight one.
### Return value

Current distance ahead in time the direction of travel is taken from, in seconds
---

## AnimationChannelFollowPath ( AnimParams::PARAM param )

Constructor. Creates a channel that follows a path written into the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cpp.md) class rather than written out by hand.

## AnimationChannelFollowPath ( AnimParams::PARAM param , int param_index )

Constructor. Creates a channel that follows a path written into the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cpp.md) class rather than written out by hand.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## void assignFrom ( const Ptr < AnimationChannelFollowPath > & channel )

Copies the content of the specified channel into this one.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationChannelFollowPath](../../../../api/library/animations/timeline/class.animationchannelfollowpath_cpp.md)> &* **channel** - Source channel to copy the content from.

## void addValue ( float time , const Math:: Vec3 & value , AnimationCurve::KEY_TYPE type = AnimationCurve::KEY_TYPE_LINEAR )

Adds a key to each of the three curves, putting the specified point of the trajectory at the given moment.
### Arguments

- *float* **time** - Moment the key is to sit at, in seconds.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **value** - Point of the trajectory to be held by the key.
- *[AnimationCurve::KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE)* **type** - Interpolation type of the key. The default value is [KEY_TYPE_LINEAR](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_LINEAR).
