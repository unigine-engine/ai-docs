# ObjectDummy Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


A [dummy object](../../../objects/objects/dummy/index.md) can be used when an invisible object with physical properties is required. For example, as a base object to hold visible physical object fixed by using [joints](../../../api/library/physics/class.joint_cpp.md). It can also serve a root node to organize hierarchy same as [NodeDummy](../../../api/library/nodes/class.nodedummy_cpp.md).


## ObjectDummy Class

---

## static ObjectDummyPtr create ( )

Constructor. Creates a new dummy object.
## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cpp.md) type identifier.
