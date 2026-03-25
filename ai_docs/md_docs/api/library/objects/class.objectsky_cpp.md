# ObjectSky Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


This class is used to create [sky](../../../objects/objects/sky/index.md).


### See Also


UnigineScript samples:


-
-


## ObjectSky Class

### Members

---

## static ObjectSkyPtr create ( )

Constructor. Creates a new sky object.
## static int type ( )

Returns the type of the node.
### Return value

[ObjectSky](../../../api/library/nodes/class.node_cpp.md#OBJECT_SKY) node type identifier.
## void setSpherical ( bool spherical )

Sets a value indicating if a sky background cube map should be mapped onto a whole sphere rather then a hemisphere.
### Arguments

- *bool* **spherical** - **true** for the whole sphere; **false** for a sky hemisphere.

## bool isSpherical ( ) const

Returns a value indicating whether a sky background cube map should be mapped onto a whole sphere rather then a hemisphere.
### Return value

**true** if the sky is a sphere; **false**, if a hemisphere.
