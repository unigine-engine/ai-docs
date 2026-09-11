# Unigine::WorldTransformPath Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


This class is used to create a frame-based succession of transformations from a loaded path. For other nodes to move along with these transformations, they should be assigned as *WorldTransformPath* children.


> **Notice:** The *path* is a spline along which an object can be moved.


### See Also


UnigineScript samples:


-
-


## WorldTransformPath Class

### Members

## bool isStopped () const

Returns the current value indicating if the transformation defined by the path is stopped.
### Return value

true if the transformation is stopped; otherwise, false.
## bool isPlaying () const

Returns the current value indicating if the transformation defined by the path is played.
### Return value

true if the transformation is played; otherwise, false.
## void setSpeed ( float speed )

Sets a new speed of the transformation playback. Negative value controls reverse playback.speed of playback of the transformation defined by the path.
### Arguments

- *float* **speed** - The

## float getSpeed () const

Returns the current speed of the transformation playback. Negative value controls reverse playback.speed of playback of the transformation defined by the path.
### Return value

Current
## void setTime ( float time )

Sets a new time from which the playback of the transformation defined by the path starts. If the object is [oriented](#getOrientation_int) along the path, its transformation will be correspond to the path transformation at the specified time. Otherwise, only position of the object will change.
### Arguments

- *float* **time** - The playback start time.

## float getTime () const

Returns the current time from which the playback of the transformation defined by the path starts. If the object is [oriented](#getOrientation_int) along the path, its transformation will be correspond to the path transformation at the specified time. Otherwise, only position of the object will change.
### Return value

Current playback start time.
## void setLoop ( int loop )

Sets a new value indicating if the transformation defined by the path is looped.
### Arguments

- *int* **loop** - The 1 to loop the transformation defined by the path; 0 to play it only once.

## int getLoop () const

Returns the current value indicating if the transformation defined by the path is looped.
### Return value

Current 1 to loop the transformation defined by the path; 0 to play it only once.
## void setOrientation ( int orientation )

Sets a new value indicating if an object is oriented along the path. When this option is enabled the complete transformation matrix (position, rotation, and scale) is taken into account when calculating intermediate transformation between the frames. When disabled - only the intermediate position between the frames is used, while keeping object's scale and rotation.
### Arguments

- *int* **orientation** - The 1 to orient an object along the path; 0 to keep the initial orientation of the object. The default value is 1.

## int getOrientation () const

Returns the current value indicating if an object is oriented along the path. When this option is enabled the complete transformation matrix (position, rotation, and scale) is taken into account when calculating intermediate transformation between the frames. When disabled - only the intermediate position between the frames is used, while keeping object's scale and rotation.
### Return value

Current 1 to orient an object along the path; 0 to keep the initial orientation of the object. The default value is 1.
## Path getPath () const

Returns the current instance of the [*Path*](../../../api/library/common/class.path_usc.md) class.path, by which the transformation is defined. by using this function, you can edit the current path or change velocity or transformation of the object moving along the path.
### Return value

Current
## void setUpdateDistanceLimit ( float limit )

Sets a new distance from the camera within which the object should be updated.
### Arguments

- *float* **limit** - The distance from the camera within which the object should be updated.

## float getUpdateDistanceLimit () const

Returns the current distance from the camera within which the object should be updated.
### Return value

Current distance from the camera within which the object should be updated.
---

## static WorldTransformPath ( string name , int unique = 0 )

Constructor. Creates a transformer defined by a path in world coordinates.
### Arguments

- *string* **name** - Path to the `*.path` file.
- *int* **unique** - The dynamic flag:

  - **0** - If the path is changed in run-time, paths loaded from the same file will be also changed.
  - **1** - If the path is changed in run-time, paths loaded from the same file won't be changed

## void setPathName ( string name , int unique = 0 )

Reloads the internal path transformation.
### Arguments

- *string* **name** - The path name to be set.
- *int* **unique** - The dynamic flag:

  - **0** - If the reloaded path is changed, paths loaded from the same file will be also changed.
  - **1** - If the reloaded path is changed, paths loaded from the same file won't be changed.

## string getPathName ( )

Returns the name of the path, by which the transformation is defined.
### Return value

The path name.
## void play ( )

Continues playback of the transformation defined by the path, if it is paused, or starts playback if it is stopped.
## void stop ( )

Stops playback of the transformation defined by the path. This function saves the playback position so that playing of the transformation defined by the path can be resumed from the same point.
## static int type ( )

Returns the type of the node.
### Return value

[World](../../../api/library/engine/class.world_usc.md) type identifier.
