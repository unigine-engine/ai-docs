# Primitives Class (CPP)

**Header:** #include <UniginePrimitives.h>


This class contains methods enabling you to create geometry primitives - [dynamic meshes](../../../api/library/rendering/class.meshdynamic_cpp.md) of the predefined forms, or add surfaces of the predefined forms to already existing dynamic meshes.


### Usage Example


Here is a small example demonstrating how to create a capsule primitive and add a box surface to it:


```cpp
#include <UnigineObjects.h>
#include <UniginePrimitives.h>
// ...

// Creating a capsule-shape primitive with the specified parameters
ObjectMeshDynamicPtr MyPrimitive = Primitives::createCapsule(0.5f, 3, 16, 32);

// Adding a box-shape surface to the created capsule
Primitives::addBoxSurface(MyPrimitive, vec3(2.0f), mat4_identity);

```


## Primitives Class

---

## Ptr < ObjectMeshDynamic > createBox ( const Math:: vec3 & size )

Creates a dynamic mesh in a form of a box.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Box size along the X, Y and Z axes.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* instance.
## Ptr < ObjectMeshDynamic > createCapsule ( float radius , float height , int stacks = 16 , int slices = 32 )

Creates a dynamic mesh in a form of a capsule.
### Arguments

- *float* **radius** - Capsule radius.
- *float* **height** - Capsule height.
- *int* **stacks** - Number of stacks that divide the capsule radially.
- *int* **slices** - Number of slices that divide the capsule horizontally.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* instance.
## Ptr < ObjectMeshDynamic > createCylinder ( float radius , float height , int stacks = 1 , int slices = 32 )

Creates a dynamic mesh in a form of a cylinder.
### Arguments

- *float* **radius** - Cylinder radius.
- *float* **height** - Cylinder height.
- *int* **stacks** - Number of stacks that divide the cylinder radially.
- *int* **slices** - Number of slices that divide the cylinder horizontally.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* instance.
## Ptr < ObjectMeshDynamic > createDodecahedron ( float radius )

Creates a dynamic mesh in a form of a dodecahedron.
### Arguments

- *float* **radius** - Dodecahedron radius.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* instance.
## Ptr < ObjectMeshDynamic > createIcosahedron ( float radius )

Creates a dynamic mesh in a form of an icosahedron.
### Arguments

- *float* **radius** - Icosahedron radius.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* instance.
## Ptr < ObjectMeshDynamic > createPlane ( float width , float height , float step )

Creates a dynamic mesh in a form of a plane. It is divided into equal squares whose size is defined by the given step.
### Arguments

- *float* **width** - Plane width.
- *float* **height** - Plane height.
- *float* **step** - Step of surface subdivision (vertical and horizontal).

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* instance.
## Ptr < ObjectMeshDynamic > createPrism ( float size_0 , float size_1 , float height , int sides = 8 )

Creates a dynamic mesh in a form of a prism.
### Arguments

- *float* **size_0** - Radius of the circle circumscribed about the top prism base.
- *float* **size_1** - Radius of the circle circumscribed about the bottom prism base.
- *float* **height** - Height of the prism.
- *int* **sides** - Number of the prism faces.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* instance.
## Ptr < ObjectMeshDynamic > createSphere ( float radius , int stacks = 16 , int slices = 32 )

Creates a dynamic mesh in a form of a sphere.
### Arguments

- *float* **radius** - Sphere radius.
- *int* **stacks** - Number of stacks that divide the sphere radially.
- *int* **slices** - Number of slices that divide the sphere horizontally.

### Return value

*[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* instance.
## void addBoxSurface ( Ptr < ObjectMeshDynamic > & object , const Math:: vec3 & size , const Math:: mat4 & transform )

Appends a box of the specified size to ObjectMeshDynamic.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)> &* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* instance.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Box size along the X, Y and Z axes.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Box transformation matrix.

## void addCapsuleSurface ( Ptr < ObjectMeshDynamic > & object , float radius , float height , const Math:: mat4 & transform , int stacks = 16 , int slices = 32 )

Appends a capsule of the specified size to ObjectMeshDynamic. The stacks and slices specify the surface's subdivision.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)> &* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* instance.
- *float* **radius** - Capsule radius.
- *float* **height** - Capsule height along the central axis.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Capsule transformation matrix.
- *int* **stacks** - Number of stacks that divide the capsule radially.
- *int* **slices** - Number of slices that divide the capsule horizontally.

## void addCylinderSurface ( Ptr < ObjectMeshDynamic > & object , float radius , float height , const Math:: mat4 & transform , int stacks = 1 , int slices = 32 )

Appends a cylinder of the specified size to ObjectMeshDynamic. The stacks and slices specify the surface's subdivision.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)> &* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* instance.
- *float* **radius** - Cylinder radius.
- *float* **height** - Cylinder height.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Cylinder transformation matrix.
- *int* **stacks** - Number of stacks that divide the cylinder radially.
- *int* **slices** - Number of slices that divide the cylinder horizontally.

## void addDodecahedronSurface ( Ptr < ObjectMeshDynamic > & object , float radius , const Math:: mat4 & transform )

Appends a dodecahedron (a polyhedron with twelve flat faces) of the specified size to ObjectMeshDynamic.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)> &* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* instance.
- *float* **radius** - Dodecahedron radius.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## void addIcosahedronSurface ( Ptr < ObjectMeshDynamic > & object , float radius , const Math:: mat4 & transform )

Appends a icosahedron (a polyhedron with twenty flat faces) of the specified size to ObjectMeshDynamic.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)> &* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* instance.
- *float* **radius** - Icosahedron radius.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## void addPlaneSurface ( Ptr < ObjectMeshDynamic > & object , float width , float height , float step , const Math:: mat4 & transform )

Appends a plane surface to the dynamic mesh. The plane is divided into equal squares, size of which is defined by the given step.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)> &* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* instance.
- *float* **width** - Width of the plane.
- *float* **height** - Height of the plane.
- *float* **step** - Step of surface subdivision (vertical and horizontal).
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Plane transformation matrix.

## void addPrismSurface ( Ptr < ObjectMeshDynamic > & object , float size_0 , float size_1 , float height , const Math:: mat4 & transform , int sides = 8 )

Appends a prism to the dynamic mesh.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)> &* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* instance.
- *float* **size_0** - Radius of the circle circumscribed about the top prism base.
- *float* **size_1** - Radius of the circle circumscribed about the bottom prism base.
- *float* **height** - Dimension of the prism's central axis.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Prism transformation matrix.
- *int* **sides** - Number of the prism faces.

## void addSphereSurface ( Ptr < ObjectMeshDynamic > & object , float radius , const Math:: mat4 & transform , int stacks = 16 , int slices = 32 )

Appends a sphere surface to the dynamic mesh. The stacks and slices specify the surface's subdivision.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)> &* **object** - *[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* instance.
- *float* **radius** - Sphere radius.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.
- *int* **stacks** - Number of stacks that divide the sphere radially.
- *int* **slices** - Number of slices that divide the sphere horizontally.
