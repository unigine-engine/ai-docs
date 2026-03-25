# Unigine::WorldTransformPath Class (CPP)

**Header:** #include <UnigineWorlds.h>

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

## static WorldTransformPathPtr create ( const char * name , int unique = 0 )

Constructor. Creates a transformer defined by a path in world coordinates.
### Arguments

- *const char ** **name** - Path to the `*.path` file.
- *int* **unique** - The dynamic flag:

  - **0** - If the path is changed in run-time, paths loaded from the same file will be also changed.
  - **1** - If the path is changed in run-time, paths loaded from the same file won't be changed

## void setLoop ( int loop )

Sets a value indicating if the transformation defined by the path should be looped.
### Arguments

- *int* **loop** - 1 to loop the transformation defined by the path; 0 to play it only once.

## int getLoop ( ) const

Returns a value indicating if the transformation defined by the path is looped.
### Return value

1 if the transformation is looped; otherwise, 0.
## void setOrientation ( int orientation )

Sets a value indicating if an object should be oriented along the path. When this option is enabled the complete transformation matrix (position, rotation, and scale) is taken into account when calculating intermediate transformation between the frames. When disabled - only the intermediate position between the frames is used, while keeping object's scale and rotation.
### Arguments

- *int* **orientation** - 1 to orient an object along the path; 0 to keep the initial orientation of the object. The default value is 1.

## int getOrientation ( ) const

Returns a value indicating if an object is oriented along the path. When this option is enabled the complete transformation matrix (position, rotation, and scale) is taken into account when calculating intermediate transformation between the frames. When disabled - only the intermediate position between the frames is used, while keeping object's scale and rotation.
### Return value

1 if an object is oriented along the path; 0 if the object initial orientation is kept. The default value is 1.
## Ptr < Path > getPath ( ) const

Returns the path, by which the transformation is defined. By using this function, you can edit the current path or change velocity or transformation of the object moving along the path.
### Return value

Instance of the [*Path*](../../../api/library/common/class.path_cpp.md) class.
## void setPathName ( const char * name , int unique = 0 )

Reloads the internal path transformation.
### Arguments

- *const char ** **name** - The path name to be set.
- *int* **unique** - The dynamic flag:

  - **0** - If the reloaded path is changed, paths loaded from the same file will be also changed.
  - **1** - If the reloaded path is changed, paths loaded from the same file won't be changed.

## const char * getPathName ( ) const

Returns the name of the path, by which the transformation is defined.
### Return value

The path name.
## bool isPlaying ( ) const

Returns a value indicating if the transformation defined by the path is played.
### Return value

true if the transformation is played; otherwise, false.
## void setSpeed ( float speed )

Sets the speed of playback of the transformation defined by the path.
### Arguments

- *float* **speed** - Speed of the transformation playback. Negative value controls reverse playback.

## float getSpeed ( ) const

Returns the speed of playback of the transformation defined by the path.
### Return value

The playback speed.
## bool isStopped ( ) const

Returns a value indicating if the transformation defined by the path is stopped.
### Return value

true if the transformation is stopped; otherwise, false.
## void setTime ( float time )

Sets the time, from which the playback of the transformation defined by the path starts. If the object is [oriented](#getOrientation_int) along the path, its transformation will be correspond to the path transformation at the specified time. Otherwise, only position of the object will change.
### Arguments

- *float* **time** - The playback time to be set.

## float getTime ( ) const

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

[World](../../../api/library/engine/class.world_cpp.md) type identifier.
## void setUpdateDistanceLimit ( float limit )

Sets the distance from the camera within which the object should be updated.
### Arguments

- *float* **limit** - Distance from the camera within which the object should be updated.

## float getUpdateDistanceLimit ( ) const

Returns the distance from the camera within which the object should be updated.
### Return value

Distance from the camera within which the object should be updated.
