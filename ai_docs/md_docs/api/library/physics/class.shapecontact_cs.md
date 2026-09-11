# Unigine::ShapeContact Class (CS)


This class stores the result of a physical contact (coordinates of the point, contact duration, penetration depth, contact object, physical shapes participating in the contact, index of the contact surface). This class can be used for implementation of your own custom physics or a custom [player](../../../api/library/players/class.player_cs.md).


## ShapeContact Class

### Properties

## Object Object

The object participating in the contact.
## Shape Shape1

The second shape participating in the contact.
## Shape Shape0

The first shape participating in the contact.
## vec3 Normal

The normal coordinates at the contact point.
## vec3 Point

The coordinates of the contact point, in world coordinates.
## float Depth

The penetration depth of the contact. This distance is measured along the contact [normal](#getNormal_vec3).
## float Time

The time when the contact occurs. In case of [CCD](../../../api/library/physics/class.shape_cs.md#isContinuous_int), it returns the time starting from the current physics simulation tick to the moment when the calculated contact is bound to happen. In case of non-continuous collision detection, 0 is always returned.
## int Surface

The contact surface number.
## int ID

The contact id.
### Members

---

## ShapeContact ( )

ShapeContact class constructor.
