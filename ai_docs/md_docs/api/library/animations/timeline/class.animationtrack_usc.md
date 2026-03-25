# Unigine::AnimationTrack Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage [animation tracks](../../../../principles/animations/index.md#animation_track) via code.


## AnimationTrack Class

### Members

## UGUID getGUID () const

Returns the current GUID of the animation track.
### Return value

Current track GUID.
## void setName ( string name )

Sets a new name of the animation track.
### Arguments

- *string* **name** - The track name.

## const char * getName () const

Returns the current name of the animation track.
### Return value

Current track name.
## getNumObjects () const

Returns the current total number of [animation objects](../../../../principles/animations/index.md#animation_object) controlled by the [track](../../../../principles/animations/index.md#animation_track).
### Return value

Current number of animation objects controlled by the track.
## getDuration () const

Returns the current total track duration, in seconds.
### Return value

Current track duration, in seconds.
## getManualDuration () const

Returns the current
### Return value

Current
## const char * getPath () const

Returns the current path to the track file.
### Return value

Current track file path.
## void setEventCurve ( AnimationCurveInt curve )

Sets a new event curve for the track. Events enable you to call a function or method directly from the animation at a certtain frame/time that you specify. You can use events, for example, to play a sound effect or perform any other actions at any moment on the timeline. The key values on this curve define which events are to be triggered at the corresponding moments. You define the desired list of events as a enumeration, and then simply add keys with the certain enum values to the curve at certain moments when you want the corresponding event to occur.
### Arguments

- *[AnimationCurveInt](../../../../api/library/animations/timeline/class.animationcurveint_usc.md)* **curve** - The event curve for the track.

## AnimationCurveInt getEventCurve () const

Returns the current event curve for the track. Events enable you to call a function or method directly from the animation at a certtain frame/time that you specify. You can use events, for example, to play a sound effect or perform any other actions at any moment on the timeline. The key values on this curve define which events are to be triggered at the corresponding moments. You define the desired list of events as a enumeration, and then simply add keys with the certain enum values to the curve at certain moments when you want the corresponding event to occur.
### Return value

Current event curve for the track.
---

## AnimationTrack ( )

Constructor. Creates an empty track with default settings.
## AnimationTrack ( string name )

Constructor. Creates an empty track with default settings and specified name.
### Arguments

- *string* **name** - Animation track name.

## void copy ( AnimationTrack track )

Copies all data from the specified source track to the track.
### Arguments

- *[AnimationTrack](../../../../api/library/animations/timeline/class.animationtrack_usc.md)* **track** - Source animation track.

## void clear ( )

Clears the animation track removing all animation objects and modifiers from it. This method also resets track duration to 0.
## int containsObject ( AnimationObject anim_obj )

Returns a value indicating if the animation track contains the specified [animation object](../../../../principles/animations/index.md#animation_object).
### Arguments

- *[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_usc.md)* **anim_obj** - Animation object to be checked.

### Return value

**1** if the the animation playback contains the specified animation object; otherwise, **0**.
## AnimationObject getObject ( int index )

Returns an [animation object](../../../../principles/animations/index.md#animation_object) by its index.
### Arguments

- *int* **index** - Animation object index.

### Return value

Animation object with the specified index.
## int addObject ( AnimationObject anim_obj )

Adds the specified [animation object](../../../../principles/animations/index.md#animation_object) to the track.
### Arguments

- *[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_usc.md)* **anim_obj** - Animation object to be added.

### Return value

Index of the new animation object added on success; otherwise, -1.
## void removeObject ( AnimationObject anim_obj )

Removes the specified [animation object](../../../../principles/animations/index.md#animation_object) along with all modifiers added for it.
### Arguments

- *[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_usc.md)* **anim_obj** - Animation object to be removed.

## void addObjectModifier ( AnimationObject anim_obj , AnimationModifier modifier )

Adds the specified [modifier](../../../../principles/animations/index.md#animation_modifier) to the specified [animation object](../../../../principles/animations/index.md#animation_object) to control changes of a certain parameter over time.
### Arguments

- *[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_usc.md)* **anim_obj** - Target animation object to which a modifier should be added.
- *[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_usc.md)* **modifier** - Animation modifier to be added.

## int updateObjectModifier ( AnimationObject anim_obj , AnimationModifier modifier )

Updates the specified [modifier](../../../../principles/animations/index.md#animation_modifier) for the specified [animation object](../../../../principles/animations/index.md#animation_object).
### Arguments

- *[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_usc.md)* **anim_obj** - Target animation object to which a modifier should be added.
- *[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_usc.md)* **modifier** - New source animation modifier to be used.

### Return value

**1** if the specified modifier was successfully updated for the animation object; otherwise, **0**.
## void removeObjectModifier ( AnimationObject anim_obj , AnimationModifier modifier )

Removes the specified [modifier](../../../../principles/animations/index.md#animation_modifier) from the specified [animation object](../../../../principles/animations/index.md#animation_object).
### Arguments

- *[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_usc.md)* **anim_obj** - Target animation object from which a modifier should be removed.
- *[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_usc.md)* **modifier** - Animation modifier to be removed.

## int getObjectModifiers ( AnimationObject anim_obj , Vector< AnimationModifier >& OUT_out_modifiers )

Collects all modifiers for the specified [animation object](../../../../principles/animations/index.md#animation_object) and puts them to the **out_modifiers** buffer.
### Arguments

- *[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_usc.md)* **anim_obj** - Animation object.
- *Vector<[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_usc.md)>&* **OUT_out_modifiers** - Output buffer for the list of all modifiers for the specified object. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of modifiers for the specified object.
## void addObjectModifier ( string anim_obj_name , AnimationModifier modifier )

Adds the specified [modifier](../../../../principles/animations/index.md#animation_modifier) to the [animation object](../../../../principles/animations/index.md#animation_object) with the specified name to control changes of a certain parameter over time.
### Arguments

- *string* **anim_obj_name** - Name of the target animation object to which a modifier should be added.
- *[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_usc.md)* **modifier** - Animation modifier to be added.

## void addSingletonModifier ( AnimationModifier modifier )

Adds the specified singleton animation [modifier](../../../../principles/animations/index.md#animation_modifier) to control changes of a certain parameter of some Engine's singleton class, such as *[Physics](../../../../api/library/physics/class.physics_usc.md), [Render](../../../../api/library/rendering/class.render_usc.md)*, etc.
### Arguments

- *[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_usc.md)* **modifier** - Singleton animation modifier to be added.

## int updateSingletonModifier ( AnimationModifier modifier )

Updates the specified singleton animation [modifier](../../../../principles/animations/index.md#animation_modifier) used to control changes of a certain parameter of some Engine's singleton class, such as *[Physics](../../../../api/library/physics/class.physics_usc.md), [Render](../../../../api/library/rendering/class.render_usc.md)*, etc.
### Arguments

- *[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_usc.md)* **modifier** - Singleton animation modifier to be updated.

### Return value

**1** if the specified singleton modifier was successfully updated; otherwise, **0**.
## void removeSingletonModifier ( AnimationModifier modifier )

Removes the specified singleton animation [modifier](../../../../principles/animations/index.md#animation_modifier) from the track.
### Arguments

- *[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_usc.md)* **modifier** - Singleton animation modifier to be removed.

## int getSingletonModifiers ( Vector< AnimationModifier >& OUT_out_modifiers )

Collects all singleton animation modifiers of the track and puts them to the **out_modifiers** buffer.
### Arguments

- *Vector<[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_usc.md)>&* **OUT_out_modifiers** - Output buffer for the list of all singleton modifiers of the track. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of singleton animation modifiers of the track.
## AnimationFrame getFrame ( float time )

Returns the [animation frame](../../../../principles/animations/index.md#animation_frame) for the specified moment of time. A frame can be thought of as a vertical slice of values of all tracks and modifiers played at the specified moment.
### Arguments

- *float* **time** - Time (in seconds) for which a frame is to be obtained.

### Return value

Animation frame for the specified time.
## AnimationFrame getFrameByNormalizedTime ( float time )

Returns the [animation frame](../../../../principles/animations/index.md#animation_frame) for the specified moment of time (normalized). A frame can be thought of as a vertical slice of values of all tracks and modifiers played at the specified moment.
### Arguments

- *float* **time** - Normalized time value (in the [0.0f, 1.0f] range) for which a frame is to be obtained .

### Return value

Animation frame for the specified time.
