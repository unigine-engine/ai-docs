# Unigine::ShapeCapsule Class (CS)

**Inherits from:** Shape


This class is used to create collision shape in the form of a [capsule](../../../principles/physics/shapes/index.md#capsule).


### See Also


UnigineScript samples:


-
-
-
-


## ShapeCapsule Class

### Properties

## float Height

The height of the capsule, in units.
## float Radius

The radius of the capsule, in units.
## 🔒︎ vec3 TopCap

The coordinates of the center of the top hemisphere of the capsule.
## 🔒︎ vec3 BottomCap

The coordinates of the center of the bottom hemisphere of the capsule.
### Members

---

## ShapeCapsule ( )

Constructor. Creates a new capsule with the zero radius and the zero height.
## ShapeCapsule ( float radius , float height )

Constructor. Creates a new capsule with given dimensions.
### Arguments

- *float* **radius** - Radius of the capsule in units.
- *float* **height** - Height of the capsule in units.

## ShapeCapsule ( Body body , float radius , float height )

Constructor. Creates a new capsule with given dimensions and adds it to a given body.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body** - Body, to which the capsule will belong.
- *float* **radius** - Radius of the capsule in units.
- *float* **height** - Height of the capsule in units.
