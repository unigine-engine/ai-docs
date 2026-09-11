# Unigine::BodyPath Class (CS)

**Inherits from:** Body


This class represents a path along which an arbitrary rigid body can be moved. For example, it allows for creation of a physically simulated train moving along the railtrack.  BodyRigid and BodyPath should be connected together with JointPath.

> **Notice:** The *path* is a spline along which an object can be moved.


#### See Also


- UnigineScript samples:

  -
  -


## BodyPath Class

### Properties

## 🔒︎ Path Path

The path along which physical objects are moving. by using this function, you can change velocity of the objects moving along the path, their transformation, etc.
## 🔒︎ string PathName

The name of the path along which physical objects are moving.
### Members

---

## BodyPath ( )

Constructor. Creates a path with default properties, along which a rigid body is moved.
## BodyPath ( Object object )

Constructor. Creates a path with default properties for the given object. Along this path a rigid body is moved.
### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object represented with the new path body.

## vec3 GetClosestPosition ( vec3 position )

Finds the point on the path which is the closest to the given reference point.
### Arguments

- *vec3* **position** - Coordinates of the reference point.

### Return value

Coordinates of the reference point, if the path exists; otherwise, the (0 0 0) vector is returned.
## quat GetClosestRotation ( vec3 position )

Finds the point on the path which is the closest to the given reference point and returns rotation set by the path in this point.
### Arguments

- *vec3* **position** - Coordinates of the reference point.

### Return value

Rotation set by the path in the found point, if the path is exists; otherwise, the (0 0 0 1) quaternion is returned.
## void SetPathName ( string name , int unique = 0 )

Reloads the internal path transformation.
### Arguments

- *string* **name** - Path to the path file to be set.
- *int* **unique** - The dynamic flag:

  - **0** - If the reloaded path is changed at run time, paths loaded from the same file will be also changed.
  - **1** - If the reloaded path is changed at run time, paths loaded from the same file won't be changed.
