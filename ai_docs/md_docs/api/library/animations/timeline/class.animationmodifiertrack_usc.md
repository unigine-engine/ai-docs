# Unigine::AnimationModifierTrack Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** AnimationModifier


This class represents an interface enabling you to use tracks in animation.


## AnimationModifierTrack Class

---

## AnimationModifierTrack ( )

Constructor. Creates a new modifier to animate objects using tracks.
## void addTrack ( string path , float begin_time )

Adds a track at the specified point of the timeline.
### Arguments

- *string* **path** - Path to the track.
- *float* **begin_time** - Time on the timeline, in seconds, for this track to start.

## void setTrackTimeCurve ( AnimationCurveFloat curve )

Sets the time curve to be used by the track.
### Arguments

- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_usc.md)* **curve** - Time curve for the track.
