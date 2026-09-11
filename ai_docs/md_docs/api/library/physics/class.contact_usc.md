# Contact Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class stores the result of a physical contact (coordinates of the point, contact duration, penetration depth, contact object, physical shapes participating in the contact, index of the contact surface). This class can be used for implementation of your own custom physics or a custom [player](../../../api/library/players/class.player_usc.md).


## Contact Class

---

## static Contact ( )

Contact class constructor.
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

Sets the time when the contact occurs. In case of [CCD](../../../api/library/physics/class.shape_usc.md#isContinuous_int), it's the time starting from the current physics simulation tick to the moment when the calculated contact is bound to happen. In case of non-continuous collision detection, it is always 0.
### Arguments

- *float* **time** - Contact time, in milliseconds.

## float getTime ( )

Returns the time when the contact occurs. In case of [CCD](../../../api/library/physics/class.shape_usc.md#isContinuous_int), it returns the time starting from the current physics simulation tick to the moment when the calculated contact is bound to happen. In case of non-continuous collision detection, 0 is always returned.
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
## void setPoint ( Vec3 point )

Sets new coordinates of the contact point.
### Arguments

- *Vec3* **point** - Coordinates of the contact point, in world coordinate system.

## Vec3 getPoint ( )

Returns the coordinates of the contact point.
### Return value

Coordinates of the contact point, in world coordinate system.
## void setNormal ( vec3 normal )

Sets new normal coordinates at the contact point.
### Arguments

- *vec3* **normal** - Normal coordinates at the contact point.

## vec3 getNormal ( )

Returns the normal coordinates at the contact point.
### Return value

Normal coordinates at the contact point.
## void setShape0 ( Shape shape0 )

Sets the first shape participating in the contact.
### Arguments

- *[Shape](../../../api/library/physics/class.shape_usc.md)* **shape0** - First shape participating in the contact.

## Shape getShape0 ( )

Returns the first shape participating in the contact.
### Return value

First shape participating in the contact.
## void setShape1 ( Shape shape1 )

Sets the second shape participating in the contact.
### Arguments

- *[Shape](../../../api/library/physics/class.shape_usc.md)* **shape1** - Second shape participating in the contact.

## Shape getShape1 ( )

Returns the second shape participating in the contact.
### Return value

Second shape participating in the contact.
## void setObject ( Object val )

Sets the object participating in the contact.
### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **val** - Contact object.

## Object getObject ( )

Returns the object participating in the contact.
### Return value

Contact object.
