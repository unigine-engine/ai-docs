# Unigine::AnimationTrack Class (CPP)

**Header:** #include <UnigineAnimation.h>


This class is used to manage [animation tracks](../../../../principles/animations/index.md#animation_track) via code.


## AnimationTrack Class

### Members

## UGUID getGUID () const

Returns the current GUID of the animation track.
### Return value

Current track GUID.
## void setName ( const char * name )

Sets a new name of the animation track.
### Arguments

- *const char ** **name** - The track name.

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
## void setEventCurve ( const Ptr < AnimationCurveInt >& curve )

Sets a new event curve for the track. Events enable you to call a function or method directly from the animation at a certtain frame/time that you specify. You can use events, for example, to play a sound effect or perform any other actions at any moment on the timeline. The key values on this curve define which events are to be triggered at the corresponding moments. You define the desired list of events as a enumeration, and then simply add keys with the certain enum values to the curve at certain moments when you want the corresponding event to occur.
```cpp
// enumeration that defines all available events
enum
{
	EVENT_PLAY_SOUND = 0, 		// on this event we play a sound
	EVENT_CONSOLE_MESSAGE,		// on this event we print a message to the console
	//...
};

// handler function used to process all events by their IDs
void on_event(int id)
{
	if (id == EVENT_PLAY_SOUND)
	{
		sound->stop();
		sound->play();
	}

	if (id == EVENT_CONSOLE_MESSAGE)
	{
		Console::onscreenMessageLine(vec4_blue, "A message.");
	}

	// ...
}

// creating a track for events
AnimationTrackPtr event_track = AnimationTrack::create();

// creating a track for events
AnimationCurveIntPtr event_curve = AnimationCurveInt::create();
event_curve->addKey(1.25f, EVENT_PLAY_SOUND);
event_curve->addKey(2.07f, EVENT_CONSOLE_MESSAGE);
event_curve->addKey(2.75f, EVENT_PLAY_SOUND);
event_track->setEventCurve(event_curve);

// adding a track to the playback
playback->addLayer(event_track);

// adding a callback handler to process events
event_track->addEventCallback(MakeCallback(on_event));


```


### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveInt](../../../../api/library/animations/timeline/class.animationcurveint_cpp.md)>&* **curve** - The event curve for the track.

## Ptr < AnimationCurveInt > getEventCurve () const

Returns the current event curve for the track. Events enable you to call a function or method directly from the animation at a certtain frame/time that you specify. You can use events, for example, to play a sound effect or perform any other actions at any moment on the timeline. The key values on this curve define which events are to be triggered at the corresponding moments. You define the desired list of events as a enumeration, and then simply add keys with the certain enum values to the curve at certain moments when you want the corresponding event to occur.
```cpp
// enumeration that defines all available events
enum
{
	EVENT_PLAY_SOUND = 0, 		// on this event we play a sound
	EVENT_CONSOLE_MESSAGE,		// on this event we print a message to the console
	//...
};

// handler function used to process all events by their IDs
void on_event(int id)
{
	if (id == EVENT_PLAY_SOUND)
	{
		sound->stop();
		sound->play();
	}

	if (id == EVENT_CONSOLE_MESSAGE)
	{
		Console::onscreenMessageLine(vec4_blue, "A message.");
	}

	// ...
}

// creating a track for events
AnimationTrackPtr event_track = AnimationTrack::create();

// creating a track for events
AnimationCurveIntPtr event_curve = AnimationCurveInt::create();
event_curve->addKey(1.25f, EVENT_PLAY_SOUND);
event_curve->addKey(2.07f, EVENT_CONSOLE_MESSAGE);
event_curve->addKey(2.75f, EVENT_PLAY_SOUND);
event_track->setEventCurve(event_curve);

// adding a track to the playback
playback->addLayer(event_track);

// adding a callback handler to process events
event_track->addEventCallback(MakeCallback(on_event));


```


### Return value

Current event curve for the track.
---

## AnimationTrack ( )

Constructor. Creates an empty track with default settings.
## AnimationTrack ( const char * name )

Constructor. Creates an empty track with default settings and specified name.
### Arguments

- *const char ** **name** - Animation track name.

## void copy ( const Ptr < AnimationTrack > & track )

Copies all data from the specified source track to the track.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationTrack](../../../../api/library/animations/timeline/class.animationtrack_cpp.md)> &* **track** - Source animation track.

## void clear ( )

Clears the animation track removing all animation objects and modifiers from it. This method also resets track duration to 0.
## bool containsObject ( const Ptr < AnimationObject > & anim_obj )

