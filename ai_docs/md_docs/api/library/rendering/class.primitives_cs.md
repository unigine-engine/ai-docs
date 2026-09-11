# Primitives Class (CS)


This class contains methods enabling you to create geometry primitives - [dynamic meshes](../../../api/library/rendering/class.meshdynamic_cs.md) of the predefined forms, or add surfaces of the predefined forms to already existing dynamic meshes.


### Usage Example


Here is a small example demonstrating how to create a capsule primitive and add a box surface to it:


```csharp
// Creating a capsule-shape primitive with the specified parameters
ObjectMeshDynamic MyPrimitive = Primitives.CreateCapsule(0.5f, 3, 16, 32);

// Adding a box-shape surface to the created capsule
Primitives.AddBoxSurface(MyPrimitive, new vec3(2.0f), mat4.IDENTITY);

```


## Primitives Class

### Members

---

## ObjectMeshDynamic CreateBox ( vec3 size )

Creates a dynamic mesh in a form of a box.
### Arguments

- *vec3* **size** - Box size along the X, Y and Z axes.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* instance.
## ObjectMeshDynamic CreateCapsule ( float radius , float height , int stacks = 16 , int slices = 32 )

Creates a dynamic mesh in a form of a capsule.
### Arguments

- *float* **radius** - Capsule radius.
- *float* **height** - Capsule height.
- *int* **stacks** - Number of stacks that divide the capsule radially.
- *int* **slices** - Number of slices that divide the capsule horizontally.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* instance.
## ObjectMeshDynamic CreateCylinder ( float radius , float height , int stacks = 1 , int slices = 32 )

Creates a dynamic mesh in a form of a cylinder.
### Arguments

- *float* **radius** - Cylinder radius.
- *float* **height** - Cylinder height.
- *int* **stacks** - Number of stacks that divide the cylinder radially.
- *int* **slices** - Number of slices that divide the cylinder horizontally.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* instance.
## ObjectMeshDynamic CreateDodecahedron ( float radius )

Creates a dynamic mesh in a form of a dodecahedron.
### Arguments

- *float* **radius** - Dodecahedron radius.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* instance.
## ObjectMeshDynamic CreateIcosahedron ( float radius )

Creates a dynamic mesh in a form of an icosahedron.
### Arguments

- *float* **radius** - Icosahedron radius.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* instance.
## ObjectMeshDynamic CreatePlane ( float width , float height , float step )

Creates a dynamic mesh in a form of a plane. It is divided into equal squares whose size is defined by the given step.
### Arguments

- *float* **width** - Plane width.
- *float* **height** - Plane height.
- *float* **step** - Step of surface subdivision (vertical and horizontal).

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* instance.
## ObjectMeshDynamic CreatePrism ( float size_0 , float size_1 , float height , int sides = 8 )

Creates a dynamic mesh in a form of a prism.
### Arguments

- *float* **size_0** - Radius of the circle circumscribed about the top prism base.
- *float* **size_1** - Radius of the circle circumscribed about the bottom prism base.
- *float* **height** - Height of the prism.
- *int* **sides** - Number of the prism faces.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* instance.
## ObjectMeshDynamic CreateSphere ( float radius , int stacks = 16 , int slices = 32 )

Creates a dynamic mesh in a form of a sphere.
### Arguments

- *float* **radius** - Sphere radius.
- *int* **stacks** - Number of stacks that divide the sphere radially.
- *int* **slices** - Number of slices that divide the sphere horizontally.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* instance.
## void AddBoxSurface ( ObjectMeshDynamic object , vec3 size , mat4 transform )

Appends a box of the specified size to ObjectMeshDynamic.
### Arguments

- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* instance.
- *vec3* **size** - Box size along the X, Y and Z axes.
- *mat4* **transform** - Box transformation matrix.

## void AddCapsuleSurface ( ObjectMeshDynamic object , float radius , float height , mat4 transform , int stacks = 16 , int slices = 32 )

Appends a capsule of the specified size to ObjectMeshDynamic. The stacks and slices specify the surface's subdivision.
### Arguments

- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* instance.
- *float* **radius** - Capsule radius.
- *float* **height** - Capsule height along the central axis.
- *mat4* **transform** - Capsule transformation matrix.
- *int* **stacks** - Number of stacks that divide the capsule radially.
- *int* **slices** - Number of slices that divide the capsule horizontally.

## void AddCylinderSurface ( ObjectMeshDynamic object , float radius , float height , mat4 transform , int stacks = 1 , int slices = 32 )

Appends a cylinder of the specified size to ObjectMeshDynamic. The stacks and slices specify the surface's subdivision.
### Arguments

- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* instance.
- *float* **radius** - Cylinder radius.
- *float* **height** - Cylinder height.
- *mat4* **transform** - Cylinder transformation matrix.
- *int* **stacks** - Number of stacks that divide the cylinder radially.
- *int* **slices** - Number of slices that divide the cylinder horizontally.

## void AddDodecahedronSurface ( ObjectMeshDynamic object , float radius , mat4 transform )

Appends a dodecahedron (a polyhedron with twelve flat faces) of the specified size to ObjectMeshDynamic.
### Arguments

- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* instance.
- *float* **radius** - Dodecahedron radius.
- *mat4* **transform** - Transformation matrix.

## void AddIcosahedronSurface ( ObjectMeshDynamic object , float radius , mat4 transform )

Appends a icosahedron (a polyhedron with twenty flat faces) of the specified size to ObjectMeshDynamic.
### Arguments

- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* instance.
- *float* **radius** - Icosahedron radius.
- *mat4* **transform** - Transformation matrix.

## void AddPlaneSurface ( ObjectMeshDynamic object , float width , float height , float step , mat4 transform )

Appends a plane surface to the dynamic mesh. The plane is divided into equal squares, size of which is defined by the given step.
### Arguments

- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* instance.
- *float* **width** - Width of the plane.
- *float* **height** - Height of the plane.
- *float* **step** - Step of surface subdivision (vertical and horizontal).
- *mat4* **transform** - Plane transformation matrix.

## void AddPrismSurface ( ObjectMeshDynamic object , float size_0 , float size_1 , float height , mat4 transform , int sides = 8 )

Appends a prism to the dynamic mesh.
### Arguments

- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* instance.
- *float* **size_0** - Radius of the circle circumscribed about the top prism base.
- *float* **size_1** - Radius of the circle circumscribed about the bottom prism base.
- *float* **height** - Dimension of the prism's central axis.
- *mat4* **transform** - Prism transformation matrix.
- *int* **sides** - Number of the prism faces.

## void AddSphereSurface ( ObjectMeshDynamic object , float radius , mat4 transform , int stacks = 16 , int slices = 32 )

Appends a sphere surface to the dynamic mesh. The stacks and slices specify the surface's subdivision.
### Arguments

- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* instance.
- *float* **radius** - Sphere radius.
- *mat4* **transform** - Transformation matrix.
- *int* **stacks** - Number of stacks that divide the sphere radially.
- *int* **slices** - Number of slices that divide the sphere horizontally.
