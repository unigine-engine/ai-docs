# Unigine::ShapeConvex Class (CS)

**Inherits from:** Shape


This class is used to create collision shape in the form of a [convex hull](../../../principles/physics/shapes/index.md#convex).


### See Also


UnigineScript samples:


-
-
-
-
-
-
-


## ShapeConvex Class

### Members

---

## ShapeConvex ( )

Constructor. Creates a new empty convex hull.
## ShapeConvex ( Object object , int surface )

Constructor. Creates a convex hull for a given object surface.
### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object, which surface will be approximated.
- *int* **surface** - Number of the surface to approximate with the convex hull.

## ShapeConvex ( Body body , Object object , int surface )

Constructor. Creates a convex hull for a given object surface and adds it to a given body.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body** - Body, to which the convex hull will belong.
- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object, which surface will be approximated.
- *int* **surface** - Number of the surface to approximate with the convex hull.

## int SetObject ( Object object , int surface , float error = 0.01 )

Sets an object surface, for which the convex hull should be created.
### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object, which surface will be approximated.
- *int* **surface** - Number of the surface to approximate with the convex hull. If **-1** is passed to the function as a number of the surface then the convex hull is created for all the surfaces of the mesh. > **Notice:** For a dynamic mesh, the convex hull is not created for all the surfaces.
- *float* **error** - Permissible error, which is used to create the convex hull. This is an optional parameter.

### Return value

**1** if the convex hull is created successfully; otherwise **0**.
