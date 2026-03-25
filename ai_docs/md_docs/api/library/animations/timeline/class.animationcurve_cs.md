# Unigine::AnimationCurve Class (CS)


This is a base class for all [animation curves](../../../../principles/animations/index.md#animation_curve). Animation curves define changes of values of certain types (*bool, float, integer, quat*, etc.) over time.


## AnimationCurve Class

### Enums

## TYPE

Animation curve type.
| Name | Description |
|---|---|
| **ANIMATION_CURVE** = 0 | The animation curve storing values. |
| **ANIMATION_CURVE_INT** = 1 | The animation curve storing *integer* values (see the *[AnimationCurveInt](../../../../api/library/animations/timeline/class.animationcurveint_cs.md)* class). |
| **ANIMATION_CURVE_FLOAT** = 2 | The animation curve storing *float* values (see the *[AnimationCurveIntFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* class). |
| **ANIMATION_CURVE_DOUBLE** = 3 | The animation curve storing *double* values (see the *[AnimationCurveDouble](../../../../api/library/animations/timeline/class.animationcurvedouble_cs.md)* class). |
| **ANIMATION_CURVE_BOOL** = 4 | The animation curve storing *boolean* values (see the *[AnimationCurveBool](../../../../api/library/animations/timeline/class.animationcurvebool_cs.md)* class). |
| **ANIMATION_CURVE_SCALAR** = 5 | The animation curve storing *scalar* values (see the *[AnimationCurveScalar](../../../../api/library/animations/timeline/class.animationcurvescalar_cs.md)* class). |
| **ANIMATION_CURVE_QUAT** = 6 | The animation curve storing *quaternion* values (see the *[AnimationCurveQuat](../../../../api/library/animations/timeline/class.animationcurvequat_cs.md)* class). |
| **ANIMATION_CURVE_STRING** = 7 | The animation curve storing *string* values (see the *[AnimationCurveString](../../../../api/library/animations/timeline/class.animationcurvestring_cs.md)* class). |
| **ANIMATION_CURVE_UGUID** = 8 | The animation curve storing *UGUID* values (see the *[AnimationCurveUGUID](../../../../api/library/animations/timeline/class.animationcurveuguid_cs.md)* class). |

## KEY_TYPE

Type of interpolation between the neighboring keys.
| Name | Description |
|---|---|
| **CONSTANT** = 0 | The left key value is used within the whole segment between two keys. |
| **LINEAR** = 1 | Linear interpolation between two keys is used. |
| **SMOOTH** = 2 | A Bézier curve is used for interpolation, with the left and the right tangent of each key symmetric to the origin. |
| **BREAK** = 3 | A Bézier curve is used for interpolation, with a possibility to configure the left and the right tangent of each key independently. |
| **NUM_KEY_TYPES** = 4 | The total number of types of interpolation between the keys. |

### Properties

## 🔒︎ AnimationCurve.TYPE Type

The type of the animation curve.
## 🔒︎ string TypeName

The name of the animation curve type.
