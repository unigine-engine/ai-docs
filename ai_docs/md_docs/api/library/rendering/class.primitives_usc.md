# Primitives Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class contains methods enabling you to create geometry primitives - [dynamic meshes](../../../api/library/rendering/class.meshdynamic_usc.md) of the predefined forms, or add surfaces of the predefined forms to already existing dynamic meshes.


## Primitives Class

---

## ObjectMeshDynamic createBox ( vec3 size )

Creates a dynamic mesh in a form of a box.
### Arguments

- *vec3* **size** - Box size along the X, Y and Z axes.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md)* instance.
## ObjectMeshDynamic createCapsule ( float radius , float height , int stacks = 16 , int slices = 32 )

Creates a dynamic mesh in a form of a capsule.
### Arguments

- *float* **radius** - Capsule radius.
- *float* **height** - Capsule height.
- *int* **stacks** - Number of stacks that divide the capsule radially.
- *int* **slices** - Number of slices that divide the capsule horizontally.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md)* instance.
## ObjectMeshDynamic createCylinder ( float radius , float height , int stacks = 1 , int slices = 32 )

Creates a dynamic mesh in a form of a cylinder.
### Arguments

- *float* **radius** - Cylinder radius.
- *float* **height** - Cylinder height.
- *int* **stacks** - Number of stacks that divide the cylinder radially.
- *int* **slices** - Number of slices that divide the cylinder horizontally.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md)* instance.
## ObjectMeshDynamic createDodecahedron ( float radius )

Creates a dynamic mesh in a form of a dodecahedron.
### Arguments

- *float* **radius** - Dodecahedron radius.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md)* instance.
## ObjectMeshDynamic createIcosahedron ( float radius )

Creates a dynamic mesh in a form of an icosahedron.
### Arguments

- *float* **radius** - Icosahedron radius.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md)* instance.
## ObjectMeshDynamic createPlane ( float width , float height , float step )

Creates a dynamic mesh in a form of a plane. It is divided into equal squares whose size is defined by the given step.
### Arguments

- *float* **width** - Plane width.
- *float* **height** - Plane height.
- *float* **step** - Step of surface subdivision (vertical and horizontal).

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md)* instance.
## ObjectMeshDynamic createPrism ( float size_0 , float size_1 , float height , int sides = 8 )

Creates a dynamic mesh in a form of a prism.
### Arguments

- *float* **size_0** - Radius of the circle circumscribed about the top prism base.
- *float* **size_1** - Radius of the circle circumscribed about the bottom prism base.
- *float* **height** - Height of the prism.
- *int* **sides** - Number of the prism faces.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md)* instance.
## ObjectMeshDynamic createSphere ( float radius , int stacks = 16 , int slices = 32 )

Creates a dynamic mesh in a form of a sphere.
### Arguments

- *float* **radius** - Sphere radius.
- *int* **stacks** - Number of stacks that divide the sphere radially.
- *int* **slices** - Number of slices that divide the sphere horizontally.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md)* instance.
## void addBoxSurface ( ObjectMeshDynamic & object , vec3 size , mat4 transform )

Appends a box of the specified size to ObjectMeshDynamic.
### Arguments

- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md) &* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md)* instance.
- *vec3* **size** - Box size along the X, Y and Z axes.
- *mat4* **transform** - Box transformation matrix.

## void addCapsuleSurface ( ObjectMeshDynamic & object , float radius , float height , mat4 transform , int stacks = 16 , int slices = 32 )

Appends a capsule of the specified size to ObjectMeshDynamic. The stacks and slices specify the surface's subdivision.
### Arguments

- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md) &* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md)* instance.
- *float* **radius** - Capsule radius.
- *float* **height** - Capsule height along the central axis.
- *mat4* **transform** - Capsule transformation matrix.
- *int* **stacks** - Number of stacks that divide the capsule radially.
- *int* **slices** - Number of slices that divide the capsule horizontally.

## void addCylinderSurface ( ObjectMeshDynamic & object , float radius , float height , mat4 transform , int stacks = 1 , int slices = 32 )

Appends a cylinder of the specified size to ObjectMeshDynamic. The stacks and slices specify the surface's subdivision.
### Arguments

- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md) &* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md)* instance.
- *float* **radius** - Cylinder radius.
- *float* **height** - Cylinder height.
- *mat4* **transform** - Cylinder transformation matrix.
- *int* **stacks** - Number of stacks that divide the cylinder radially.
- *int* **slices** - Number of slices that divide the cylinder horizontally.

## void addDodecahedronSurface ( ObjectMeshDynamic & object , float radius , mat4 transform )

Appends a dodecahedron (a polyhedron with twelve flat faces) of the specified size to ObjectMeshDynamic.
### Arguments

- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md) &* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md)* instance.
- *float* **radius** - Dodecahedron radius.
- *mat4* **transform** - Transformation matrix.

## void addIcosahedronSurface ( ObjectMeshDynamic & object , float radius , mat4 transform )

Appends a icosahedron (a polyhedron with twenty flat faces) of the specified size to ObjectMeshDynamic.
### Arguments

- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md) &* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md)* instance.
- *float* **radius** - Icosahedron radius.
- *mat4* **transform** - Transformation matrix.

## void addPlaneSurface ( ObjectMeshDynamic & object , float width , float height , float step , mat4 transform )

Appends a plane surface to the dynamic mesh. The plane is divided into equal squares, size of which is defined by the given step.
### Arguments

- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md) &* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md)* instance.
- *float* **width** - Width of the plane.
- *float* **height** - Height of the plane.
- *float* **step** - Step of surface subdivision (vertical and horizontal).
- *mat4* **transform** - Plane transformation matrix.

## void addPrismSurface ( ObjectMeshDynamic & object , float size_0 , float size_1 , float height , mat4 transform , int sides = 8 )

Appends a prism to the dynamic mesh.
### Arguments

- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md) &* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md)* instance.
- *float* **size_0** - Radius of the circle circumscribed about the top prism base.
- *float* **size_1** - Radius of the circle circumscribed about the bottom prism base.
- *float* **height** - Dimension of the prism's central axis.
- *mat4* **transform** - Prism transformation matrix.
- *int* **sides** - Number of the prism faces.

## void addSphereSurface ( ObjectMeshDynamic & object , float radius , mat4 transform , int stacks = 16 , int slices = 32 )

Appends a sphere surface to the dynamic mesh. The stacks and slices specify the surface's subdivision.
### Arguments

- *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md) &* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md)* instance.
- *float* **radius** - Sphere radius.
- *mat4* **transform** - Transformation matrix.
- *int* **stacks** - Number of stacks that divide the sphere radially.
- *int* **slices** - Number of slices that divide the sphere horizontally.
