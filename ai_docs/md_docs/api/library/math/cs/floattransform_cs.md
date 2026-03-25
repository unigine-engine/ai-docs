# Unigine.FloatTransform Struct (CS)


The *FloatTransform* struct represents a spatial transformation in TRS (Translation-Rotation-Scale) decomposed form. It stores position, rotation, and scale as separate fields rather than combining them into a single matrix.


Unlike matrix-based transforms, FloatTransform correctly handles composition when non-uniform scale is involved - child rotations are not distorted by a parent's non-uniform scale.


### Decomposed Form vs. Matrix Form


When transformations are composed using matrix multiplication (e.g., [mat4](../../../../api/library/math/cs/mat4_cs.md)), non-uniform scale on a parent transform can introduce unintended shearing into a child's rotation. This happens because the parent's scale is baked into the matrix rows, distorting the child's orientation vectors when the matrices are multiplied.


FloatTransform avoids this by composing each component independently:


- **Scale** - multiplied component-wise: *result.scale = parent.scale * child.scale*
- **Rotation** - composed as quaternions: *result.rotation = parent.rotation * child.rotation*
- **Position** - child position is first scaled and rotated by the parent, then added to the parent position: *result.position = parent.position + parent.rotation * (parent.scale * child.position)*


As a result, child rotations remain correct even when a parent transform has non-uniform scale.


Operations such as composition ([Mul()](../../../../api/library/math/cs/mathcommon_cs.md#Mul_FloatTransform_FloatTransform_FloatTransform)), inversion ([Inverse()](../../../../api/library/math/cs/mathcommon_cs.md#Inverse_FloatTransform_FloatTransform)), and blending ([BlendTransform()](../../../../api/library/math/cs/mathcommon_cs.md#BlendTransform_FloatTransform_FloatTransform_float_FloatTransform)) are available as static methods of the **MathLib** class.


## FloatTransform Class

### Properties

## vec3 position

The Translation component of the transform.
## quat rotation

The Rotation component of the transform, stored as a quaternion.
## vec3 scale

The Scale component of the transform. Defaults to **(1, 1, 1)**.
### Members

---

## FloatTransform ( )

Default constructor. Creates an identity transform: position at the origin, no rotation, and uniform scale of 1.
## FloatTransform ( FloatTransform transform )

Copy constructor.
### Arguments

- *FloatTransform* **transform** - Source transform to copy.

## FloatTransform ( vec3 position , quat rotation , vec3 scale )

Constructor. Initializes the transform with the given translation, rotation, and scale values.
### Arguments

- *vec3* **position** - Translation component.
- *quat* **rotation** - Rotation component.
- *vec3* **scale** - Scale component.

## void SetMat ( mat4 mat )

Sets the transform by decomposing the given [mat4](../../../../api/library/math/cs/mat4_cs.md) into translation, rotation, and scale components.
### Arguments

- *mat4* **mat** - Matrix to decompose.

## mat4 GetMat ( )

Composes and returns a [mat4](../../../../api/library/math/cs/mat4_cs.md) from the transform components.
### Return value

The composed transform matrix.
## mat4 GetIMat ( )

Computes and returns the inverse of this transform as a [mat4](../../../../api/library/math/cs/mat4_cs.md).
### Return value

The inverse transform matrix.
