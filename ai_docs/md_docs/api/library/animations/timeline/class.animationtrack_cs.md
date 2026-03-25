# Unigine::AnimationTrack Class (CS)


This class is used to manage [animation tracks](../../../../principles/animations/index.md#animation_track) via code.


## AnimationTrack Class

### Properties

## 🔒︎ UGUID GUID

The GUID of the animation track.
## string Name

The name of the animation track.
## 🔒︎ int NumObjects

The total number of [animation objects](../../../../principles/animations/index.md#animation_object) controlled by the [track](../../../../principles/animations/index.md#animation_track).
## 🔒︎ float Duration

The total track duration, in seconds.
## 🔒︎ float ManualDuration

The
## 🔒︎ string Path

The path to the track file.
## AnimationCurveInt EventCurve

The event curve for the track. Events enable you to call a function or method directly from the animation at a certtain frame/time that you specify. You can use events, for example, to play a sound effect or perform any other actions at any moment on the timeline. The key values on this curve define which events are to be triggered at the corresponding moments. You define the desired list of events as a enumeration, and then simply add keys with the certain enum values to the curve at certain moments when you want the corresponding event to occur.
```csharp
// enumeration that defines all available events
enum EVENT
{
	PLAY_SOUND = 0, 		// on this event we play a sound
	CONSOLE_MESSAGE,		// on this event we print a message to the console
	//...
};

// handler function used to process all events by their IDs
void on_event(int id)
{
	EVENT event_id = (EVENT)id;
	SoundSource sound = new SoundSource("some.mp3", 1);
	if (event_id == EVENT.PLAY_SOUND)
	{
		sound.Stop();
		sound.Play();
	}

	if (event_id == EVENT.CONSOLE_MESSAGE)
	{
		Console.OnscreenMessageLine(vec4.BLUE, "A message.");
	}

	// ...
}

// somwhere in code

// creating a track for events
AnimationTrack event_track = new AnimationTrack();

// creating a track for events
AnimationCurveInt event_curve = new AnimationCurveInt();
event_curve.AddKey(1.25f, (int)EVENT.PLAY_SOUND);
event_curve.AddKey(2.07f, (int)EVENT.CONSOLE_MESSAGE);
event_curve.AddKey(2.75f, (int)EVENT.PLAY_SOUND);
event_track.EventCurve = event_curve;

AnimationPlayback playback = new AnimationPlayback();
// adding a track to the playback
playback.AddLayer(event_track);

// adding a callback handler to process events
event_track.AddEventCallback(on_event);


```


### Members

---

## AnimationTrack ( )

Constructor. Creates an empty track with default settings.
## AnimationTrack ( string name )

Constructor. Creates an empty track with default settings and specified name.
### Arguments

- *string* **name** - Animation track name.

## void Copy ( AnimationTrack track )

Copies all data from the specified source track to the track.
### Arguments

- *[AnimationTrack](../../../../api/library/animations/timeline/class.animationtrack_cs.md)* **track** - Source animation track.

## void Clear ( )

Clears the animation track removing all animation objects and modifiers from it. This method also resets track duration to 0.
## bool ContainsObject ( AnimationObject anim_obj )

Returns a value indicating if the animation track contains the specified [animation object](../../../../principles/animations/index.md#animation_object).
### Arguments

- *[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_cs.md)* **anim_obj** - Animation object to be checked.

### Return value

true if the the animation playback contains the specified animation object; otherwise, false.
## AnimationObject GetObject ( int index )

Returns an [animation object](../../../../principles/animations/index.md#animation_object) by its index.
### Arguments

- *int* **index** - Animation object index.

### Return value

Animation object with the specified index.
## int AddObject ( AnimationObject anim_obj )

Adds the specified [animation object](../../../../principles/animations/index.md#animation_object) to the track.
### Arguments

- *[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_cs.md)* **anim_obj** - Animation object to be added.

### Return value

Index of the new animation object added on success; otherwise, -1.
## void RemoveObject ( AnimationObject anim_obj )

Removes the specified [animation object](../../../../principles/animations/index.md#animation_object) along with all modifiers added for it.
### Arguments

- *[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_cs.md)* **anim_obj** - Animation object to be removed.

## void AddObjectModifier ( AnimationObject anim_obj , AnimationModifier modifier )

Adds the specified [modifier](../../../../principles/animations/index.md#animation_modifier) to the specified [animation object](../../../../principles/animations/index.md#animation_object) to control changes of a certain parameter over time.
### Arguments

- *[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_cs.md)* **anim_obj** - Target animation object to which a modifier should be added.
- *[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cs.md)* **modifier** - Animation modifier to be added.

## bool UpdateObjectModifier ( AnimationObject anim_obj , AnimationModifier modifier )

Updates the specified [modifier](../../../../principles/animations/index.md#animation_modifier) for the specified [animation object](../../../../principles/animations/index.md#animation_object).
### Arguments

- *[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_cs.md)* **anim_obj** - Target animation object to which a modifier should be added.
- *[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cs.md)* **modifier** - New source animation modifier to be used.

### Return value

true if the specified modifier was successfully updated for the animation object; otherwise, false.
## void RemoveObjectModifier ( AnimationObject anim_obj , AnimationModifier modifier )

Removes the specified [modifier](../../../../principles/animations/index.md#animation_modifier) from the specified [animation object](../../../../principles/animations/index.md#animation_object).
### Arguments

- *[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_cs.md)* **anim_obj** - Target animation object from which a modifier should be removed.
- *[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cs.md)* **modifier** - Animation modifier to be removed.

## int GetObjectModifiers ( AnimationObject anim_obj , AnimationModifier [] OUT_out_modifiers )

Collects all modifiers for the specified [animation object](../../../../principles/animations/index.md#animation_object) and puts them to the **out_modifiers** buffer.
### Arguments

- *[AnimationObject](../../../../api/library/animations/timeline/class.animationobject_cs.md)* **anim_obj** - Animation object.
- *[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cs.md)[]* **OUT_out_modifiers** - Output buffer for the list of all modifiers for the specified object. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of modifiers for the specified object.
## void AddObjectModifier ( string anim_obj_name , AnimationModifier modifier )

Adds the specified [modifier](../../../../principles/animations/index.md#animation_modifier) to the [animation object](../../../../principles/animations/index.md#animation_object) with the specified name to control changes of a certain parameter over time.
### Arguments

- *string* **anim_obj_name** - Name of the target animation object to which a modifier should be added.
- *[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cs.md)* **modifier** - Animation modifier to be added.

## void AddSingletonModifier ( AnimationModifier modifier )

Adds the specified singleton animation [modifier](../../../../principles/animations/index.md#animation_modifier) to control changes of a certain parameter of some Engine's singleton class, such as *[Physics](../../../../api/library/physics/class.physics_cs.md), [Render](../../../../api/library/rendering/class.render_cs.md)*, etc.
### Arguments

- *[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cs.md)* **modifier** - Singleton animation modifier to be added.

## bool UpdateSingletonModifier ( AnimationModifier modifier )

Updates the specified singleton animation [modifier](../../../../principles/animations/index.md#animation_modifier) used to control changes of a certain parameter of some Engine's singleton class, such as *[Physics](../../../../api/library/physics/class.physics_cs.md), [Render](../../../../api/library/rendering/class.render_cs.md)*, etc.
### Arguments

- *[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cs.md)* **modifier** - Singleton animation modifier to be updated.

### Return value

true if the specified singleton modifier was successfully updated; otherwise, false.
## void RemoveSingletonModifier ( AnimationModifier modifier )

Removes the specified singleton animation [modifier](../../../../principles/animations/index.md#animation_modifier) from the track.
### Arguments

- *[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cs.md)* **modifier** - Singleton animation modifier to be removed.

## int GetSingletonModifiers ( AnimationModifier [] OUT_out_modifiers )

Collects all singleton animation modifiers of the track and puts them to the **out_modifiers** buffer.
### Arguments

- *[AnimationModifier](../../../../api/library/animations/timeline/class.animationmodifier_cs.md)[]* **OUT_out_modifiers** - Output buffer for the list of all singleton modifiers of the track. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of singleton animation modifiers of the track.
## AnimationFrame GetFrame ( float time )

Returns the [animation frame](../../../../principles/animations/index.md#animation_frame) for the specified moment of time. A frame can be thought of as a vertical slice of values of all tracks and modifiers played at the specified moment.
### Arguments

- *float* **time** - Time (in seconds) for which a frame is to be obtained.

### Return value

Animation frame for the specified time.
## AnimationFrame GetFrameByNormalizedTime ( float time )

Returns the [animation frame](../../../../principles/animations/index.md#animation_frame) for the specified moment of time (normalized). A frame can be thought of as a vertical slice of values of all tracks and modifiers played at the specified moment.
### Arguments

- *float* **time** - Normalized time value (in the [0.0f, 1.0f] range) for which a frame is to be obtained .

### Return value

Animation frame for the specified time.
