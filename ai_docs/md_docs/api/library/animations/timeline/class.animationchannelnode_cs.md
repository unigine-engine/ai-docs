# Unigine::AnimationChannelNode Class (CS)

**Inherits from:** AnimationChannel


This channel animates a parameter that refers to a node over time. It is one row of a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cs.md), while everything the channels share, such as the animated parameter, the binding and the clips, comes from the [AnimationChannel](../../../../api/library/animations/timeline/class.animationchannel_cs.md) base class.


A node reference has nothing in between, so the channel holds the value of a key until the next one is reached. This is what a camera cut is built on, where every key names the camera the shot is taken with.


## AnimationChannelNode Class

### Properties

## 🔒︎ Node DefaultValue

The value the channel falls back to where it has no keys of its own.
## AnimationCurveInt CurveID

The curve that holds the identifiers of the nodes the channel switches between.
### Members

---

## AnimationChannelNode ( AnimParams.PARAM param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.

## AnimationChannelNode ( AnimParams.PARAM param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelNode ( AnimParams.PARAM param , string param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.
- *string* **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## AnimationChannelNode ( string param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *string* **param** - Name of the parameter to be animated by the channel.

## AnimationChannelNode ( string param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *string* **param** - Name of the parameter to be animated by the channel.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelNode ( string param , string param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *string* **param** - Name of the parameter to be animated by the channel.
- *string* **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## void AssignFrom ( AnimationChannelNode channel )

Copies the content of the specified channel into this one.
### Arguments

- *[AnimationChannelNode](../../../../api/library/animations/timeline/class.animationchannelnode_cs.md)* **channel** - Source channel to copy the content from.

## Node GetValueByTime ( float time )

Returns the value the channel holds at the given moment.
### Arguments

- *float* **time** - Moment to be sampled, in seconds.

### Return value

Value the channel holds at the specified moment.
## Node GetValueByNormalizedTime ( float normalized_time )

Returns the value the channel holds at the given moment, addressed as a share of its time span rather than in seconds.
### Arguments

- *float* **normalized_time** - Moment to be sampled, given as a share of the channel time span in the [0.0f, 1.0f] range.

### Return value

Value the channel holds at the specified moment.
## void AddValue ( float time , int node_id )

Adds a key holding a node, addressed by its identifier.
### Arguments

- *float* **time** - Moment the key is to sit at, in seconds.
- *int* **node_id** - Identifier of the node to be held by the key.
