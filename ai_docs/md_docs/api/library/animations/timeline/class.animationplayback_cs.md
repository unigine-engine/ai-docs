# Unigine::AnimationPlayback Class (CS)


This class is used to manage [animation playbacks](../../../../principles/animations/index.md#animation_playback) via code.


## AnimationPlayback Class

### Properties

## 🔒︎ int NumObjects

The total number of [animation objects](../../../../principles/animations/index.md#animation_object) controlled within all the [tracks](../../../../principles/animations/index.md#animation_track) in the playback.
## 🔒︎ bool IsPlaying

The value indicating if the playback is currently being played.
## 🔒︎ bool IsStopped

The value indicating if the playback is currently stopped.
## 🔒︎ float Duration

The total playback duration, in seconds.
## float TimeTo

The playback end time, in seconds.
## float TimeFrom

The playback start time, in seconds.
## float Speed

The speed factor for the animation playback. This parameter enables you to control how fast the particular playback should be played giving you more flexibility and control (for example, you can use it for slow-motion effect).
## bool Loop

The value indicating if the playback is looped.
### Members

---

## AnimationPlayback ( )

Constructor. Creates an empty playback with default settings.
## AnimationObject GetObject ( int index )

Returns an [animation object](../../../../principles/animations/index.md#animation_object) by its index.
### Arguments

- *int* **index** - Animation object index.

### Return value

Animation object with the specified index.
## bool ContainsObject ( AnimationObject anim_obj )

Returns a value indicating if the animation playback contains the specified [animation object](../../../../principles/animations/index.md#animation_object).
### Arguments

- *[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_cs.md)* **anim_obj** - Animation object to be checked.

### Return value

true if the the animation playback contains the specified animation object; otherwise, false.
## void Clear ( )

Clears the animation playback removing all animation objects, layers and tracks from it.
## void Apply ( float time )

Calculates actual values for all modifiers of all tracks played at the specified moment (taking weights into account) and applied to real animated objects (overrides of animation objects for this playback).
### Arguments

- *float* **time** - Time value for which the resulting changes are to be calculated and applied to animated objects.

## void Apply ( AnimationFrame frame )

Applies the specified animation frame - actual values are calculated for all modifiers of all tracks played at this frame (taking weights into account) and applied to real animated objects (overrides of animation objects for this playback).
### Arguments

- *[AnimationFrame](../../../../api/library/animations/timeline/class.animationframe_cs.md)* **frame** - Animation frame to be applied.

## void Play ( )

Plays the animation playback either from the start or from the moment when the playback was paused (see *[Pause()](../../../...md#pause_void)*).
## void Pause ( )

Pauses the animation playback, so the playback can be resumed from this moment upon calling *[Play()](../../../...md#play_void)*.
## void Stop ( )

Stops the animation playback.
## void SetTrack ( AnimationTrack track )

Sets the first animation [track](../../../../principles/animations/index.md#animation_track) of the first [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *[AnimationTrack](../../../../api/library/animations/timeline/class.animationtrack_cs.md)* **track** - New animation track to be set as the first track of the first layer.

## AnimationTrack GetTrack ( )

Returns the first animation [track](../../../../principles/animations/index.md#animation_track) of the first [layer](../../../../principles/animations/index.md#animation_layer).
### Return value

First animation track of the first layer.
## int AddLayer ( )

Adds a new animation [layer](../../../../principles/animations/index.md#animation_layer) to the playback.
### Return value

Index of the new added layer.
## int AddLayer ( AnimationTrack track )

Adds a new animation [layer](../../../../principles/animations/index.md#animation_layer) to the playback and adds the specified animation [track](../../../../principles/animations/index.md#animation_track) to this new layer.
### Arguments

- *[AnimationTrack](../../../../api/library/animations/timeline/class.animationtrack_cs.md)* **track** - Animation track to be added to the new created layer.

### Return value

Index of the new added layer.
## void RemoveLayer ( int index )

Removes the animation [layer](../../../../principles/animations/index.md#animation_layer) with the specified index from the playback.
### Arguments

- *int* **index** - Index of the layer to be removed.

## int GetNumLayers ( )

Returns the total number of animation [layers](../../../../principles/animations/index.md#animation_layer) in the playback.
## int AddLayerTrack ( int layer_index )

Adds a new empty animation track to the [layer](../../../../principles/animations/index.md#animation_layer) with the specified index.
### Arguments

- *int* **layer_index** - Layer index.

### Return value

Index of the new added animation track.
## int AddLayerTrack ( int layer_index , AnimationTrack track )

Adds the specified animation [track](../../../../principles/animations/index.md#animation_track) to the [layer](../../../../principles/animations/index.md#animation_layer) with the specified index.
### Arguments

- *int* **layer_index** - Layer index.
- *[AnimationTrack](../../../../api/library/animations/timeline/class.animationtrack_cs.md)* **track** - New track to be added to the layer.

### Return value

Index of the new added animation track.
## void RemoveLayerTrack ( int layer_index , int track_index )

Removes the animation [track](../../../../principles/animations/index.md#animation_track) with the specified index from the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Index of the layer containing the track to be removed.
- *int* **track_index** - Index of the track to be removed.

## int GetNumLayerTracks ( int layer_index )

Returns the number of animation [tracks](../../../../principles/animations/index.md#animation_track) for the [layer](../../../../principles/animations/index.md#animation_layer) with the specified index.
### Arguments

- *int* **layer_index** - Layer index.

### Return value

Number of animation tracks for the layer.
## void SetLayerTrack ( int layer_index , int track_index , AnimationTrack track )

Sets the specified animation [track](../../../../principles/animations/index.md#animation_track) by index for the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.
- *[AnimationTrack](../../../../api/library/animations/timeline/class.animationtrack_cs.md)* **track** - Animation track to be set for the given layer.

## AnimationTrack GetLayerTrack ( int layer_index , int track_index )

Returns the animation [track](../../../../principles/animations/index.md#animation_track) by index for the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.

### Return value

Animation track set for the given layer.
## void SetLayerTrackBeginTime ( int layer_index , int track_index , float offest )

Sets a new offset time (from the beginning of the playback) for the specified [track](../../../../principles/animations/index.md#animation_track) of the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.
- *float* **offest** - Offset time to be set, in seconds.

## float GetLayerTrackBeginTime ( int layer_index , int track_index )

Returns the current offset time (from the beginning of the playback) for the specified [track](../../../../principles/animations/index.md#animation_track) of the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.

### Return value

Current offset time, in seconds.
## void SetLayerTrackSpeed ( int layer_index , int track_index , float speed )

Sets a new speed factor value for the specified [track](../../../../principles/animations/index.md#animation_track) of the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.
- *float* **speed** - New speed factor value to be set (the value of 2 means that the track is played 2 times faster, while 0.5f will slow it down 2 times).

## float GetLayerTrackSpeed ( int layer_index , int track_index )

Returns the current speed factor value for the specified [track](../../../../principles/animations/index.md#animation_track) of the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.

### Return value

Current speed factor value (the value of 2 means that the track is played 2 times faster, while 0.5f will slow it down 2 times).
## void SetLayerTrackApplyBefore ( int layer_index , int track_index , bool is_apply )

Sets the flag specifying if the start frame of the track is applied to the playback before the track starts.
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.
- *bool* **is_apply** - true to enable applying the start frame of the track before the track starts; false - to disable it.

## bool IsLayerTrackApplyBefore ( int layer_index , int track_index )

Returns the flag specifying if the the start frame of the track is applied to the playback before the track starts.
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.

### Return value

true if the start frame of the track is applied to the playback before the track starts; otherwise false.
## void SetLayerTrackApplyAfter ( int layer_index , int track_index , bool is_apply )

Sets the flag specifying if the end frame of the track is applied to the playback after the track ends.
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.
- *bool* **is_apply** - true to enable applying the end frame of the track after the track ends; false - to disable it.

## bool IsLayerTrackApplyAfter ( int layer_index , int track_index )

Returns the flag specifying if the end frame of the track is applied to the playback after the track ends.
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.

### Return value

true if the end frame of the track is applied to the playback after the track ends; false - to disable it.
## void SetLayerTrackWeightCurve ( int layer_index , int track_index , AnimationCurveFloat curve )

Sets a new weight curve for the specified [track](../../../../principles/animations/index.md#animation_track) of the specified [layer](../../../../principles/animations/index.md#animation_layer). Weights are used for [mixing](../../../../principles/animations/index.md#animation_track_blending) multiple simultaneously played tracks together. The weight curve defines the dynamics of track weight change over time.
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **curve** - Weight curve to be set for the specified track.

## AnimationCurveFloat GetLayerTrackWeightCurve ( int layer_index , int track_index )

Returns the current weight curve for the specified [track](../../../../principles/animations/index.md#animation_track) of the specified [layer](../../../../principles/animations/index.md#animation_layer). Weights are used for [mixing](../../../../principles/animations/index.md#animation_track_blending) multiple simultaneously played tracks together. The weight curve defines the dynamics of track weight change over time.
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.

### Return value

Weight curve for the specified track.
## void SetLayerTrackLinearFade ( int layer_index , int track_index , float effect_time , bool use_fade_in , bool use_fade_out )

Enables linear fading (in, out, or both) for the track across the specified effect time span. This method automatically updates the [weight](../../../../principles/animations/index.md#animation_track_blending) curve for the track.
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.
- *float* **effect_time** - Time interval (in seconds) across which the fading effect is applied. Both fade-in and fade-out intervals (if used together) are equal to this value.
- *bool* **use_fade_in** - Set true to enable the fade-in effect for the track; false - to disable it.
- *bool* **use_fade_out** - Set true to enable the fade-out effect for the track; false - to disable it.

## float GetLayerTrackDuration ( int layer_index , int track_index )

Returns the current duration for the specified [track](../../../../principles/animations/index.md#animation_track) of the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.

### Return value

Track duration, in seconds.
## float GetLayerTrackEndTime ( int layer_index , int track_index )

Returns the current end time for the specified [track](../../../../principles/animations/index.md#animation_track) of the specified [layer](../../../../principles/animations/index.md#animation_layer).
### Arguments

- *int* **layer_index** - Layer index.
- *int* **track_index** - Track index.

### Return value

Track end time, in seconds.
## float GetLayerDuration ( int layer_index )

Returns the duration of the animation [layer](../../../../principles/animations/index.md#animation_layer) with the specified index.
### Arguments

- *int* **layer_index** - Layer index.

### Return value

Duration of the layer, in seconds.
## void SetTime ( float time , float from = -1.0f , float to = -1.0f )

Sets the current playback time, and optional from and to limits.
### Arguments

- *float* **time** - Current playback time to be set, in seconds.
- *float* **from** - Start time to be set, in seconds.
- *float* **to** - End time to be set, in seconds.

## float GetTime ( )

Returns the current playback time, in seconds.
### Return value

Current playback time, in seconds.
