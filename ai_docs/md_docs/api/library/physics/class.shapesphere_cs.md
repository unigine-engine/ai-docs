# Unigine::ShapeSphere Class (CS)

**Inherits from:** Shape


This class is used to create collision shape in the form of a [sphere](../../../principles/physics/shapes/index.md#sphere).


### See Also


UnigineScript samples:


-
-
-
-
-
-


## ShapeSphere Class

### Properties

## vec3 Center

The center of the sphere, in world coordinates.
## float Radius

The radius of the sphere, in units.
### Members

---

## ShapeSphere ( )

Constructor. Creates a new sphere with the zero radius.
## ShapeSphere ( float radius )

Constructor. Creates a new sphere with a given radius.
### Arguments

- *float* **radius** - Radius of the sphere in units.

## ShapeSphere ( Body body , float radius )

Constructor. Creates a new sphere with a given radius and adds it to a given body.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body** - Body, to which the shape will belong.
- *float* **radius** - Radius of the sphere in units.
