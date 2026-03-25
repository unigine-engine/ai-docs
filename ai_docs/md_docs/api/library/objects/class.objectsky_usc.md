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

---

## static ObjectSky ( )

Constructor. Creates a new sky object.
## static int type ( )

Returns the type of the node.
### Return value

[ObjectSky](../../../api/library/nodes/class.node_usc.md#OBJECT_SKY) node type identifier.
## void setSpherical ( int spherical )

Sets a value indicating if a sky background cube map should be mapped onto a whole sphere rather then a hemisphere.
### Arguments

- *int* **spherical** - **1** for the whole sphere; **0** for a sky hemisphere.

## int isSpherical ( )

Returns a value indicating whether a sky background cube map should be mapped onto a whole sphere rather then a hemisphere.
### Return value

**1** if the sky is a sphere; **0**, if a hemisphere.
