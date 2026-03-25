# Unigine::AnimationPlayback Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage [animation playbacks](../../../../principles/animations/index.md#animation_playback) via code.


## AnimationPlayback Class

### Members

## getNumObjects () const

Returns the current total number of [animation objects](../../../../principles/animations/index.md#animation_object) controlled within all the [tracks](../../../../principles/animations/index.md#animation_track) in the playback.
### Return value

Current number of animation objects controlled within all the tracks in the playback.
## int isPlaying () const

Returns the current value indicating if the playback is currently being played.
### Return value

Current the playback is currently being played
## int isStopped () const

Returns the current value indicating if the playback is currently stopped.
### Return value

Current the playback is currently stopped
## getDuration () const

Returns the current total playback duration, in seconds.
### Return value

Current playback duration, in seconds.
## void setTimeTo ( float to )

Sets a new playback end time, in seconds.
### Arguments

- *float* **to** - The playback end time, in seconds.

## float getTimeTo () const

Returns the current playback end time, in seconds.
### Return value

Current playback end time, in seconds.
## void setTimeFrom ( float from )

Sets a new playback start time, in seconds.
### Arguments

- *float* **from** - The playback start time, in seconds.

## float getTimeFrom () const

Returns the current playback start time, in seconds.
### Return value

Current playback start time, in seconds.
## void setSpeed ( )

Sets a new speed factor for the animation playback. This parameter enables you to control how fast the particular playback should be played giving you more flexibility and control (for example, you can use it for slow-motion effect).
### Arguments

- **speed** - The playback speed factor (the value of 2 means that the track is played 2 times faster, while 0.5f will slow it down 2 times).

## getSpeed () const

Returns the current speed factor for the animation playback. This parameter enables you to control how fast the particular playback should be played giving you more flexibility and control (for example, you can use it for slow-motion effect).
### Return value

Current playback speed factor (the value of 2 means that the track is played 2 times faster, while 0.5f will slow it down 2 times).
## void setLoop ( int loop )

Sets a new value indicating if the playback is looped.
### Arguments

- *int* **loop** - The the playback is looped

## int isLoop () const

Returns the current value indicating if the playback is looped.
### Return value

Current the playback is looped
---

## AnimationPlayback ( )

Constructor. Creates an empty playback with default settings.
## AnimationObject getObject ( int index )

Returns an [animation object](../../../../principles/animations/index.md#animation_object) by its index.
### Arguments

- *int* **index** - Animation object index.

### Return value

Animation object with the specified index.
## int containsObject ( AnimationObject anim_obj )

Returns a value indicating if the animation playback contains the specified [animation object](../../../../principles/animations/index.md#animation_object).
### Arguments

- *[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_usc.md)* **anim_obj** - Animation object to be checked.

### Return value

**1** if the the animation playback contains the specified animation object; otherwise, **0**.
## void clear ( )

Clears the animation playback removing all animation objects, layers and tracks from it.
## void apply ( float time )

Calculates actual values for all modifiers of all tracks played at the specified moment (taking weights into account) and applied to real animated objects (overrides of animation objects for this playback).
### Arguments

- *float* **time** - Time value for which the resulting changes are to be calculated and applied to animated objects.

## void apply ( AnimationFrame frame )

Applies the specified animation frame - actual values are calculated for all modifiers of all tracks played at this frame (taking weights into account) and applied to real animated objects (overrides of animation objects for this playback).
### Arguments

- *[AnimationFrame](../../../../api/library/animations/timeline/class.animationframe_usc.md)* **frame** - Animation frame to be applied.

## void play ( )

Plays the animation playback either from the start or from the moment when the playback was paused (see *[pause()()](../../../...md#pause_void)*).
## void pause ( )

Pauses the animation playback, so the playback can be resumed from this moment upon calling *[play()()](../../../...md#play_void)*.
## void stop ( )

Stops the animation playback.
## void setTrack ( AnimationTrack track )

Sets the first animation [track](../../../../principles/animations/index.md#animation_track) of the first [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *[AnimationTrack](../../../../api/library/animations/timeline/class.animationtrack_usc.md)* **track** - New animation track to be set as the first track of the first layer.

## AnimationTrack getTrack ( )

Returns the first animation [track](../../../../principles/animations/index.md#animation_track) of the first [layer](../../../../principles/animations/index.md#animation_layer).
### Return value

First animation track of the first layer.
## int addLayer ( )

Adds a new animation [layer](../../../../principles/animations/index.md#animation_layer) to the playback.
### Return value

Index of the new added layer.
## int addLayer ( AnimationTrack track )

Adds a new animation [layer](../../../../principles/animations/index.md#animation_layer) to the playback and adds the specified animation [track](../../../../principles/animations/index.md#animation_track) to this new layer.
### Arguments

- *[AnimationTrack](../../../../api/library/animations/timeline/class.animationtrack_usc.md)* **track** - Animation track to be added to the new created layer.

### Return value

Index of the new added layer.
## void removeLayer ( int index )

Removes the animation [layer](../../../../principles/animations/index.md#animation_layer) with the specified index from the playback.
### Arguments

- *int* **index** - Index of the layer to be removed.

## int getNumLayers ( )

Returns the total number of animation [layers](../../../../principles/animations/index.md#animation_layer) in the playback.
## int addLayerTrack ( int layer_index )

Adds a new empty animation track to the [layer](../../../../principles/animations/index.md#animation_layer) with the specified index.
### Arguments

- *int* **layer_index** - Layer index.

### Return value

Index of the new added animation track.
## int addLayerTrack ( int layer_index , AnimationTrack track )

Adds the specified animation [track](../../../../principles/animations/index.md#animation_track) to the [layer](../../../../principles/animations/index.md#animation_layer) with the specified index.
### Arguments

- *int* **layer_index** - Layer index.
- *[AnimationTrack](../../../../api/library/animations/timeline/class.animationtrack_usc.md)* **track** - New track to be added to the layer.

### Return value

Index of the new added animation track.
## void removeLayerTrack ( int layer_index , int track_index )

Removes the animation [track](../../../../principles/animations/index.md#animation_track) with the specified index from the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Index of the layer containing the track to be removed.
- *int* **track_index** - Index of the track to be removed.

## int getNumLayerTracks ( int layer_index )

Returns the number of animation [tracks](../../../../principles/animations/index.md#animation_track) for the [layer](../../../../principles/animations/index.md#animation_layer) with the specified index.
### Arguments

- *int* **layer_index** - Layer index.

### Return value

Number of animation tracks for the layer.
## void setLayerTrack ( int layer_index , int track_index , AnimationTrack track )

Sets the specified animation [track](../../../../principles/animations/index.md#animation_track) by index for the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.
- *[AnimationTrack](../../../../api/library/animations/timeline/class.animationtrack_usc.md)* **track** - Animation track to be set for the given layer.

## AnimationTrack getLayerTrack ( int layer_index , int track_index )

Returns the animation [track](../../../../principles/animations/index.md#animation_track) by index for the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.

### Return value

Animation track set for the given layer.
## void setLayerTrackBeginTime ( int layer_index , int track_index , float offest )

Sets a new offset time (from the beginning of the playback) for the specified [track](../../../../principles/animations/index.md#animation_track) of the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.
- *float* **offest** - Offset time to be set, in seconds.

## float getLayerTrackBeginTime ( int layer_index , int track_index )

Returns the current offset time (from the beginning of the playback) for the specified [track](../../../../principles/animations/index.md#animation_track) of the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.

### Return value

Current offset time, in seconds.
## void setLayerTrackSpeed ( int layer_index , int track_index , float speed )

Sets a new speed factor value for the specified [track](../../../../principles/animations/index.md#animation_track) of the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.
- *float* **speed** - New speed factor value to be set (the value of 2 means that the track is played 2 times faster, while 0.5f will slow it down 2 times).

## float getLayerTrackSpeed ( int layer_index , int track_index )

Returns the current speed factor value for the specified [track](../../../../principles/animations/index.md#animation_track) of the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.

### Return value

Current speed factor value (the value of 2 means that the track is played 2 times faster, while 0.5f will slow it down 2 times).
## void setLayerTrackApplyBefore ( int layer_index , int track_index , int is_apply )

Sets the flag specifying if the start frame of the track is applied to the playback before the track starts.
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.
- *int* **is_apply** - **1** to enable applying the start frame of the track before the track starts; **0** - to disable it.

## int isLayerTrackApplyBefore ( int layer_index , int track_index )

Returns the flag specifying if the the start frame of the track is applied to the playback before the track starts.
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.

### Return value

**1** if the start frame of the track is applied to the playback before the track starts; otherwise **0**.
## void setLayerTrackApplyAfter ( int layer_index , int track_index , int is_apply )

Sets the flag specifying if the end frame of the track is applied to the playback after the track ends.
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.
- *int* **is_apply** - **1** to enable applying the end frame of the track after the track ends; **0** - to disable it.

## int isLayerTrackApplyAfter ( int layer_index , int track_index )

Returns the flag specifying if the end frame of the track is applied to the playback after the track ends.
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.

### Return value

**1** if the end frame of the track is applied to the playback after the track ends; **0** - to disable it.
## void setLayerTrackWeightCurve ( int layer_index , int track_index , const AnimationCurveFloat curve )

Sets a new weight curve for the specified [track](../../../../principles/animations/index.md#animation_track) of the specified [layer](../../../../principles/animations/index.md#animation_layer). Weights are used for [mixing](../../../../principles/animations/index.md#animation_track_blending) multiple simultaneously played tracks together. The weight curve defines the dynamics of track weight change over time.
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.
- *const [AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_usc.md)* **curve** - Weight curve to be set for the specified track.

## AnimationCurveFloat getLayerTrackWeightCurve ( int layer_index , int track_index )

Returns the current weight curve for the specified [track](../../../../principles/animations/index.md#animation_track) of the specified [layer](../../../../principles/animations/index.md#animation_layer). Weights are used for [mixing](../../../../principles/animations/index.md#animation_track_blending) multiple simultaneously played tracks together. The weight curve defines the dynamics of track weight change over time.
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.

### Return value

Weight curve for the specified track.
## void setLayerTrackLinearFade ( int layer_index , int track_index , float effect_time , int use_fade_in , int use_fade_out )

Enables linear fading (in, out, or both) for the track across the specified effect time span. This method automatically updates the [weight](../../../../principles/animations/index.md#animation_track_blending) curve for the track.
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.
- *float* **effect_time** - Time interval (in seconds) across which the fading effect is applied. Both fade-in and fade-out intervals (if used together) are equal to this value.
- *int* **use_fade_in** - Set **1** to enable the fade-in effect for the track; **0** - to disable it.
- *int* **use_fade_out** - Set **1** to enable the fade-out effect for the track; **0** - to disable it.

## float getLayerTrackDuration ( int layer_index , int track_index )

Returns the current duration for the specified [track](../../../../principles/animations/index.md#animation_track) of the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.

### Return value

Track duration, in seconds.
## float getLayerTrackEndTime ( int layer_index , int track_index )

Returns the current end time for the specified [track](../../../../principles/animations/index.md#animation_track) of the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.

### Return value

Track end time, in seconds.
## float getLayerDuration ( int layer_index )

Returns the duration of the animation [layer](../../../../principles/animations/index.md#animation_layer) with the specified index.
### Arguments

- *int* **layer_index** - Layer index.

### Return value

Duration of the layer, in seconds.
## void setTime ( float time , float from = -1.0f , float to = -1.0f )

Sets the current playback time, and optional from and to limits.
### Arguments

- *float* **time** - Current playback time to be set, in seconds.
- *float* **from** - Start time to be set, in seconds.
- *float* **to** - End time to be set, in seconds.

## float getTime ( )

Returns the current playback time, in seconds.
### Return value

Current playback time, in seconds.
