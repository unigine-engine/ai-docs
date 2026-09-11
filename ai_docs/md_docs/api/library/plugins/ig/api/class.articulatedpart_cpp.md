# Unigine::Plugins::IG::ArticulatedPart Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


This class represents the *IG Articulated Part* interface.


> **Notice:** IG plugin must be loaded.


## ArticulatedPart Class

### Members

---

## int getID ( ) const

Returns the ID of the articulated part.
### Return value

Articulated part ID.
## int getNumNodes ( ) const

Returns the total number of nodes representing the articulated part.
### Return value

Number of nodes representing the articulated part.
## Ptr < Node > getNode ( int num ) const

Returns the given node from the array of nodes representing the articulated part.
### Arguments

- *int* **num** - Node number.

### Return value

Node.
## void setEnabled ( bool enable )

Sets the value indicating if the articulated part is enabled.
### Arguments

- *bool* **enable** - true to enable the articulated part; false - to disable it.

## int isEnabled ( ) const

Returns the value indicating if the articulated part is enabled.
### Return value

true if the articulated part is enabled; otherwise, false.
## void setPosition ( const Math::vec3& offset )

Sets the offset of the articulated part in the submodel coordinate system (SCS).
### Arguments

- *const  Math::vec3&* **offset** - Articulated part offset coordinates to set (X - back, Y - left, Z - down).

## Math:: vec3 getPosition ( ) const

Returns the current offset of the articulated part in the submodel coordinate system (SCS).
### Return value

Articulated part offset coordinates (X - back, Y - left, Z - down).
## void setRotationEuler ( const Math::vec3& rotation_euler )

Sets the rotation of the articulated part in the submodel coordinate system (SCS).
### Arguments

- *const  Math::vec3&* **rotation_euler** - Articulated part rotation euler angles to set.

## Math:: vec3 getRotationEuler ( ) const

Returns the rotation of the articulated part in the submodel coordinate system (SCS).
### Return value

Articulated part rotation euler angles.
## void setLinearRate ( const Math::vec3& rate )

Sets the rate of linear motion of the articulated part.
### Arguments

- *const  Math::vec3&* **rate** - Vector of linear motion rates to be set for the corresponding axes (the result is automatically converted for the current [coordinate system](../../../../../api/library/plugins/ig/api/class.nedconverter_cpp.md#TARGET_COORDINATE_SYSTEM)).

## Math:: vec3 getLinearRate ( ) const

Returns the current rate of linear motion of the articulated part.
### Return value

Vector of linear motion rates for the corresponding axes (the result is automatically converted for the current [coordinate system](../../../../../api/library/plugins/ig/api/class.nedconverter_cpp.md#TARGET_COORDINATE_SYSTEM)).
## void setAngularRate ( const Math::vec3& rate )

Sets the rate of angular motion of the articulated part.
### Arguments

- *const  Math::vec3&* **rate** - Vector of angular motion rates to be set for the corresponding axes (the result is automatically converted for the current [coordinate system](../../../../../api/library/plugins/ig/api/class.nedconverter_cpp.md#TARGET_COORDINATE_SYSTEM)).

## Math:: vec3 getAngularRate ( ) const

Returns the current rate of angular motion of the articulated part.
### Return value

Vector of angular motion rates for the corresponding axes (the result is automatically converted for the current [coordinate system](../../../../../api/library/plugins/ig/api/class.nedconverter_cpp.md#TARGET_COORDINATE_SYSTEM)).
