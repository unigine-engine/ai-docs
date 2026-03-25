# Unigine.DoubleTransform Struct (CS)


The *DoubleTransform* struct represents a spatial transformation in TRS (Translation-Rotation-Scale) decomposed form with double-precision translation. It stores position as [dvec3](../../../../api/library/math/cs/dvec3_cs.md), rotation as [quat](../../../../api/library/math/class.quat_cs.md), and scale as [vec3](../../../../api/library/math/cs/vec3_cs.md).


DoubleTransform is intended for world-space transformations in double-precision builds, where large coordinate values require higher precision to avoid floating-point errors.


### Decomposed Form vs. Matrix Form


When transformations are composed using matrix multiplication (e.g., [mat4](../../../../api/library/math/cs/mat4_cs.md)), non-uniform scale on a parent transform can introduce unintended shearing into a child's rotation. This happens because the parent's scale is baked into the matrix rows, distorting the child's orientation vectors when the matrices are multiplied.


DoubleTransform avoids this by composing each component independently:


- **Scale** - multiplied component-wise: *result.scale = parent.scale * child.scale*
- **Rotation** - composed as quaternions: *result.rotation = parent.rotation * child.rotation*
- **Position** - child position is first scaled and rotated by the parent, then added to the parent position: *result.position = parent.position + parent.rotation * (parent.scale * child.position)*


As a result, child rotations remain correct even when a parent transform has non-uniform scale.


Operations such as composition ([Mul()](../../../../api/library/math/cs/mathcommon_cs.md#Mul_DoubleTransform_DoubleTransform_DoubleTransform)), inversion ([Inverse()](../../../../api/library/math/cs/mathcommon_cs.md#Inverse_DoubleTransform_DoubleTransform)), and blending ([BlendTransform()](../../../../api/library/math/cs/mathcommon_cs.md#BlendTransform_DoubleTransform_DoubleTransform_float_DoubleTransform)) are available as static methods of the **MathLib** class.


## DoubleTransform Class

### Properties

## dvec3 position

The Translation component of the transform, stored in double precision.
## quat rotation

The Rotation component of the transform, stored as a quaternion.
## vec3 scale

The Scale component of the transform. Defaults to **(1, 1, 1)**.
### Members

---

## DoubleTransform ( )

Default constructor. Creates an identity transform: position at the origin, no rotation, and uniform scale of 1.
## DoubleTransform ( DoubleTransform transform )

Copy constructor.
### Arguments

- *DoubleTransform* **transform** - Source transform to copy.

## DoubleTransform ( dvec3 position , quat rotation , vec3 scale )

Constructor. Initializes the transform with the given translation, rotation, and scale values.
### Arguments

- *dvec3* **position** - Translation component.
- *quat* **rotation** - Rotation component.
- *vec3* **scale** - Scale component.

## void SetMat ( dmat4 mat )

Sets the transform by decomposing the given [dmat4](../../../../api/library/math/cs/dmat4_cs.md) into translation, rotation, and scale components.
### Arguments

- *dmat4* **mat** - Matrix to decompose.

## dmat4 GetMat ( )

Composes and returns a [dmat4](../../../../api/library/math/cs/dmat4_cs.md) from the transform components.
### Return value

The composed transform matrix.
## dmat4 GetIMat ( )

Computes and returns the inverse of this transform as a [dmat4](../../../../api/library/math/cs/dmat4_cs.md).
### Return value

The inverse transform matrix.
