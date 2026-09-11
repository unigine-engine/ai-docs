# ObjectDummy Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


A [dummy object](../../../objects/objects/dummy/index.md) can be used when an invisible object with physical properties is required. For example, as a base object to hold visible physical object fixed by using [joints](../../../api/library/physics/class.joint_usc.md). It can also serve a root node to organize hierarchy same as [NodeDummy](../../../api/library/nodes/class.nodedummy_usc.md).


## ObjectDummy Class

---

## static ObjectDummy ( )

Constructor. Creates a new dummy object.
## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_usc.md) type identifier.
