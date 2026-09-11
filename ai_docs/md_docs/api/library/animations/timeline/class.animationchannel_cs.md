# Unigine::AnimationChannel Class (CS)


A channel is one animated thing inside an [AnimationSequence](../../../../api/library/animations/timeline/class.animationsequence_cs.md): one parameter, one row of the timeline, one set of keys. Everything the [Sequencer](../../../../editor2/tools/sequencer/index.md) shows as a row is a channel, whether it drives a number, a whole skeleton, a sound, an event or a nested sequence. This class is the base of them all and holds what they share: which parameter is animated, what it is bound to, where the keys sit in time, and how the row is shown.


A channel says *what* is animated; a [binding](../../../../api/library/animations/timeline/class.animationbind_cs.md) says *which object* it is animated on. A channel with no binding is a global one, such as a console command or a render setting, and drives no particular object.


Keys are reached in two ways. The typed subclasses give values of their own type, while this class gives type-agnostic access by component: components come first as the axes of the channel curve, and the playback property lanes follow. A channel of a certain type also carries clips, which are blocks of content placed along the timeline with their own weight and speed.


A channel taken from a sequence is a copy. Edit it and put it back with *[UpdateChannel()](../../../../api/library/animations/timeline/class.animationsequence_cs.md#updateChannel_AnimationChannel_int)*, which matches it to the stored one by ID.


## AnimationChannel Class

### Enums

## TYPE

Channel type. It tells what kind of value the channel animates and which subclass it is.
| Name | Description |
|---|---|
| **ANIMATION_CHANNEL** = 0 | Base channel type. It animates nothing on its own and stands for a channel whose type is not set. |
| **ANIMATION_CHANNEL_INT** = 1 | Channel that animates an integer parameter (see the *[AnimationChannelInt](../../../../api/library/animations/timeline/class.animationchannelint_cs.md)* class). |
| **ANIMATION_CHANNEL_BOOL** = 2 | Channel that animates a boolean parameter (see the *[AnimationChannelBool](../../../../api/library/animations/timeline/class.animationchannelbool_cs.md)* class). |
| **ANIMATION_CHANNEL_QUAT** = 3 | Channel that animates an orientation (see the *[AnimationChannelQuat](../../../../api/library/animations/timeline/class.animationchannelquat_cs.md)* class). |
| **ANIMATION_CHANNEL_SCALAR** = 4 | Channel that animates a scalar parameter, which is a float or a double depending on the build (see the *[AnimationChannelScalar](../../../../api/library/animations/timeline/class.animationchannelscalar_cs.md)* class). |
| **ANIMATION_CHANNEL_FLOAT** = 5 | Channel that animates a float parameter (see the *[AnimationChannelFloat](../../../../api/library/animations/timeline/class.animationchannelfloat_cs.md)* class). |
| **ANIMATION_CHANNEL_DOUBLE** = 6 | Channel that animates a double parameter (see the *[AnimationChannelDouble](../../../../api/library/animations/timeline/class.animationchanneldouble_cs.md)* class). |
| **ANIMATION_CHANNEL_STRING** = 7 | Channel that animates a string parameter (see the *[AnimationChannelString](../../../../api/library/animations/timeline/class.animationchannelstring_cs.md)* class). |
| **ANIMATION_CHANNEL_UGUID** = 8 | Channel that animates an asset reference (see the *[AnimationChannelUGUID](../../../../api/library/animations/timeline/class.animationchanneluguid_cs.md)* class). |
| **ANIMATION_CHANNEL_IVEC2** = 9 | Channel that animates a two-component integer vector (see the *[AnimationChannelIVec2](../../../../api/library/animations/timeline/class.animationchannelivec2_cs.md)* class). |
| **ANIMATION_CHANNEL_IVEC3** = 10 | Channel that animates a three-component integer vector (see the *[AnimationChannelIVec3](../../../../api/library/animations/timeline/class.animationchannelivec3_cs.md)* class). |
| **ANIMATION_CHANNEL_IVEC4** = 11 | Channel that animates a four-component integer vector (see the *[AnimationChannelIVec4](../../../../api/library/animations/timeline/class.animationchannelivec4_cs.md)* class). |
| **ANIMATION_CHANNEL_VEC2** = 12 | Channel that animates a two-component scalar vector (see the *[AnimationChannelVec2](../../../../api/library/animations/timeline/class.animationchannelvec2_cs.md)* class). |
| **ANIMATION_CHANNEL_FVEC2** = 13 | Channel that animates a two-component float vector (see the *[AnimationChannelFVec2](../../../../api/library/animations/timeline/class.animationchannelfvec2_cs.md)* class). |
| **ANIMATION_CHANNEL_DVEC2** = 14 | Channel that animates a two-component double vector (see the *[AnimationChannelDVec2](../../../../api/library/animations/timeline/class.animationchanneldvec2_cs.md)* class). |
| **ANIMATION_CHANNEL_VEC3** = 15 | Channel that animates a three-component scalar vector (see the *[AnimationChannelVec3](../../../../api/library/animations/timeline/class.animationchannelvec3_cs.md)* class). |
| **ANIMATION_CHANNEL_FVEC3** = 16 | Channel that animates a three-component float vector (see the *[AnimationChannelFVec3](../../../../api/library/animations/timeline/class.animationchannelfvec3_cs.md)* class). |
| **ANIMATION_CHANNEL_DVEC3** = 17 | Channel that animates a three-component double vector (see the *[AnimationChannelDVec3](../../../../api/library/animations/timeline/class.animationchanneldvec3_cs.md)* class). |
| **ANIMATION_CHANNEL_VEC4** = 18 | Channel that animates a four-component scalar vector (see the *[AnimationChannelVec4](../../../../api/library/animations/timeline/class.animationchannelvec4_cs.md)* class). |
| **ANIMATION_CHANNEL_FVEC4** = 19 | Channel that animates a four-component float vector (see the *[AnimationChannelFVec4](../../../../api/library/animations/timeline/class.animationchannelfvec4_cs.md)* class). |
| **ANIMATION_CHANNEL_DVEC4** = 20 | Channel that animates a four-component double vector (see the *[AnimationChannelDVec4](../../../../api/library/animations/timeline/class.animationchanneldvec4_cs.md)* class). |
| **ANIMATION_CHANNEL_NODE** = 21 | Channel that animates a node reference, which is how a camera cut switches the shot (see the *[AnimationChannelNode](../../../../api/library/animations/timeline/class.animationchannelnode_cs.md)* class). |
| **ANIMATION_CHANNEL_BONES** = 22 | Channel that animates the bones of a skeleton directly (see the *[AnimationChannelBones](../../../../api/library/animations/timeline/class.animationchannelbones_cs.md)* class). |
| **ANIMATION_CHANNEL_EVENT** = 23 | Channel that fires an event when the playhead crosses one of its keys. It drives no engine parameter (see the *[AnimationChannelEvent](../../../../api/library/animations/timeline/class.animationchannelevent_cs.md)* class). |
| **ANIMATION_CHANNEL_SKELETON_ANIMATION** = 24 | Channel that plays a skeletal animation on the bound node, starting it at the key time (see the *[AnimationChannelSkeletonAnimation](../../../../api/library/animations/timeline/class.animationchannelskeletonanimation_cs.md)* class). |
| **ANIMATION_CHANNEL_SOUND** = 25 | Channel that plays a sound on the bound sound source, starting it at the key time (see the *[AnimationChannelSound](../../../../api/library/animations/timeline/class.animationchannelsound_cs.md)* class). |
| **ANIMATION_CHANNEL_EVENT_STATE** = 26 | Channel that keeps a state over an interval, raising the begin phase when the playhead enters it and the end phase when it leaves (see the *[AnimationChannelEventState](../../../../api/library/animations/timeline/class.animationchanneleventstate_cs.md)* class). |
| **ANIMATION_CHANNEL_SUB_SEQUENCE** = 27 | Channel that plays whole sequences as clips, which is how a composition is assembled (see the *[AnimationChannelSubSequence](../../../../api/library/animations/timeline/class.animationchannelsubsequence_cs.md)* class). |
| **ANIMATION_CHANNEL_FOLLOW_PATH** = 28 | Channel that moves a node along a trajectory and turns it to face the direction of travel, writing both the position and the rotation (see the *[AnimationChannelFollowPath](../../../../api/library/animations/timeline/class.animationchannelfollowpath_cs.md)* class). |
| **NUM_ANIMATION_CHANNELS** = 29 | Number of channel types. |

## EVENT_PHASE

Phase an event is reported with. A key of an event channel is a single point, while a state interval has a beginning and an end.
| Name | Description |
|---|---|
| **POINT** = 0 | The playhead crossed a key of an event channel, so the event is a single impulse. |
| **BEGIN** = 1 | The playhead entered an interval of an event state channel. |
| **END** = 2 | The playhead left an interval of an event state channel. |

## PROPERTY

Playback property of a channel. These curves shape how the channel plays its content rather than what it writes into the scene, and only some channel types offer them.
| Name | Description |
|---|---|
| **PITCH** = 0 | Pitch of the sound played by the channel. |
| **SOUND_TRIM_IN** = 1 | Offset from the beginning of the sound file the playback starts at, in seconds. |
| **SOUND_DURATION** = 2 | Length of the played part of the sound file, in seconds. |
| **SOUND_FADE_IN** = 3 | Time the sound gain rises from silence over, in seconds. |
| **SOUND_FADE_OUT** = 4 | Time the sound gain falls to silence over, in seconds. |
| **NUM_PROPERTIES** = 5 | Number of playback property kinds. |

## RESOLVE_STATE

State of the parameter the channel refers to. It is recomputed when the sequence is loaded and is not saved to the file.
| Name | Description |
|---|---|
| **RESOLVED** = 0 | The parameter animated by the channel was found and it matches the channel. |
| **PARAM_MISSING** = 1 | The parameter animated by the channel no longer exists. |
| **TYPE_MISMATCH** = 2 | The parameter exists, but its type no longer matches the type of the channel. |
| **ENUM_DRIFT** = 3 | The parameter is an enumeration whose set of items changed since the channel was authored, so the stored values may no longer mean what they meant. |

## SLOT_ACCESS

Way the slot of the animated parameter is addressed. It matters only for parameters that come as an array, such as a surface of an object or a slot of a material.
| Name | Description |
|---|---|
| **BY_INDEX** = 0 | The slot is addressed by the position it takes in the list of slots, so the channel keeps writing into the same numbered slot whatever it is called. |
| **BY_NAME** = 1 | The slot is looked up by its name on each target the channel is bound to, which is what one channel driving several objects needs when their slots sit in a different order. |

### Properties

## 🔒︎ AnimationChannelInfo Info

The compact description of what the channel animates. It carries the type and the parameter of the channel and is what a frame is described by.
## 🔒︎ AnimationChannel.TYPE Type

The type of the channel, which tells which subclass it can be cast to.
## 🔒︎ string TypeName

The name of the channel type. It is the symbolic form of the type, the one stored in the file.
## 🔒︎ AnimParams.PARAM Param

The parameter animated by the channel. Channels that drive no engine parameter, such as event ones, report an unknown parameter by design. The identifier comes from the registry of animatable parameters, which is looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class.
## 🔒︎ int ParamIndex

The slot of the animated parameter for parameters that come as an array, such as a surface or a bone. A parameter that has no slots reports -1.
## string ParamName

The name that addresses the animated parameter when a number is not enough, such as the name of a property parameter or of a surface. Event channels keep the name of the event here.
## AnimationChannel.SLOT_ACCESS SlotAccess

The way the parameter slot is addressed: by the position it takes in the list of slots, or by its name. The slot itself is set through [ParamIndex](#ParamIndex) or [ParamName](#ParamName) accordingly. See [SLOT_ACCESS_*](#SLOT_ACCESS_BY_INDEX).
## 🔒︎ bool IsConstantSpeedSupported

The value indicating if the channel can travel its curve at a constant speed. The value of the channel has to have a length to measure for it: a floating-point number, a vector of floats or doubles and a followed path carry it, while a rotation carries it only in one of the angles modes, since the segments of a quaternion rotation are spherical blends already. An integer value has no such length, and neither does a texture or a name, so those channels do not offer the setting.
## 🔒︎ bool IsConstantSpeed

The value indicating if the channel travels its curve at a constant speed. Use [setConstantSpeed()](#setConstantSpeed_int_int_void) to turn it on or off.
## string CustomName

The custom name given to the channel in the Sequencer. It is a free label with no meaning to the engine, and it is what the searches by name work with.
## 🔒︎ AnimationBind BindCopy

The copy of the binding that points the channel at what it animates. A global channel, such as a console or a render one, has no binding.
## 🔒︎ int BindType

The kind of binding the channel expects, which tells which [AnimationBind](../../../../api/library/animations/timeline/class.animationbind_cs.md) subclass fits it.
## 🔒︎ float MinTime

The moment the content of the channel starts at, in seconds.
## 🔒︎ float MaxTime

The moment the content of the channel ends at, in seconds.
## 🔒︎ float Duration

The time span covered by the channel, in seconds, which is the distance between the first and the last moment of its content.
## float DisplayValueMin

The lower end of the value range the curve view is scaled to. It shapes the way the channel is shown and does not clamp any value.
## float DisplayValueMax

The upper end of the value range the curve view is scaled to. It shapes the way the channel is shown and does not clamp any value.
## int Order

The display order of the channel, which is also its priority: where two channels drive the same target, the one that sits higher in the list wins, and a lower number means a higher place. A channel added with no order set gets one automatically.
## int RowGroup

The row the channel shares with the other channels of the same group, or -1 when it takes a row of its own. It shapes the way the timeline is drawn and does not affect playback.
## int GroupID

The channel group the channel belongs to, or -1 when it sits at the top level. A disabled group mutes every channel in it.
## int ID

The identifier of the channel inside its sequence. It stays with the channel while the display order changes, which is why updating and removing a channel go by it. A channel that was never added anywhere has the identifier of 0.
## bool Enabled

The value indicating if the channel takes part in playback. A muted channel keeps its keys and its place, and simply contributes nothing.
## 🔒︎ int NumPropertyCurves

The number of playback property curves attached to the channel.
## 🔒︎ int NumComponents

The number of components the keys of the channel are reached by. The axes of the channel curve come first, and the playback property lanes follow them.
## 🔒︎ int NumClips

The number of clips placed on the channel.
## 🔒︎ int NumClipRows

The number of rows the clips of the channel are laid out in.
## 🔒︎ AnimationChannel.RESOLVE_STATE ResolveState

The state of the parameter the channel refers to. It tells a channel that lost its parameter from one whose parameter changed its type or its set of items.
## 🔒︎ bool Resolved

The value indicating if the parameter animated by the channel was found and matches it.
## string AuthoredTypeName

The type name the animated parameter had when the channel was authored. The stored signature is what a parameter that changed since then is told apart by.
## string AuthoredEnumItems

The items the animated enumeration had when the channel was authored. Comparing them with the current ones is what reports a drifted enumeration.
## string AuthoredTitle

The title the animated parameter was shown under when the channel was authored. It keeps the row readable when the parameter itself can no longer be found.
## string AuthoredParamName

The symbolic name the animated parameter had when the channel was authored, which is the canonical form rather than the title shown in the interface.
### Members

---

## static int TypeFromName ( string name )

Returns the channel type that goes by the specified name, which is the reverse of the type name of a channel.
### Arguments

- *string* **name** - Name of the channel type.

### Return value

Channel type with the specified name.
## void SetBind ( AnimationBind bind )

Points the channel at what it is to animate. The channel keeps a copy of the binding, so later changes to the one passed here do not reach it.
### Arguments

- *[AnimationBind](../../../../api/library/animations/timeline/class.animationbind_cs.md)* **bind** - Binding to be used by the channel.

## int GetPropertyCurveKind ( int index )

Returns the kind of playback property the curve with the specified number shapes.
### Arguments

- *int* **index** - Number of the property curve.

### Return value

Kind of the playback property the curve shapes.
## AnimationCurveFloat GetPropertyCurve ( AnimationChannel.PROPERTY kind )

Returns the curve that shapes the specified playback property of the channel.
### Arguments

- *[AnimationChannel.PROPERTY](../../../../api/library/animations/timeline/class.animationchannel_cs.md#PROPERTY)* **kind** - Kind of the playback property.

### Return value

Copy of the curve of the specified kind, or NULL (null in C#) if the channel has none.
## void SetPropertyCurve ( AnimationChannel.PROPERTY kind , AnimationCurveFloat curve )

Attaches a curve that shapes the specified playback property of the channel. The channel keeps a copy of the curve.
### Arguments

- *[AnimationChannel.PROPERTY](../../../../api/library/animations/timeline/class.animationchannel_cs.md#PROPERTY)* **kind** - Kind of the playback property.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **curve** - Curve to shape the property with.

## void RemovePropertyCurve ( AnimationChannel.PROPERTY kind )

Removes the curve that shapes the specified playback property, so the property goes back to a single value.
### Arguments

- *[AnimationChannel.PROPERTY](../../../../api/library/animations/timeline/class.animationchannel_cs.md#PROPERTY)* **kind** - Kind of the playback property.

## float GetPropertyValueByTime ( AnimationChannel.PROPERTY kind , float time )

Returns the value the specified playback property holds at the given moment.
### Arguments

- *[AnimationChannel.PROPERTY](../../../../api/library/animations/timeline/class.animationchannel_cs.md#PROPERTY)* **kind** - Kind of the playback property.
- *float* **time** - Moment to be sampled, in seconds.

### Return value

Value of the property at the specified moment.
## int GetComponentPropertyKind ( int component )

Returns what the specified component stands for. It is the way to tell the axes of the channel curve from the playback property lanes that follow them.
### Arguments

- *int* **component** - Component number.

### Return value

Kind of the playback property the component stands for, or -1 when it is an axis of the channel curve.
## int GetComponentNumKeys ( int component )

Returns the number of keys the specified component holds.
### Arguments

- *int* **component** - Component number.

### Return value

Number of keys on the component.
## float GetComponentKeyTime ( int component , int key )

Returns the moment the specified key sits at.
### Arguments

- *int* **component** - Component number.
- *int* **key** - Key number.

### Return value

Moment the key sits at, in seconds.
## double GetComponentKeyValue ( int component , int key )

Returns the value of the specified key. Every component reports its value as a double, whatever the type of the channel is.
### Arguments

- *int* **component** - Component number.
- *int* **key** - Key number.

### Return value

Value of the key.
## double GetComponentValueByTime ( int component , float time )

Returns the value the specified component holds at the given moment. A component with no keys reports the neutral value of the animated parameter.
### Arguments

- *int* **component** - Component number.
- *float* **time** - Moment to be sampled, in seconds.

### Return value

Value of the component at the specified moment.
## int GetComponentKeyType ( int component , int key )

Returns the way the curve leaves and enters the specified key.
### Arguments

- *int* **component** - Component number.
- *int* **key** - Key number.

### Return value

Interpolation type of the key (see [KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE_LINEAR)).
## void SetComponentKeyType ( int component , int key , int type , float value_time_ratio = 1.0f )

Sets the way the curve leaves and enters the specified key.
### Arguments

- *int* **component** - Component number.
- *int* **key** - Key number.
- *int* **type** - Interpolation type of the key (see [KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE_LINEAR)).
- *float* **value_time_ratio** - Number of units of value that make up one unit of time. It is taken into account when the two handles of an [aligned](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE_ALIGNED) key are made collinear: the handles are brought into a common space through this ratio, aligned there and converted back, so that a curve drawn with value and time on different scales still shows the pair as one straight line. The default value is 1.0f, which measures value and time on the same scale.

## vec2 GetComponentKeyLeftTangent ( int component , int key )

Returns the tangent the curve arrives at the specified key with.
### Arguments

- *int* **component** - Component number.
- *int* **key** - Key number.

### Return value

Tangent the curve arrives at the key with.
## vec2 GetComponentKeyRightTangent ( int component , int key )

Returns the tangent the curve leaves the specified key with.
### Arguments

- *int* **component** - Component number.
- *int* **key** - Key number.

### Return value

Tangent the curve leaves the key with.
## void SetComponentKeyLeftTangent ( int component , int key , vec2 tangent , float value_time_ratio = 1.0f )

Sets the tangent the curve arrives at the specified key with.
### Arguments

- *int* **component** - Component number.
- *int* **key** - Key number.
- *vec2* **tangent** - Tangent the curve is to arrive at the key with.
- *float* **value_time_ratio** - Number of units of value that make up one unit of time, taken into account when the opposite handle of an [aligned](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE_ALIGNED) key is brought back in line with this one. The default value is 1.0f, which measures value and time on the same scale.

## void SetComponentKeyRightTangent ( int component , int key , vec2 tangent , float value_time_ratio = 1.0f )

Sets the tangent the curve leaves the specified key with.
### Arguments

- *int* **component** - Component number.
- *int* **key** - Key number.
- *vec2* **tangent** - Tangent the curve is to leave the key with.
- *float* **value_time_ratio** - Number of units of value that make up one unit of time, taken into account when the opposite handle of an [aligned](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE_ALIGNED) key is brought back in line with this one. The default value is 1.0f, which measures value and time on the same scale.

## int AddComponentKey ( int component , float time , double value , int type )

Adds a key to the specified component. Keys are kept in time order, so the number of the new key follows from the moment it was placed at.
### Arguments

- *int* **component** - Component number.
- *float* **time** - Moment the key is to sit at, in seconds.
- *double* **value** - Value of the key.
- *int* **type** - Interpolation type of the key (see [KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE_LINEAR)).

### Return value

Number of the new key.
## void RemoveComponentKey ( int component , int key )

Removes the specified key from the component.
### Arguments

- *int* **component** - Component number.
- *int* **key** - Key number.

## int MoveComponentKey ( int component , int key , float new_time )

Moves the specified key to another moment. Moving a key past its neighbours renumbers it, which is why the new number is reported back.
### Arguments

- *int* **component** - Component number.
- *int* **key** - Key number.
- *float* **new_time** - Moment the key is to be moved to, in seconds.

### Return value

New number of the key.
## void SetComponentKeyValue ( int component , int key , double value )

Sets the value of the specified key.
### Arguments

- *int* **component** - Component number.
- *int* **key** - Key number.
- *double* **value** - Value to be set.

## int GetComponentPreInfinity ( int component )

Returns the way the specified component behaves before its first key.
### Arguments

- *int* **component** - Component number.

### Return value

Way the component behaves before its first key.
## int GetComponentPostInfinity ( int component )

Returns the way the specified component behaves after its last key.
### Arguments

- *int* **component** - Component number.

### Return value

Way the component behaves after its last key.
## void SetComponentPreInfinity ( int component , int mode )

Sets the way the specified component behaves before its first key.
### Arguments

- *int* **component** - Component number.
- *int* **mode** - Way the component is to behave before its first key.

## void SetComponentPostInfinity ( int component , int mode )

Sets the way the specified component behaves after its last key.
### Arguments

- *int* **component** - Component number.
- *int* **mode** - Way the component is to behave after its last key.

## void SetConstantSpeed ( bool enabled , bool force_update = false )

Makes the value travel its curve at a constant speed, or lets it keep the pace the key times imply. The curve is measured along its own length and a table is built that remaps the playhead through that measurement, so the total duration stays and only the pace between the keys changes. The call has no effect on a channel that does not support it, see [IsConstantSpeedSupported](#IsConstantSpeedSupported).
### Arguments

- *bool* **enabled** - true to make the value travel the curve at a constant speed, false to let each stretch between two keys take the time between them however far the value moves in it.
- *bool* **force_update** - true to rebuild the length-to-time table even when the setting itself did not change, which is what a channel whose keys have moved needs. The default value is false.

## float GetConstantSpeedTime ( float time )

Returns the moment the channel samples its curve at for the given moment on the timeline, that is, the argument put through the length-to-time table built by [setConstantSpeed()](#setConstantSpeed_int_int_void).
### Arguments

- *float* **time** - Moment on the timeline, in seconds.

### Return value

Moment the channel actually samples its curve at, in seconds. It equals the argument where constant speed is off or unsupported.
## UGUID GetKeyValueUGUID ( int key )

Returns the asset reference held by the specified key. It works on the channels whose keys carry a GUID rather than a number, which are the asset and the skeletal animation ones.
### Arguments

- *int* **key** - Key number.

### Return value

Asset reference held by the key.
## void SetKeyValueUGUID ( int key , UGUID value )

Sets the asset reference held by the specified key.
### Arguments

- *int* **key** - Key number.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **value** - Asset reference to be set.

## int AddKeyValueUGUID ( float time , UGUID value )

Adds a key holding an asset reference.
### Arguments

- *float* **time** - Moment the key is to sit at, in seconds.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **value** - Asset reference to be held by the key.

### Return value

Number of the new key.
## UGUID GetValueByTimeUGUID ( float time )

Returns the asset reference the channel holds at the given moment.
### Arguments

- *float* **time** - Moment to be sampled, in seconds.

### Return value

Asset reference held at the specified moment.
## string GetKeyValueString ( int key )

Returns the string held by the specified key. It works on the channels whose keys carry text rather than a number, which are the string and the sound ones.
### Arguments

- *int* **key** - Key number.

### Return value

String held by the key.
## void SetKeyValueString ( int key , string value )

Sets the string held by the specified key.
### Arguments

- *int* **key** - Key number.
- *string* **value** - String to be set.

## int AddKeyValueString ( float time , string value )

Adds a key holding a string.
### Arguments

- *float* **time** - Moment the key is to sit at, in seconds.
- *string* **value** - String to be held by the key.

### Return value

Number of the new key.
## string GetValueByTimeString ( float time )

Returns the string the channel holds at the given moment.
### Arguments

- *float* **time** - Moment to be sampled, in seconds.

### Return value

String held at the specified moment.
## int AddClip ( float begin_time , float length , string content , int row = 0 )

Places a clip on the channel. Clips are kept in time order, and a clip covers the half-open span that starts at its beginning and ends before the next moment, so two clips that meet do not overlap by a frame.
### Arguments

- *float* **begin_time** - Moment the clip starts at, in seconds.
- *float* **length** - Length of the clip, in seconds. A value of zero or less makes the clip stretch to the next one on the same row.
- *string* **content** - Content of the clip, which names what it plays.
- *int* **row** - Row the clip is placed on. The default value is 0.

### Return value

Number of the new clip.
## void RemoveClip ( int index )

Removes the specified clip from the channel.
### Arguments

- *int* **index** - Clip number.

## float GetClipBeginTime ( int index )

Returns the moment the specified clip starts at.
### Arguments

- *int* **index** - Clip number.

### Return value

Moment the clip starts at, in seconds.
## void SetClipBeginTime ( int index , float v )

Moves the specified clip to another moment.
### Arguments

- *int* **index** - Clip number.
- *float* **v** - Moment the clip is to start at, in seconds.

## float GetClipLength ( int index )

Returns the length of the specified clip.
### Arguments

- *int* **index** - Clip number.

### Return value

Length of the clip, in seconds.
## void SetClipLength ( int index , float v )

Sets the length of the specified clip.
### Arguments

- *int* **index** - Clip number.
- *float* **v** - Length of the clip, in seconds. A value of zero or less makes the clip stretch to the next one on the same row.

## float GetClipIn ( int index )

Returns how far into its content the specified clip starts playing, which is what trimming the head of a clip changes.
### Arguments

- *int* **index** - Clip number.

### Return value

Offset into the content of the clip, in seconds.
## void SetClipIn ( int index , float v )

Sets how far into its content the specified clip starts playing.
### Arguments

- *int* **index** - Clip number.
- *float* **v** - Offset into the content of the clip, in seconds.

## float GetClipSpeedAt ( int index , float local_time )

Returns how fast the specified clip runs at the given moment of its own time. A clip with no speed curve runs at its plain speed all the way.
### Arguments

- *int* **index** - Clip number.
- *float* **local_time** - Moment inside the clip, in seconds, counted from its beginning.

### Return value

Speed multiplier of the clip at the specified moment.
## int GetClipRow ( int index )

Returns the row the specified clip sits on.
### Arguments

- *int* **index** - Clip number.

### Return value

Row the clip sits on.
## void SetClipRow ( int index , int row )

Moves the specified clip to another row. Rows set the priority of clips that overlap: the higher row wins, and the one that starts later wins a tie.
### Arguments

- *int* **index** - Clip number.
- *int* **row** - Row the clip is to sit on.

## bool IsClipEnabled ( int index )

Returns a value indicating if the specified clip takes part in playback.
### Arguments

- *int* **index** - Clip number.

### Return value

true if the specified clip takes part in playback; otherwise, false.
## void SetClipEnabled ( int index , bool enabled )

Lets the specified clip play or mutes it, keeping it in place either way.
### Arguments

- *int* **index** - Clip number.
- *bool* **enabled** - true to let the clip play, false to mute it.

## int GetClipPreInfinity ( int index )

Returns the way the specified clip fills the part of its span that comes before its content.
### Arguments

- *int* **index** - Clip number.

### Return value

Way the clip fills the time before its content.
## void SetClipPreInfinity ( int index , int mode )

Sets the way the specified clip fills the part of its span that comes before its content, which is what makes a stretched clip hold or repeat.
### Arguments

- *int* **index** - Clip number.
- *int* **mode** - Way the clip is to fill the time before its content.

## int GetClipPostInfinity ( int index )

Returns the way the specified clip fills the part of its span that comes after its content.
### Arguments

- *int* **index** - Clip number.

### Return value

Way the clip fills the time after its content.
## void SetClipPostInfinity ( int index , int mode )

Sets the way the specified clip fills the part of its span that comes after its content.
### Arguments

- *int* **index** - Clip number.
- *int* **mode** - Way the clip is to fill the time after its content.

## vec4 GetClipColor ( int index )

Returns the color the specified clip is drawn with on the timeline.
### Arguments

- *int* **index** - Clip number.

### Return value

Color the clip is drawn with.
## void SetClipColor ( int index , vec4 color )

Sets the color the specified clip is drawn with on the timeline.
### Arguments

- *int* **index** - Clip number.
- *vec4* **color** - Color the clip is to be drawn with.

## string GetClipContent ( int index )

Returns what the specified clip plays, in the form the channel type stores it in.
### Arguments

- *int* **index** - Clip number.

### Return value

Content of the clip.
## void SetClipContent ( int index , string content )

Sets what the specified clip plays.
### Arguments

- *int* **index** - Clip number.
- *string* **content** - Content the clip is to play.

## string GetClipContentName ( int index )

Returns the name the specified clip is shown under on the timeline.
### Arguments

- *int* **index** - Clip number.

### Return value

Name the clip is shown under.
## void SetClipContentName ( int index , string name )

Sets the name the specified clip is shown under on the timeline.
### Arguments

- *int* **index** - Clip number.
- *string* **name** - Name the clip is to be shown under.

## void SetClipNode ( int index , Node node )

Points the specified clip at a node in the scene. It applies to the node channels, where a clip stands for a shot and the node is the camera it is taken with.
### Arguments

- *int* **index** - Clip number.
- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node** - Node the clip is to point at.

## void SetClipNodeDescription ( int index , int node_id , string node_name )

Points the specified clip at a node by its identifier and name rather than by a live node, which is how a target is stored for a scene that is not loaded yet.
### Arguments

- *int* **index** - Clip number.
- *int* **node_id** - Identifier of the node.
- *string* **node_name** - Name of the node.

## int GetClipNodeID ( int index )

Returns the identifier of the node stored for the specified clip.
### Arguments

- *int* **index** - Clip number.

### Return value

Identifier of the node stored for the clip, or -1 if the clip points at no node.
## string GetClipNodeName ( int index )

Returns the name of the node stored for the specified clip.
### Arguments

- *int* **index** - Clip number.

### Return value

Name of the node stored for the clip.
## int GetClipNodeAccess ( int index )

Returns the way the node of the specified clip is looked up in the scene.
### Arguments

- *int* **index** - Clip number.

### Return value

Way the node of the clip is looked up: 0 by identifier, 1 by name.
## void SetClipNodeAccess ( int index , int access )

Sets the way the node of the specified clip is looked up in the scene. Looking a node up by name survives a scene rebuilt from scratch, while an identifier is exact.
### Arguments

- *int* **index** - Clip number.
- *int* **access** - Way the node is to be looked up: 0 by identifier, 1 by name.

## int GetClipLiveNodeID ( int index )

Returns the node the specified clip resolves to in the scene that is loaded right now, which may differ from the identifier stored in the file.
### Arguments

- *int* **index** - Clip number.

### Return value

Identifier of the node the clip resolves to in the loaded scene, or -1 if it resolves to none.
## AnimationSequence GetClipSequence ( int index )

Returns the sequence the specified clip plays. It applies to the sub-sequence channels, which is how one animation is nested in another.
### Arguments

- *int* **index** - Clip number.

### Return value

Sequence played by the clip, or NULL (null in C#) if the clip plays none.
## void SetClipSequence ( int index , AnimationSequence sequence )

Sets the sequence the specified clip plays.
### Arguments

- *int* **index** - Clip number.
- *[AnimationSequence](../../../../api/library/animations/timeline/class.animationsequence_cs.md)* **sequence** - Sequence the clip is to play.

## UGUID GetClipSlotGUID ( int index )

Returns the GUID that tells this placement of a nested sequence from every other one. It is minted by the sequence itself, and it is what keeps the bindings of two instances of one nested animation apart.
### Arguments

- *int* **index** - Clip number.

### Return value

GUID of the placement slot of the clip.
## bool IsClipEmbedded ( int index )

Returns a value indicating if the specified clip carries a sequence of its own rather than referring to a file.
### Arguments

- *int* **index** - Clip number.

### Return value

true if the sequence of the clip is stored inside the host sequence; otherwise, false.
## void SetClipEmbedded ( int index , bool embedded )

Sets whether the specified clip carries a sequence of its own or refers to a file. An embedded sequence travels with its host and is not shared with anything else.
### Arguments

- *int* **index** - Clip number.
- *bool* **embedded** - true to store the sequence inside the host one, false to refer to a file.

## AnimationCurveFloat GetClipWeightCurve ( int index )

Returns the curve that sets how much the specified clip contributes over its own time. A clip with no such curve contributes in full.
### Arguments

- *int* **index** - Clip number.

### Return value

Copy of the weight curve of the clip, or NULL (null in C#) if the clip has none.
## void SetClipWeightCurve ( int index , AnimationCurveFloat curve )

Sets the curve that shapes how much the specified clip contributes over its own time, which is what crossfades two overlapping clips.
### Arguments

- *int* **index** - Clip number.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **curve** - Weight curve to be used by the clip.

## AnimationCurveFloat GetClipSpeedMultiplierCurve ( int index )

Returns the curve that retimes the specified clip over its own time.
### Arguments

- *int* **index** - Clip number.

### Return value

Copy of the speed curve of the clip, or NULL (null in C#) if the clip has none.
## void SetClipSpeedMultiplierCurve ( int index , AnimationCurveFloat curve )

Sets the curve that retimes the specified clip over its own time, so that its content speeds up or slows down as it plays.
### Arguments

- *int* **index** - Clip number.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **curve** - Speed curve to be used by the clip.

## AnimationCurveFloat GetClipPropertyCurve ( int index , AnimationChannel.PROPERTY kind )

Returns the curve that shapes the specified playback property of a single clip.
### Arguments

- *int* **index** - Clip number.
- *[AnimationChannel.PROPERTY](../../../../api/library/animations/timeline/class.animationchannel_cs.md#PROPERTY)* **kind** - Kind of the playback property.

### Return value

Copy of the curve of the specified kind, or NULL (null in C#) if the clip has none.
## void SetClipPropertyCurve ( int index , AnimationChannel.PROPERTY kind , AnimationCurveFloat curve )

Attaches a curve that shapes the specified playback property of a single clip, such as the fade of one sound among several on the row.
### Arguments

- *int* **index** - Clip number.
- *[AnimationChannel.PROPERTY](../../../../api/library/animations/timeline/class.animationchannel_cs.md#PROPERTY)* **kind** - Kind of the playback property.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **curve** - Curve to shape the property with.

## void RemoveClipPropertyCurve ( int index , AnimationChannel.PROPERTY kind )

Removes the curve that shapes the specified playback property of a single clip.
### Arguments

- *int* **index** - Clip number.
- *[AnimationChannel.PROPERTY](../../../../api/library/animations/timeline/class.animationchannel_cs.md#PROPERTY)* **kind** - Kind of the playback property.

## float GetClipPropertyValueByTime ( int index , AnimationChannel.PROPERTY kind , float local_time )

Returns the value the specified playback property of a clip holds at the given moment of the clip own time.
### Arguments

- *int* **index** - Clip number.
- *[AnimationChannel.PROPERTY](../../../../api/library/animations/timeline/class.animationchannel_cs.md#PROPERTY)* **kind** - Kind of the playback property.
- *float* **local_time** - Moment inside the clip, in seconds, counted from its beginning.

### Return value

Value of the property at the specified moment.
## bool HasClipPropertyCurve ( int index , AnimationChannel.PROPERTY kind )

Returns a value indicating if the specified clip has a curve of the given playback property kind.
### Arguments

- *int* **index** - Clip number.
- *[AnimationChannel.PROPERTY](../../../../api/library/animations/timeline/class.animationchannel_cs.md#PROPERTY)* **kind** - Kind of the playback property.

### Return value

true if the clip has a curve of the specified kind; otherwise, false.
## bool SaveClipToBlob ( int clip_index , Blob blob )

Saves a single clip to a blob, which is what copying a clip is built on.
### Arguments

- *int* **clip_index** - Clip number.
- *[Blob](../../../../api/library/common/class.blob_cs.md)* **blob** - Blob to save the clip to.

### Return value

true if the clip was saved successfully; otherwise, false.
## int LoadClipFromBlob ( float begin_time , Blob blob )

Loads a clip from a blob and places it at the specified moment. A nested sequence pasted this way gets a placement of its own, so its bindings do not follow the clip it was copied from.
### Arguments

- *float* **begin_time** - Moment the loaded clip is to start at, in seconds.
- *[Blob](../../../../api/library/common/class.blob_cs.md)* **blob** - Blob to load the clip from.

### Return value

Number of the loaded clip, or -1 if the blob was written by another version of the format.
## float NextClipBeginAfter ( float after_begin , int row , float none_value )

Returns the moment the next clip on the row starts at, which is where a clip of automatic length stops.
### Arguments

- *float* **after_begin** - Moment to search after, in seconds.
- *int* **row** - Row to search on.
- *float* **none_value** - Value to be returned when there is no such clip.

### Return value

Moment the next clip on the row starts at, or the specified fallback value.
## void RefreshTimesFromClips ( )

Recomputes the time span of the channel from the clips it holds. Call it after moving or resizing clips by hand, so that the channel reports the span it now covers.
## void Save ( Blob blob )

Saves the channel to a blob, in the latest version of the format.
### Arguments

- *[Blob](../../../../api/library/common/class.blob_cs.md)* **blob** - Blob to save the channel to.

## void Load ( Blob blob )

Loads the channel from a blob, replacing everything it currently holds.
### Arguments

- *[Blob](../../../../api/library/common/class.blob_cs.md)* **blob** - Blob to load the channel from.
