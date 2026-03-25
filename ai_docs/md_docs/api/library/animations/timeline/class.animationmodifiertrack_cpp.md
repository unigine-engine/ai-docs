# Unigine::AnimationModifierTrack Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationModifier


This class represents an interface enabling you to use tracks in animation.


## AnimationModifierTrack Class

---

## AnimationModifierTrack ( )

Constructor. Creates a new modifier to animate objects using tracks.
## void addTrack ( const char * path , float begin_time )

Adds a track at the specified point of the timeline.
### Arguments

- *const char ** **path** - Path to the track.
- *float* **begin_time** - Time on the timeline, in seconds, for this track to start.

## void setTrackTimeCurve ( const Ptr < AnimationCurveFloat > & curve )

Sets the time curve to be used by the track.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)> &* **curve** - Time curve for the track.
