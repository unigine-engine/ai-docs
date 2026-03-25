# Unigine::ShapeContact Class (CPP)

**Header:** #include <UniginePhysics.h>


This class stores the result of a physical contact (coordinates of the point, contact duration, penetration depth, contact object, physical shapes participating in the contact, index of the contact surface). This class can be used for implementation of your own custom physics or a custom [player](../../../api/library/players/class.player_cpp.md).


## ShapeContact Class

### Members

---

## static ShapeContactPtr create ( )

ShapeContact class constructor.
## void setID ( int id )

Sets a new contact ID.
### Arguments

- *int* **id** - Contact ID.

## int getID ( )

Returns the contact ID.
### Return value

Contact ID.
## void setSurface ( int surface )

Sets a new contact surface number.
### Arguments

- *int* **surface** - Contact surface number.

## int getSurface ( )

Returns the contact surface number.
### Return value

Contact surface number.
## void setTime ( float time )

Sets the time when the contact occurs. In case of CCD (for spheres or capsules), it's the time starting from the current physics simulation tick to the moment when the calculated contact is bound to happen. In case of non-continuous collision detection, it is always 0.
### Arguments

- *float* **time** - Contact time, in milliseconds.

## float getTime ( )

Returns the time when the contact occurs. In case of CCD (for spheres or capsules), it returns the time starting from the current physics simulation tick to the moment when the calculated contact is bound to happen. In case of non-continuous collision detection, 0 is always returned.
### Return value

Contact time, in milliseconds.
## void setDepth ( float depth )

Sets a new penetration depth of the contact. This distance is measured along the contact [normal](#getNormal_vec3).
### Arguments

- *float* **depth** - Contact depth, in units.

## float getDepth ( )

Returns the penetration depth of the contact. This distance is measured along the contact [normal](#getNormal_vec3).
### Return value

Contact depth, in units.
## void setPoint ( const Math:: Vec3 & point )

Sets new coordinates of the contact point.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Coordinates of the contact point, in world coordinate system.

## Math:: Vec3 getPoint ( )

Returns the coordinates of the contact point.
### Return value

Coordinates of the contact point, in world coordinate system.
## void setNormal ( const Math:: vec3 & normal )

Sets new normal coordinates at the contact point.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **normal** - Normal coordinates at the contact point.

## Math:: vec3 getNormal ( )

Returns the normal coordinates at the contact point.
### Return value

Normal coordinates at the contact point.
## void setShape0 ( const Ptr < Shape > & shape0 )

Sets the first shape participating in the contact.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Shape](../../../api/library/physics/class.shape_cpp.md)> &* **shape0** - First shape participating in the contact.

## Ptr < Shape > getShape0 ( )

Returns the first shape participating in the contact.
### Return value

First shape participating in the contact.
## void setShape1 ( const Ptr < Shape > & shape1 )

Sets the second shape participating in the contact.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Shape](../../../api/library/physics/class.shape_cpp.md)> &* **shape1** - Second shape participating in the contact.

## Ptr < Shape > getShape1 ( )

Returns the second shape participating in the contact.
### Return value

Second shape participating in the contact.
## void setObject ( const Ptr < Object > & val )

Sets the object participating in the contact.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)> &* **val** - Contact object.

## Ptr < Object > getObject ( )

Returns the object participating in the contact.
### Return value

Contact object.
