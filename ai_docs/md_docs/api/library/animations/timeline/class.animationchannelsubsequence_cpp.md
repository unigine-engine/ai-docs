# Unigine::AnimationChannelSubSequence Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationChannel


This channel plays whole sequences as clips, which is how a long animation is assembled out of shorter ones. Each clip stands for one placement of a nested [sequence](../../../../api/library/animations/timeline/class.animationsequence_cpp.md) and can be trimmed, retimed and blended like any other clip.


A nested sequence comes either from an asset, shared with everything else that uses it, or embedded in the host sequence and owned by it. Each placement gets an identity of its own, which is what lets the same nested animation drive different objects in two places of one composition.


## AnimationChannelSubSequence Class

---

## AnimationChannelSubSequence ( )

Constructor. Creates an empty channel.
## void assignFrom ( const Ptr < AnimationChannelSubSequence > & channel )

Copies the content of the specified channel into this one.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationChannelSubSequence](../../../../api/library/animations/timeline/class.animationchannelsubsequence_cpp.md)> &* **channel** - Source channel to copy the content from.

## int addSubSequence ( float begin_time , float length , const UGUID & sequence_guid )

Adds a clip that plays a sequence stored in an asset. The asset stays shared, so editing it changes every composition that nests it.
### Arguments

- *float* **begin_time** - Moment the clip starts at, in seconds.
- *float* **length** - Length of the clip, in seconds. A value of zero or less makes the clip stretch to the next one on the same row.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **sequence_guid** - GUID of the sequence asset to be played by the clip.

### Return value

Number of the new clip.
## int addEmbeddedSubSequence ( float begin_time , float length , const Ptr < AnimationSequence > & sequence )

Adds a clip that carries a sequence of its own. An embedded sequence is stored inside the host one, travels with it and is shared with nothing else.
### Arguments

- *float* **begin_time** - Moment the clip starts at, in seconds.
- *float* **length** - Length of the clip, in seconds. A value of zero or less makes the clip stretch to the next one on the same row.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationSequence](../../../../api/library/animations/timeline/class.animationsequence_cpp.md)> &* **sequence** - Sequence to be played by the clip.

### Return value

Number of the new clip.
