# Unigine.Physical Class (CPP)

**Header:** #include <UniginePhysicals.h>

**Inherits from:** Node


This class is used to create physicals that represent an invisible force acting upon physical [bodies](../../../api/library/physics/class.body_cpp.md) with collision [shapes](../../../api/library/physics/class.shape_cpp.md) and matching [physical mask](../../../api/library/physics/class.body_cpp.md#setPhysicalMask_int_void).


## Physical Class

### Members

---

## void setPhysicalMask ( int mask )

Sets the bit mask for physical interactions. The Physical object will interact with the other object if they both have matching masks.
### Arguments

- *int* **mask** - An integer value, each bit of which is used to set a bit mask.

## int getPhysicalMask ( )

Returns the bit mask for physical interactions. The Physical object will interact with the other object if they both have matching masks.
### Return value

An integer value, each bit of which is used to set a bit mask.
