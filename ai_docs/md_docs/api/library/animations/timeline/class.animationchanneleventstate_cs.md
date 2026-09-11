# Unigine::AnimationChannelEventState Class (CS)

**Inherits from:** AnimationChannel


This channel keeps a state over a span of time rather than firing at a single moment. Entering an interval raises the begin phase of the event and leaving it raises the end phase, which is what a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cs.md) switches something on and back off with.


A player that joins a take in the middle can ask which intervals are open at that moment, so a state that began before it started playing is not lost.


## AnimationChannelEventState Class

### Properties

## 🔒︎ int NumIntervals

The number of intervals placed on the channel.
### Members

---

## AnimationChannelEventState ( )

Constructor. Creates an empty channel.
## void AssignFrom ( AnimationChannelEventState channel )

Copies the content of the specified channel into this one.
### Arguments

- *[AnimationChannelEventState](../../../../api/library/animations/timeline/class.animationchanneleventstate_cs.md)* **channel** - Source channel to copy the content from.

## int AddInterval ( float start , float end , int payload )

Adds an interval to the channel. The begin phase is raised when the playhead enters it and the end phase when it leaves.
### Arguments

- *float* **start** - Moment the interval opens at, in seconds.
- *float* **end** - Moment the interval closes at, in seconds.
- *int* **payload** - Payload carried by the interval.

### Return value

Number of the new interval.
## void SetInterval ( int index , float start , float end , int payload )

Sets the bounds and the payload of the specified interval.
### Arguments

- *int* **index** - Interval number.
- *float* **start** - Moment the interval opens at, in seconds.
- *float* **end** - Moment the interval closes at, in seconds.
- *int* **payload** - Payload carried by the interval.

## void RemoveInterval ( int index )

Removes the specified interval from the channel.
### Arguments

- *int* **index** - Interval number.

## void ClearIntervals ( )

Removes all intervals from the channel.
## float GetIntervalStart ( int index )

Returns the moment the specified interval opens at.
### Arguments

- *int* **index** - Interval number.

### Return value

Moment the interval opens at, in seconds.
## float GetIntervalEnd ( int index )

Returns the moment the specified interval closes at.
### Arguments

- *int* **index** - Interval number.

### Return value

Moment the interval closes at, in seconds.
## int GetIntervalPayload ( int index )

Returns the payload carried by the specified interval.
### Arguments

- *int* **index** - Interval number.

### Return value

Payload carried by the interval.
