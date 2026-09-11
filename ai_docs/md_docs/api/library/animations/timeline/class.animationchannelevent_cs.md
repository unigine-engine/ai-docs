# Unigine::AnimationChannelEvent Class (CS)

**Inherits from:** AnimationChannel


This channel fires an event every time the playhead crosses one of its keys. It drives no engine parameter: it is the way a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cs.md) tells the game logic that a certain moment has come, such as a footstep, a line of dialogue or a trigger.


Each key carries an integer payload, and the name of the event is the parameter name of the channel. Handle the events by subscribing to the player, and note that they fire whatever the playback weight is, so a faded out sequence still drives logic.


## AnimationChannelEvent Class

### Properties

## 🔒︎ int DefaultValue

The value the channel falls back to where it has no keys of its own.
## AnimationCurveInt Curve

The curve that holds the keys of the channel.
### Members

---

## AnimationChannelEvent ( )

Constructor. Creates an empty channel.
## void AssignFrom ( AnimationChannelEvent channel )

Copies the content of the specified channel into this one.
### Arguments

- *[AnimationChannelEvent](../../../../api/library/animations/timeline/class.animationchannelevent_cs.md)* **channel** - Source channel to copy the content from.

## int GetValueByTime ( float time )

Returns the payload the channel holds at the given moment.
### Arguments

- *float* **time** - Moment to be sampled, in seconds.

### Return value

Payload the channel holds at the specified moment.
## int GetValueByNormalizedTime ( float normalized_time )

Returns the payload the channel holds at the given moment, addressed as a share of its time span rather than in seconds.
### Arguments

- *float* **normalized_time** - Moment to be sampled, given as a share of the channel time span in the [0.0f, 1.0f] range.

### Return value

Payload the channel holds at the specified moment.
## void AddValue ( float time , int value )

Adds a key that fires an event carrying the specified payload.
### Arguments

- *float* **time** - Moment the key is to sit at, in seconds.
- *int* **value** - Payload to be carried by the event.
