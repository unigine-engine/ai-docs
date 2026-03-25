# Unigine::WorldTransformPath Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


This class is used to create a frame-based succession of transformations from a loaded path.  For other nodes to move along with these transformations, they should be assigned as *WorldTransformPath* children.

> **Notice:** The *path* is a spline along which an object can be moved.


### See Also


UnigineScript samples:


-
-


## WorldTransformPath Class

### Members

---

## static WorldTransformPath ( string name , int unique = 0 )

Constructor. Creates a transformer defined by a path in world coordinates.
### Arguments

- *string* **name** - Path to the `*.path` file.
- *int* **unique** - The dynamic flag:

  - **0** - If the path is changed in run-time, paths loaded from the same file will be also changed.
  - **1** - If the path is changed in run-time, paths loaded from the same file won't be changed

## void setLoop ( int loop )

Sets a value indicating if the transformation defined by the path should be looped.
### Arguments

- *int* **loop** - 1 to loop the transformation defined by the path; 0 to play it only once.

## int getLoop ( )

Returns a value indicating if the transformation defined by the path is looped.
### Return value

1 if the transformation is looped; otherwise, 0.
## void setOrientation ( int orientation )

Sets a value indicating if an object should be oriented along the path. When this option is enabled the complete transformation matrix (position, rotation, and scale) is taken into account when calculating intermediate transformation between the frames. When disabled - only the intermediate position between the frames is used, while keeping object's scale and rotation.
### Arguments

- *int* **orientation** - 1 to orient an object along the path; 0 to keep the initial orientation of the object. The default value is 1.

## int getOrientation ( )

Returns a value indicating if an object is oriented along the path. When this option is enabled the complete transformation matrix (position, rotation, and scale) is taken into account when calculating intermediate transformation between the frames. When disabled - only the intermediate position between the frames is used, while keeping object's scale and rotation.
### Return value

1 if an object is oriented along the path; 0 if the object initial orientation is kept. The default value is 1.
## Path getPath ( )

Returns the path, by which the transformation is defined. By using this function, you can edit the current path or change velocity or transformation of the object moving along the path.
### Return value

Instance of the [*Path*](../../../api/library/common/class.path_usc.md) class.
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
## int isPlaying ( )

Returns a value indicating if the transformation defined by the path is played.
### Return value

**1** if the transformation is played; otherwise, **0**.
## void setSpeed ( float speed )

Sets the speed of playback of the transformation defined by the path.
### Arguments

- *float* **speed** - Speed of the transformation playback. Negative value controls reverse playback.

## float getSpeed ( )

Returns the speed of playback of the transformation defined by the path.
### Return value

The playback speed.
## int isStopped ( )

Returns a value indicating if the transformation defined by the path is stopped.
### Return value

**1** if the transformation is stopped; otherwise, **0**.
## void setTime ( float time )

Sets the time, from which the playback of the transformation defined by the path starts. If the object is [oriented](#getOrientation_int) along the path, its transformation will be correspond to the path transformation at the specified time. Otherwise, only position of the object will change.
### Arguments

- *float* **time** - The playback time to be set.

## float getTime ( )

Returns the time from which the playback of the transformation defined by the path starts.
### Return value

The playback time.
## void play ( )

Continues playback of the transformation defined by the path, if it is paused, or starts playback if it is stopped.
## void stop ( )

Stops playback of the transformation defined by the path. This function saves the playback position so that playing of the transformation defined by the path can be resumed from the same point.
## static int type ( )

Returns the type of the node.
### Return value

[World](../../../api/library/engine/class.world_usc.md) type identifier.
## void setUpdateDistanceLimit ( float limit )

Sets the distance from the camera within which the object should be updated.
### Arguments

- *float* **limit** - Distance from the camera within which the object should be updated.

## float getUpdateDistanceLimit ( )

Returns the distance from the camera within which the object should be updated.
### Return value

Distance from the camera within which the object should be updated.
