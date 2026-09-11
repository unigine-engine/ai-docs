# Unigine::BodyPath Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Body


This class represents a path along which an arbitrary rigid body can be moved. For example, it allows for creation of a physically simulated train moving along the railtrack.  BodyRigid and BodyPath should be connected together with JointPath.

> **Notice:** The *path* is a spline along which an object can be moved.


#### See Also


- UnigineScript samples:

  -
  -


## BodyPath Class

### Members

## Path getPath () const

Returns the current path along which physical objects are moving. by using this function, you can change velocity of the objects moving along the path, their transformation, etc.
### Return value

Current path along which physical objects move
## const char * getPathName () const

Returns the current name of the path along which physical objects are moving.
### Return value

Current name of the path along which physical objects move
---

## static BodyPath ( )

Constructor. Creates a path with default properties, along which a rigid body is moved.
## static BodyPath ( Object object )

Constructor. Creates a path with default properties for the given object. Along this path a rigid body is moved.
### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Object represented with the new path body.

## Vec3 getClosestPosition ( Vec3 position )

Finds the point on the path which is the closest to the given reference point.
### Arguments

- *Vec3* **position** - Coordinates of the reference point.

### Return value

Coordinates of the reference point, if the path exists; otherwise, the (0 0 0) vector is returned.
## quat getClosestRotation ( Vec3 position )

Finds the point on the path which is the closest to the given reference point and returns rotation set by the path in this point.
### Arguments

- *Vec3* **position** - Coordinates of the reference point.

### Return value

Rotation set by the path in the found point, if the path is exists; otherwise, the (0 0 0 1) quaternion is returned.
## void setPathName ( string name , int unique = 0 )

Reloads the internal path transformation.
### Arguments

- *string* **name** - Path to the path file to be set.
- *int* **unique** - The dynamic flag:

  - **0** - If the reloaded path is changed at run time, paths loaded from the same file will be also changed.
  - **1** - If the reloaded path is changed at run time, paths loaded from the same file won't be changed.
