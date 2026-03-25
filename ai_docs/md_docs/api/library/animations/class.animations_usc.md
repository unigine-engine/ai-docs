# Unigine::Animations Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This class is the central manager for the animation system. It provides functionality for two animation subsystems:


- **Timeline Animation** - managing [animation tracks](../../../principles/animations/index.md#animation_track) (`.utrack`) and [animation playbacks](../../../principles/animations/index.md#animation_playback) (`.uplay`), querying animatable classes and their parameters, and converting legacy animation formats.
- **Animation Scripts** - working with [animation scripts](../../../api/library/animations/skeletal/class.animscript_usc.md) (compiled animation graphs that can be interacted with via code), querying graph types, and monitoring the build process.


## Animations Class

### Members

## getNumObjects () const

Returns the current total number of animated objects.
### Return value

Current number of [animated objects](../../../principles/animations/index.md#animation_object).
## getNumTracks () const

Returns the current total number of [animation tracks](../../../principles/animations/index.md#animation_track).
### Return value

Current number of animation tracks.
## getNumPlaybacks () const

Returns the current total number of [animation playbacks](../../../principles/animations/index.md#animation_playback).
### Return value

Current number of animation playbacks.
## static getEventTrackRemoved () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event reference.
## static getEventTrackAdded () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event reference.
## static getEventObjectRemoved () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event reference.
## static getEventObjectAdded () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event reference.
## Event<string, string, string> getEventCustomLibBuild () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event reference.
## int getNumAnimScriptTypes () const

Returns the current total number of registered [animation script](../../../api/library/animations/skeletal/class.animscript_usc.md) types.
### Return value

Current number of registered animation script types.
## bool isAnimScriptsSuccessBuild () const

Returns the current Returns a value indicating if the last [animation script](../../../api/library/animations/skeletal/class.animscript_usc.md) build completed successfully.
### Return value

**true** if the last animation script build completed successfully; otherwise **false**.
## bool isAnimScriptsRebuilding () const

Returns the current Returns a value indicating if [animation scripts](../../../api/library/animations/skeletal/class.animscript_usc.md) are currently being rebuilt.
### Return value

**true** if animation scripts are currently being rebuilt; otherwise **false**.
## bool isAnimScriptsLoaded () const

Returns the current Returns a value indicating if [animation scripts](../../../api/library/animations/skeletal/class.animscript_usc.md) are loaded.
### Return value

**true** if animation scripts are loaded; otherwise **false**.
---

## AnimationObject getObjectByIndex ( int index )

Returns an [animation object](../../../principles/animations/index.md#animation_object) by its index in the common list of animation objects.
### Arguments

- *int* **index** - Animation object index.

### Return value

Animation object with the specified index
## AnimationObject getObjectByID ( int id )

Returns an [animation object](../../../principles/animations/index.md#animation_object) by its ID.
### Arguments

- *int* **id** - Animation object ID.

### Return value

Animation object with the specified ID.
## int containsObject ( int id )

Returns a value indicating if an [animation object](../../../principles/animations/index.md#animation_object) with the specified ID exists.
### Arguments

- *int* **id** - Animation object ID.

### Return value

**1** if the animation object with the specified ID exists; otherwise, **0**.
## int getObjectIndex ( const AnimationObject obj )

Returns an index of the specified [animation object](../../../principles/animations/index.md#animation_object) in the common list.
### Arguments

- *const [AnimationObject](../../../api/library/animations/timeline/class.animationobject_usc.md)* **obj** - Animation object for which an index is to be found.

### Return value

Animation object index in the common list of animation objects if it is found; otherwise, -1.
## void loadTracks ( )

Loads all [animation tracks](../../../principles/animations/index.md#animation_track).
## void unloadTracks ( )

Unloads all [animation tracks](../../../principles/animations/index.md#animation_track).
## void reloadTracks ( )

Reloads all [animation tracks](../../../principles/animations/index.md#animation_track).
## int loadTrack ( string path )

Loads an [animation track](../../../principles/animations/index.md#animation_track) from the specified file path.
### Arguments

- *string* **path** - Path to the source track file (`.utrack`).

### Return value

Result of loading operation.
## int reloadTrack ( string path )

Reloads an [animation track](../../../principles/animations/index.md#animation_track) from the specified file path.
### Arguments

- *string* **path** - Path to the source track file (`.utrack`).

### Return value

Result of reloading operation.
## int saveTrack ( AnimationTrack track , string path )

Saves the specified [animation track](../../../principles/animations/index.md#animation_track) to the specified file path.
### Arguments

- *[AnimationTrack](../../../api/library/animations/timeline/class.animationtrack_usc.md)* **track** - Animation track to be saved.
- *string* **path** - Path to which the specified animation track is to be saved.

### Return value

Result of saving operation.
## int saveTrackPrecomputed ( AnimationTrack track , int num_frames , int is_looped_frames , string path )

Saves the precomputed version of the specified [animation track](../../../principles/animations/index.md#animation_track) to the specified file path.
### Arguments

- *[AnimationTrack](../../../api/library/animations/timeline/class.animationtrack_usc.md)* **track** - Animation track to be saved.
- *int* **num_frames** - Number of frames to be saved.
- *int* **is_looped_frames** - Set **1** if the animation track should be looped; otherwise, **0**.
- *string* **path** - Path to which the specified animation track is to be saved.

### Return value

Result of saving operation.
## AnimationTrack getTrackByIndex ( int index )

Returns an [animation track](../../../principles/animations/index.md#animation_track) by its index in the common list of tracks.
### Arguments

- *int* **index** - Animation track index in the common list of tracks.

### Return value

Animation track with the specified index.
## AnimationTrack getTrackByGUID ( UGUID guid )

Returns an [animation track](../../../principles/animations/index.md#animation_track) by its GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - GUID of the animation track.

### Return value

Animation track with the specified GUID.
## AnimationTrack getTrackByFileGUID ( UGUID guid )

Returns an [animation track](../../../principles/animations/index.md#animation_track) by the GUID of the animation track file (`.utrack`).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - GUID of the animation track file (`.utrack`).

### Return value

Animation track with the specified file GUID.
## AnimationTrack getTrackByPath ( string path )

Returns an [animation track](../../../principles/animations/index.md#animation_track) by the path to the animation track file (`.utrack`).
### Arguments

- *string* **path** - Path to the animation track file (`.utrack`).

### Return value

Animation track with the specified file GUID.
## int containsTrack ( UGUID guid )

Returns a value indicating if an [animation track](../../../principles/animations/index.md#animation_track) with the specified GUID exists.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - GUID of the animation track.

### Return value

**1** if the animation track with the specified GUID exists; otherwise, **0**.
## int getTrackIndex ( AnimationTrack track )

Returns an index of the specified [animation track](../../../principles/animations/index.md#animation_track) in the common list.
### Arguments

- *[AnimationTrack](../../../api/library/animations/timeline/class.animationtrack_usc.md)* **track** - Animation track for which an index is to be found.

### Return value

Animation track index in the common list of animation tracks if it is found; otherwise, -1.
## void loadPlaybacks ( )

Loads all [animation playbacks](../../../principles/animations/index.md#animation_playback).
## int loadPlayback ( string path )

Loads an [animation playback](../../../principles/animations/index.md#animation_playback) from the specified file path.
### Arguments

- *string* **path** - Path to the source animation playback file (`.uplay`).

### Return value

Result of loading operation.
## int savePlayback ( AnimationPlayback playback , string path )

Saves the specified [animation playback](../../../principles/animations/index.md#animation_playback) to the specified file path.
### Arguments

- *[AnimationPlayback](../../../api/library/animations/timeline/class.animationplayback_usc.md)* **playback** - Animation playback to be saved.
- *string* **path** - Path to which the specified animation playback is to be saved.

### Return value

Result of saving operation.
## AnimationPlayback getPlaybackByIndex ( int index )

Returns an [animation playback](../../../principles/animations/index.md#animation_playback) by its index in the common list of tracks.
### Arguments

- *int* **index** - Animation playback index in the common list of playbacks.

### Return value

Animation playback with the specified index.
## AnimationPlayback getPlaybackByGUID ( UGUID guid )

Returns an [animation playback](../../../principles/animations/index.md#animation_playback) by its GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - GUID of the animation playback.

### Return value

Animation playback with the specified GUID.
## AnimationPlayback getPlaybackByFileGUID ( UGUID guid )

Returns an [animation playback](../../../principles/animations/index.md#animation_playback) by the GUID of the animation track file (`.uplay`).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - GUID of the animation playback file (`.uplay`).

### Return value

Animation track with the specified file GUID.
## AnimationPlayback getPlaybackByPath ( string path )

Returns an [animation playback](../../../principles/animations/index.md#animation_playback) by the path to the animation track file (`.uplay`).
### Arguments

- *string* **path** - Path to the animation playback file (`.uplay`).

### Return value

Animation playback with the specified path.
## int containsPlayback ( UGUID guid )

Returns a value indicating if an [animation playback](../../../principles/animations/index.md#animation_playback) with the specified GUID exists.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - GUID of the animation playback.

### Return value

**1** if the animation playback with the specified GUID exists; otherwise, **0**.
## int getPlaybackIndex ( AnimationPlayback playback )

Returns an index of the specified [animation playback](../../../principles/animations/index.md#animation_playback) in the common list.
### Arguments

- *[AnimationPlayback](../../../api/library/animations/timeline/class.animationplayback_usc.md)* **playback** - Animation playback for which an index is to be found.

### Return value

Animation track index in the common list of animation tracks if it is found; otherwise, -1.
## int getClasses ( Vector<String>& OUT_out_classes )

Obtains the list of names of all available classes that can be animated and puts it to the specified output buffer.
### Arguments

- *Vector<String>&* **OUT_out_classes** - Output buffer for the list of the Engine's classes that can be animated. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of the Engine's classes that can be animated.
## int getSingletonClasses ( Vector<String>& OUT_out_classes )

Obtains the list of names of all Engine's singleton-classes and puts it to the specified output buffer.
### Arguments

- *Vector<String>&* **OUT_out_classes** - Output buffer for the list of the Engine's singleton-classes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of the Engine's singleton-classes.
## string getParentClass ( string class_name )

Returns the name of the parent class for the specified class.
### Arguments

- *string* **class_name** - Name of the class for which the parent class is to be found.

### Return value

Name of the parent class.
## int getDerivedClasses ( string class_name , Vector<String>& OUT_out_classes )

Obtains the list of all classes derived from the specified one and puts it to the specified output buffer.
### Arguments

- *string* **class_name** - Name of the class for which derived classes are to be found.
- *Vector<String>&* **OUT_out_classes** - Output buffer for the list of classes derived from the specified class. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of derived classes.
## int getClassParameters ( string class_name , Vector<int>& OUT_out_parameters )

Obtains the list of all [animation parameter](../../../principles/animations/index.md#animation_parameters) for the specified class and puts it to the specified output buffer.
### Arguments

- *string* **class_name** - Name of the class for which the list of animation parameters is to be found.
- *Vector<int>&* **OUT_out_parameters** - Output buffer for the list of parameters of the specified class. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of animation parameters for the specified class.
## string getParameterName ( int param )

Returns the name of the specified the specified [animation parameter](../../../principles/animations/index.md#animation_parameters).
### Arguments

- *int* **param** - Animation parameter.

### Return value

Animation parameter name.
## int getParameterModifierType ( int param )

Returns the type of modifier used for the specified [animation parameter](../../../principles/animations/index.md#animation_parameters).
### Arguments

- *int* **param** - Animation parameter.

### Return value

Modifier type for the specified parameter.
## int getParameterByName ( string param_name )

Returns an [animation parameter](../../../principles/animations/index.md#animation_parameters) by its name.
### Arguments

- *string* **param_name** - Animation parameter name.

### Return value

Animation parameter with the specified name.
## void convertToUanims ( string folder_path , Vector<String> playbacks )

Converts all track-files in the old *Tracker* format ( `.track`) from the specfied folder to the new animation formats (`.utrack` / `.uplay`).
### Arguments

- *string* **folder_path** - Path to the folder containing track-files in the old *Tracker* format ( `.track`) to be converted to the new track format (`.utrack`).
- *Vector<String>* **playbacks** - List of *Tracker* animation tracks in old format ( `.track`) to be converted to the new playback format(`.uplay`).

## void convertToUanims ( Vector<String> tracks , Vector<String> playbacks )

Converts the specified lists of tracks in the old *Tracker* format ( `.track`) to the new animation formats (`.utrack` / `.uplay`).
### Arguments

- *Vector<String>* **tracks** - List of *Tracker* animation tracks in old format ( `.track`) to be converted to the new track format (`.utrack`).
- *Vector<String>* **playbacks** - List of *Tracker* animation tracks in old format ( `.track`) to be converted to the new playback format(`.uplay`).

## void checkUtrackTypes ( )

Checks all old-style animation parameter types (used in the *Tracker* tool) versus their equivalents in the new Animation System and outputs them to the console. In case of unknown parameter types the corresponding message is displayed.
## int animToBonesModifier ( string anim_path , AnimationModifierBones out_modifier , float duration )

Converts the specified mesh animation file (`.anim`) to a [modifier](../../../principles/animations/index.md#animation_modifier) for [ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_usc.md) bones ( *AnimationModifierBones*) and puts it to the specified *AnimationModifierBones* instance.
### Arguments

- *string* **anim_path** - Path to the mesh animation file (`.anim`) to be converted.
- *[AnimationModifierBones](../../../api/library/animations/timeline/class.animationmodifierbones_usc.md)* **out_modifier** - Resulting animation modifier.
- *float* **duration** - Target animation duration, in seconds.

### Return value

**1** if the specified mesh animation file was successfully converted; otherwise, **0**.
## void rebuildAnimScripts ( )

Triggers a rebuild of all [animation scripts](../../../api/library/animations/skeletal/class.animscript_usc.md). This recompiles the animation graph source files into a runtime library. Use *[()](../../...md#)* to check if the rebuild process is still in progress, and *[()](../../...md#)* to check if it completed successfully.
## string getAnimScriptTypeName ( int type_index )

Returns the name of the [animation script](../../../api/library/animations/skeletal/class.animscript_usc.md) type by its index.
### Arguments

- *int* **type_index** - Index of the animation script type in the range from 0 to the *[()](../../...md#)* of types.

### Return value

Name of the animation script type.
## static void waitAnimScriptsRebuilding ( )

Blocks execution until the current animation scripts rebuild is complete. If a rebuild is in progress, this method waits for the background build task to finish and then loads the updated library. If no rebuild is in progress, returns immediately.
