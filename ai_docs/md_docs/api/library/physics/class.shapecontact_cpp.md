# Unigine::ShapeContact Class (CPP)

**Header:** #include <UniginePhysics.h>


This class stores the result of a physical contact (coordinates of the point, contact duration, penetration depth, contact object, physical shapes participating in the contact, index of the contact surface). This class can be used for implementation of your own custom physics or a custom [player](../../../api/library/players/class.player_cpp.md).


## ShapeContact Class

### Members

## void setObject ( const Ptr < Object >& object )

Sets a new object participating in the contact.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)>&* **object** - The object participating in the contact

## Ptr < Object > getObject () const

Returns the current object participating in the contact.
### Return value

Current object participating in the contact
## void setShape1 ( const Ptr < Shape >& shape1 )

Sets a new second shape participating in the contact.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Shape](../../../api/library/physics/class.shape_cpp.md)>&* **shape1** - The second shape participating in the contact

## Ptr < Shape > getShape1 () const

Returns the current second shape participating in the contact.
### Return value

Current second shape participating in the contact
## void setShape0 ( const Ptr < Shape >& shape0 )

Sets a new first shape participating in the contact.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Shape](../../../api/library/physics/class.shape_cpp.md)>&* **shape0** - The first shape participating in the contact

## Ptr < Shape > getShape0 () const

Returns the current first shape participating in the contact.
### Return value

Current first shape participating in the contact
## void setNormal ( const Math:: vec3 & normal )

Sets a new normal coordinates at the contact point.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **normal** - The normal coordinates at the contact point

## Math:: vec3 getNormal () const

Returns the current normal coordinates at the contact point.
### Return value

Current normal coordinates at the contact point
## void setPoint ( const Math:: Vec3 & point )

Sets a new coordinates of the contact point, in world coordinates.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)&* **point** - The coordinates of the contact point, in world coordinates

## Math:: Vec3 getPoint () const

Returns the current coordinates of the contact point, in world coordinates.
### Return value

Current coordinates of the contact point, in world coordinates
## void setDepth ( float depth )

Sets a new penetration depth of the contact. This distance is measured along the contact [normal](#getNormal_vec3).
### Arguments

- *float* **depth** - The penetration depth of the contact

## float getDepth () const

Returns the current penetration depth of the contact. This distance is measured along the contact [normal](#getNormal_vec3).
### Return value

Current penetration depth of the contact
## void setTime ( float time )

Sets a new time when the contact occurs. In case of [CCD](../../../api/library/physics/class.shape_cpp.md#isContinuous_int), it returns the time starting from the current physics simulation tick to the moment when the calculated contact is bound to happen. In case of non-continuous collision detection, 0 is always returned.
### Arguments

- *float* **time** - The time when the contact occurs

## float getTime () const

Returns the current time when the contact occurs. In case of [CCD](../../../api/library/physics/class.shape_cpp.md#isContinuous_int), it returns the time starting from the current physics simulation tick to the moment when the calculated contact is bound to happen. In case of non-continuous collision detection, 0 is always returned.
### Return value

Current time when the contact occurs
## void setSurface ( int surface )

Sets a new contact surface number.
### Arguments

- *int* **surface** - The contact surface number

## int getSurface () const

Returns the current contact surface number.
### Return value

Current contact surface number
## void setID ( int id )

Sets a new contact id.
### Arguments

- *int* **id** - The contact id

## int getID () const

Returns the current contact id.
### Return value

Current contact id
---

## static ShapeContactPtr create ( )

ShapeContact class constructor.
