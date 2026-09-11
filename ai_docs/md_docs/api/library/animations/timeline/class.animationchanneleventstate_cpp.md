# Unigine::AnimationChannelEventState Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationChannel


This channel keeps a state over a span of time rather than firing at a single moment. Entering an interval raises the begin phase of the event and leaving it raises the end phase, which is what a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cpp.md) switches something on and back off with.


A player that joins a take in the middle can ask which intervals are open at that moment, so a state that began before it started playing is not lost.


## AnimationChannelEventState Class

### Members

## int getNumIntervals () const

Returns the current number of intervals placed on the channel.
### Return value

Current number of intervals on the channel
---

## AnimationChannelEventState ( )

Constructor. Creates an empty channel.
## void assignFrom ( const Ptr < AnimationChannelEventState > & channel )

Copies the content of the specified channel into this one.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationChannelEventState](../../../../api/library/animations/timeline/class.animationchanneleventstate_cpp.md)> &* **channel** - Source channel to copy the content from.

## int addInterval ( float start , float end , int payload )

Adds an interval to the channel. The begin phase is raised when the playhead enters it and the end phase when it leaves.
### Arguments

- *float* **start** - Moment the interval opens at, in seconds.
- *float* **end** - Moment the interval closes at, in seconds.
- *int* **payload** - Payload carried by the interval.

### Return value

Number of the new interval.
## void setInterval ( int index , float start , float end , int payload )

Sets the bounds and the payload of the specified interval.
### Arguments

- *int* **index** - Interval number.
- *float* **start** - Moment the interval opens at, in seconds.
- *float* **end** - Moment the interval closes at, in seconds.
- *int* **payload** - Payload carried by the interval.

## void removeInterval ( int index )

Removes the specified interval from the channel.
### Arguments

- *int* **index** - Interval number.

## void clearIntervals ( )

Removes all intervals from the channel.
## float getIntervalStart ( int index ) const

Returns the moment the specified interval opens at.
### Arguments

- *int* **index** - Interval number.

### Return value

Moment the interval opens at, in seconds.
## float getIntervalEnd ( int index ) const

Returns the moment the specified interval closes at.
### Arguments

- *int* **index** - Interval number.

### Return value

Moment the interval closes at, in seconds.
## int getIntervalPayload ( int index ) const

Returns the payload carried by the specified interval.
### Arguments

- *int* **index** - Interval number.

### Return value

Payload carried by the interval.
