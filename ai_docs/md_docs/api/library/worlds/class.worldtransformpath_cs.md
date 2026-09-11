# Unigine::WorldTransformPath Class (CS)

**Inherits from:** Node


This class is used to create a frame-based succession of transformations from a loaded path. For other nodes to move along with these transformations, they should be assigned as *WorldTransformPath* children.


> **Notice:** The *path* is a spline along which an object can be moved.


### See Also


UnigineScript samples:


-
-


## WorldTransformPath Class

### Properties

## 🔒︎ bool IsStopped

The value indicating if the transformation defined by the path is stopped.
## 🔒︎ bool IsPlaying

The value indicating if the transformation defined by the path is played.
## float Speed

The speed of the transformation playback. Negative value controls reverse playback.speed of playback of the transformation defined by the path.
## float Time

The time from which the playback of the transformation defined by the path starts. If the object is [oriented](#getOrientation_int) along the path, its transformation will be correspond to the path transformation at the specified time. Otherwise, only position of the object will change.
## int Loop

The value indicating if the transformation defined by the path is looped.
## int Orientation

The value indicating if an object is oriented along the path. When this option is enabled the complete transformation matrix (position, rotation, and scale) is taken into account when calculating intermediate transformation between the frames. When disabled - only the intermediate position between the frames is used, while keeping object's scale and rotation.
## 🔒︎ Path Path

The instance of the [*Path*](../../../api/library/common/class.path_cs.md) class.path, by which the transformation is defined. by using this function, you can edit the current path or change velocity or transformation of the object moving along the path.
## float UpdateDistanceLimit

The distance from the camera within which the object should be updated.
### Members

---

## WorldTransformPath ( string name , int unique = 0 )

Constructor. Creates a transformer defined by a path in world coordinates.
### Arguments

- *string* **name** - Path to the `*.path` file.
- *int* **unique** - The dynamic flag:

  - **0** - If the path is changed in run-time, paths loaded from the same file will be also changed.
  - **1** - If the path is changed in run-time, paths loaded from the same file won't be changed

## void SetPathName ( string name , int unique = 0 )

Reloads the internal path transformation.
### Arguments

- *string* **name** - The path name to be set.
- *int* **unique** - The dynamic flag:

  - **0** - If the reloaded path is changed, paths loaded from the same file will be also changed.
  - **1** - If the reloaded path is changed, paths loaded from the same file won't be changed.

## string GetPathName ( )

Returns the name of the path, by which the transformation is defined.
### Return value

The path name.
## void Play ( )

Continues playback of the transformation defined by the path, if it is paused, or starts playback if it is stopped.
## void Stop ( )

Stops playback of the transformation defined by the path. This function saves the playback position so that playing of the transformation defined by the path can be resumed from the same point.
## static int type ( )

Returns the type of the node.
### Return value

[World](../../../api/library/engine/class.world_cs.md) type identifier.
