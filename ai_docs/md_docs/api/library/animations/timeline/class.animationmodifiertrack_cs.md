# Unigine::AnimationModifierTrack Class (CS)

**Inherits from:** AnimationModifier


This class represents an interface enabling you to use tracks in animation.


## AnimationModifierTrack Class

### Members

---

## AnimationModifierTrack ( )

Constructor. Creates a new modifier to animate objects using tracks.
## void AddTrack ( string path , float begin_time )

Adds a track at the specified point of the timeline.
### Arguments

- *string* **path** - Path to the track.
- *float* **begin_time** - Time on the timeline, in seconds, for this track to start.

## void SetTrackTimeCurve ( AnimationCurveFloat curve )

Sets the time curve to be used by the track.
### Arguments

- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **curve** - Time curve for the track.
