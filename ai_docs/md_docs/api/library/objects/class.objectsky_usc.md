# ObjectSky Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


This class is used to create [sky](../../../objects/objects/sky/index.md).


### See Also


UnigineScript samples:


-
-


## ObjectSky Class

### Members

## void setSpherical ( int spherical )

Sets a new value indicating whether a sky background cube map should be mapped onto a whole sphere rather then a hemisphere.
### Arguments

- *int* **spherical** - The value indicating whether a sky background cube map should be mapped onto a whole sphere rather then a hemisphere

## int isSpherical () const

Returns the current value indicating whether a sky background cube map should be mapped onto a whole sphere rather then a hemisphere.
### Return value

Current value indicating whether a sky background cube map should be mapped onto a whole sphere rather then a hemisphere
---

## static ObjectSky ( )

Constructor. Creates a new sky object.
## static int type ( )

Returns the type of the node.
### Return value

[ObjectSky](../../../api/library/nodes/class.node_usc.md#OBJECT_SKY) node type identifier.
