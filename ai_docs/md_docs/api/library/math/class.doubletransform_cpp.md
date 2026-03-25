# Unigine::Math::DoubleTransform Struct (CPP)

**Header:** #include <UnigineMathLibTransforms.h>


The *DoubleTransform* struct represents a spatial transformation stored in TRS (Translation-Rotation-Scale) decomposed form with double-precision translation. It keeps translation, rotation, and scale as separate components: a [dvec3](../../../api/library/math/class.dvec3_cpp.md) position, a [quat](../../../api/library/math/class.quat_cpp.md) rotation, and a [vec3](../../../api/library/math/class.vec3_cpp.md) scale.


### Decomposed Form vs. Matrix Form


When transformations are composed using matrix multiplication (e.g., [mat4](../../../api/library/math/class.mat4_cpp.md)), non-uniform scale on a parent transform can introduce unintended shearing into a child's rotation. This happens because the parent's scale is baked into the matrix rows, distorting the child's orientation vectors when the matrices are multiplied.


DoubleTransform avoids this by composing each component independently:


- **Scale** - multiplied component-wise: *result.scale = parent.scale * child.scale*
- **Rotation** - composed as quaternions: *result.rotation = parent.rotation * child.rotation*
- **Position** - child position is first scaled and rotated by the parent, then added to the parent position: *result.position = parent.position + parent.rotation * (parent.scale * child.position)*


As a result, child rotations remain correct even when a parent transform has non-uniform scale.


### Transform and WorldTransform


Two typedefs are provided for use in application code:


- **Transform** - always resolves to [FloatTransform](../../../api/library/math/class.floattransform_cpp.md).
- **WorldTransform** - resolves to [FloatTransform](../../../api/library/math/class.floattransform_cpp.md) in a float build, or to *DoubleTransform* in a double build (when *USE_DOUBLE* is defined).


Using *WorldTransform* in application code is recommended over using *DoubleTransform* directly, as it automatically selects the appropriate precision for the build configuration.


### Available Operations


The following free functions operate on *DoubleTransform* and are defined in the same header:


- [inverse()](../../../api/library/math/math.common_cpp.md#inverse_constDoubleTransformref_DoubleTransform) - returns the inverse transform.
- [mul()](../../../api/library/math/math.common_cpp.md#mul_constDoubleTransformref_constDoubleTransformref_DoubleTransform) - composes two transforms or applies a transform to a point.
- [blendTransform()](../../../api/library/math/math.common_cpp.md#blendTransform_constDoubleTransformref_constDoubleTransformref_float_DoubleTransform) - interpolates between two transforms.


## DoubleTransform Struct

### Members

---

## DoubleTransform ( )

Default constructor. Creates an identity transform: position at the origin, no rotation, and uniform scale of 1.
## DoubleTransform ( const DoubleTransform & transform )

Copy constructor.
### Arguments

- *const DoubleTransform &* **transform** - Source transform to copy.

## DoubleTransform ( const dvec3 & position , const quat & rotation , const vec3 & scale )

Constructor. Initializes the transform with the given translation, rotation, and scale values.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **position** - Translation component.
- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **rotation** - Rotation component.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **scale** - Scale component.

## void setMat ( const dmat4 & mat )

Sets the transform by decomposing the given [dmat4](../../../api/library/math/class.dmat4_cpp.md) into translation, rotation, and scale components.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **mat** - Matrix to decompose.

## dmat4 & getMat ( dmat4 & result )

Composes a [dmat4](../../../api/library/math/class.dmat4_cpp.md) from the transform components and stores it in the provided matrix.
### Arguments

- *[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **result** - Output matrix to write into.

### Return value

The composed transform matrix.
## dmat4 getMat ( )

Composes and returns a [dmat4](../../../api/library/math/class.dmat4_cpp.md) from the transform components.
### Return value

The composed transform matrix.
## dmat4 & getIMat ( dmat4 & result )

Computes the inverse of this transform as a [dmat4](../../../api/library/math/class.dmat4_cpp.md) and stores it in the provided matrix.
### Arguments

- *[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **result** - Output matrix to write into.

### Return value

The inverse transform matrix.
## dmat4 getIMat ( )

Computes and returns the inverse of this transform as a [dmat4](../../../api/library/math/class.dmat4_cpp.md).
### Return value

The inverse transform matrix.
