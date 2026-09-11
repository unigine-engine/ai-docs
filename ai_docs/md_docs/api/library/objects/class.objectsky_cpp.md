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

## void setSpherical ( bool spherical )

Sets a new value indicating whether a sky background cube map should be mapped onto a whole sphere rather then a hemisphere.
### Arguments

- *bool* **spherical** - value indicating whether a sky background cube map should be mapped onto a whole sphere rather then a hemisphere

## bool isSpherical () const

Returns the current value indicating whether a sky background cube map should be mapped onto a whole sphere rather then a hemisphere.
### Return value

value indicating whether a sky background cube map should be mapped onto a whole sphere rather then a hemisphere
---

## static ObjectSkyPtr create ( )

Constructor. Creates a new sky object.
## static int type ( )

Returns the type of the node.
### Return value

[ObjectSky](../../../api/library/nodes/class.node_cpp.md#OBJECT_SKY) node type identifier.
