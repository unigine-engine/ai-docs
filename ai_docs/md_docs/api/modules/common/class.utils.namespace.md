# Utils Namespace


The Utils namespace provides a collection of utility functions and helper classes for common operations in template development. These include command-line argument parsing, smooth value interpolation, curve generation, node tagging, and widget utilities.


## Command Line Arguments


## Exponential Interpolation


## Utils::ExpLerp Class

### Description

A template helper class that wraps a value and its target for convenient exponential interpolation. Stores both the current value and target value, allowing you to set the target and call update() each frame without manually tracking both values. The class is implicitly convertible to its value type. value � current interpolated value target � target value to interpolate towards A template helper class that wraps a value and its target for convenient exponential interpolation. Stores both the current value and target value, allowing you to set the target and call **update()** each frame without manually tracking both values. The class is implicitly convertible to its value type.
- value � current interpolated value
- target � target value to interpolate towards


---

## ExpLerp ( T value )

Constructs an ExpLerp with both value and target set to the same initial value.
### Arguments

- *T* **value** - Initial value (also sets target to this value).

## ExpLerp ( T value , T target )

Constructs an ExpLerp with separate initial value and target.
### Arguments

- *T* **value** - Initial current value.
- *T* **target** - Initial target value.

## T update ( float rate , float dt )

Updates the stored value by interpolating towards the target using **exp_lerp**. Returns the new value.
### Arguments

- *float* **rate** - Interpolation rate.
- *float* **dt** - Delta time in seconds.

### Return value

Updated value after interpolation.
## Curve Generation


### Description

Defines a key point for a 2D curve with optional tangent control. Used with genCurve to create curves with custom tangents for fine control over the curve shape. point � key point position (default: vec2_zero) tangent_left � left tangent for curve control (default: vec2_zero) tangent_right � right tangent for curve control (default: vec2_zero) Defines a key point for a 2D curve with optional tangent control. Used with **genCurve** to create curves with custom tangents for fine control over the curve shape.
- point � key point position (default: vec2_zero)
- tangent_left � left tangent for curve control (default: vec2_zero)
- tangent_right � right tangent for curve control (default: vec2_zero)


## Node Tagging


## Widget Utilities
