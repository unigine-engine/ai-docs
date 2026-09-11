# Unigine::AnimationChannelFollowPath Class (CS)

**Inherits from:** AnimationChannel


This channel carries a trajectory and an aim at once: three curves give the position of a node over time, and the channel turns that node to face the direction it travels in. It writes both the position and the rotation of its target, which is what sets it apart from an [AnimationChannelVec3](../../../../api/library/animations/timeline/class.animationchannelvec3_cs.md) built on the same parameter.


The channel is created on a node position parameter. Everything the channels share, such as the binding, the custom name and the channel properties, comes from the [AnimationChannel](../../../../api/library/animations/timeline/class.animationchannel_cs.md) base class. In the [Sequencer](../../../../editor2/tools/sequencer/index.md) it is offered as the **Follow Path** row of the cinematic half of the channel picker, and it is also what a legacy `*.track` follow parameter becomes on conversion.


Where the trajectory does not move the node at all, there is no direction to face and the rotation is left untouched.


## AnimationChannelFollowPath Class

### Properties

## AnimationCurveScalar CurveX

The curve of the X component of the trajectory.
## AnimationCurveScalar CurveY

The curve of the Y component of the trajectory.
## AnimationCurveScalar CurveZ

The curve of the Z component of the trajectory.
## MathLib.AXIS ForwardAxis

The axis of the node that is turned along the direction of travel, one of the AXIS_X, AXIS_Y, AXIS_Z, AXIS_NX, AXIS_NY and AXIS_NZ values. The default is AXIS_Y, the forward axis of a node; a camera is aimed along AXIS_NZ.
## vec3 Up

The direction the node treats as up while it is aimed. The default is (0.0f, 0.0f, 1.0f). A stretch of the trajectory running straight along this vector leaves no side axis to build a rotation from: there the node keeps the rotation it already had rather than take a degenerate one.
## float Lookahead

The distance ahead in time, in seconds, at which the channel samples a second point of the trajectory to work out which way the node is going. The default is 0.0f, which stands for the smallest step the curve can tell apart, so the aim follows the instant tangent. A larger value averages the direction over the stretch ahead, which steadies a jittery trajectory and cuts the corners of a tight one.
### Members

---

## AnimationChannelFollowPath ( AnimParams.PARAM param )

Constructor. Creates a channel that follows a path written into the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.

## AnimationChannelFollowPath ( AnimParams.PARAM param , int param_index )

Constructor. Creates a channel that follows a path written into the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## void AssignFrom ( AnimationChannelFollowPath channel )

Copies the content of the specified channel into this one.
### Arguments

- *[AnimationChannelFollowPath](../../../../api/library/animations/timeline/class.animationchannelfollowpath_cs.md)* **channel** - Source channel to copy the content from.

## void AddValue ( float time , vec3 value , AnimationCurve.KEY_TYPE type = AnimationCurve::KEY_TYPE_LINEAR )

Adds a key to each of the three curves, putting the specified point of the trajectory at the given moment.
### Arguments

- *float* **time** - Moment the key is to sit at, in seconds.
- *vec3* **value** - Point of the trajectory to be held by the key.
- *[AnimationCurve.KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE)* **type** - Interpolation type of the key. The default value is [KEY_TYPE_LINEAR](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE_LINEAR).