Returns a value indicating if the animation track contains the specified [animation object](../../../../principles/animations/index.md#animation_object).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_cpp.md)> &* **anim_obj** - Animation object to be checked.

### Return value

true if the the animation playback contains the specified animation object; otherwise, false.
## Ptr < AnimationObject > getObject ( int index ) const

Returns an [animation object](../../../../principles/animations/index.md#animation_object) by its index.
### Arguments

- *int* **index** - Animation object index.

### Return value

Animation object with the specified index.
## int addObject ( const Ptr < AnimationObject > & anim_obj )

Adds the specified [animation object](../../../../principles/animations/index.md#animation_object) to the track.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_cpp.md)> &* **anim_obj** - Animation object to be added.

### Return value

Index of the new animation object added on success; otherwise, -1.
## void removeObject ( const Ptr < AnimationObject > & anim_obj )

Removes the specified [animation object](../../../../principles/animations/index.md#animation_object) along with all modifiers added for it.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_cpp.md)> &* **anim_obj** - Animation object to be removed.

## void addObjectModifier ( const Ptr < AnimationObject > & anim_obj , const Ptr < AnimationModifier > & modifier )

Adds the specified [modifier](../../../../principles/animations/index.md#animation_modifier) to the specified [animation object](../../../../principles/animations/index.md#animation_object) to control changes of a certain parameter over time.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_cpp.md)> &* **anim_obj** - Target animation object to which a modifier should be added.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cpp.md)> &* **modifier** - Animation modifier to be added.

## bool updateObjectModifier ( const Ptr < AnimationObject > & anim_obj , const Ptr < AnimationModifier > & modifier )

Updates the specified [modifier](../../../../principles/animations/index.md#animation_modifier) for the specified [animation object](../../../../principles/animations/index.md#animation_object).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_cpp.md)> &* **anim_obj** - Target animation object to which a modifier should be added.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cpp.md)> &* **modifier** - New source animation modifier to be used.

### Return value

true if the specified modifier was successfully updated for the animation object; otherwise, false.
## void removeObjectModifier ( const Ptr < AnimationObject > & anim_obj , const Ptr < AnimationModifier > & modifier )

Removes the specified [modifier](../../../../principles/animations/index.md#animation_modifier) from the specified [animation object](../../../../principles/animations/index.md#animation_object).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_cpp.md)> &* **anim_obj** - Target animation object from which a modifier should be removed.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cpp.md)> &* **modifier** - Animation modifier to be removed.

## int getObjectModifiers ( const Ptr < AnimationObject > & anim_obj , Vector < Ptr < AnimationModifier >> & OUT_out_modifiers ) const

Collects all modifiers for the specified [animation object](../../../../principles/animations/index.md#animation_object) and puts them to the **out_modifiers** buffer.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_cpp.md)> &* **anim_obj** - Animation object.
- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cpp.md)>> &* **OUT_out_modifiers** - Output buffer for the list of all modifiers for the specified object. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of modifiers for the specified object.
## void addObjectModifier ( const char * anim_obj_name , const Ptr < AnimationModifier > & modifier )

Adds the specified [modifier](../../../../principles/animations/index.md#animation_modifier) to the [animation object](../../../../principles/animations/index.md#animation_object) with the specified name to control changes of a certain parameter over time.
### Arguments

- *const char ** **anim_obj_name** - Name of the target animation object to which a modifier should be added.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cpp.md)> &* **modifier** - Animation modifier to be added.

## void addSingletonModifier ( const Ptr < AnimationModifier > & modifier )

Adds the specified singleton animation [modifier](../../../../principles/animations/index.md#animation_modifier) to control changes of a certain parameter of some Engine's singleton class, such as *[Physics](../../../../api/library/physics/class.physics_cpp.md), [Render](../../../../api/library/rendering/class.render_cpp.md)*, etc.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cpp.md)> &* **modifier** - Singleton animation modifier to be added.

## bool updateSingletonModifier ( const Ptr < AnimationModifier > & modifier )

Updates the specified singleton animation [modifier](../../../../principles/animations/index.md#animation_modifier) used to control changes of a certain parameter of some Engine's singleton class, such as *[Physics](../../../../api/library/physics/class.physics_cpp.md), [Render](../../../../api/library/rendering/class.render_cpp.md)*, etc.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cpp.md)> &* **modifier** - Singleton animation modifier to be updated.

### Return value

true if the specified singleton modifier was successfully updated; otherwise, false.
## void removeSingletonModifier ( const Ptr < AnimationModifier > & modifier )

Removes the specified singleton animation [modifier](../../../../principles/animations/index.md#animation_modifier) from the track.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cpp.md)> &* **modifier** - Singleton animation modifier to be removed.

## int getSingletonModifiers ( Vector < Ptr < AnimationModifier >> & OUT_out_modifiers ) const

Collects all singleton animation modifiers of the track and puts them to the **out_modifiers** buffer.
### Arguments

- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cpp.md)>> &* **OUT_out_modifiers** - Output buffer for the list of all singleton modifiers of the track. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of singleton animation modifiers of the track.
## Ptr < AnimationFrame > getFrame ( float time )

Returns the [animation frame](../../../../principles/animations/index.md#animation_frame) for the specified moment of time. A frame can be thought of as a vertical slice of values of all tracks and modifiers played at the specified moment.
### Arguments

- *float* **time** - Time (in seconds) for which a frame is to be obtained.

### Return value

Animation frame for the specified time.
## Ptr < AnimationFrame > getFrameByNormalizedTime ( float time )

Returns the [animation frame](../../../../principles/animations/index.md#animation_frame) for the specified moment of time (normalized). A frame can be thought of as a vertical slice of values of all tracks and modifiers played at the specified moment.
### Arguments

- *float* **time** - Normalized time value (in the [0.0f, 1.0f] range) for which a frame is to be obtained .

### Return value

Animation frame for the specified time.
