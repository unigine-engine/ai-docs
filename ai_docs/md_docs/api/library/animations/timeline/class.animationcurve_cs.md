# Unigine::AnimationCurve Class (CS)


This is a base class for all [animation curves](../../../../editor2/tools/sequencer/keys/index.md). Animation curves define changes of values of certain types (*bool, float, integer, quat*, etc.) over time.


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
| **AUTO_FLAT** = 0 | A B�zier curve is used for interpolation, with the tangents of each key computed automatically and flattened at local extremes so that the curve does not overshoot. |
| **LINEAR** = 1 | Linear interpolation between two keys is used. |
| **SMOOTH** = 2 | A B�zier curve is used for interpolation, with the left and the right tangent of each key symmetric to the origin. |
| **ALIGNED** = 3 | A B�zier curve is used for interpolation, with the left and the right tangent of each key kept on one line, while their lengths can differ. |
| **BREAK** = 4 | A B�zier curve is used for interpolation, with a possibility to configure the left and the right tangent of each key independently. |
| **CONSTANT** = 5 | The left key value is used within the whole segment between two keys. |
| **NUM_KEY_TYPES** = 6 | The total number of types of interpolation between the keys. |

## EXTRAPOLATION

Way a curve behaves outside the span its keys cover.
| Name | Description |
|---|---|
| **CONSTANT** = 0 | The value of the nearest key is held on and on. |
| **LINEAR** = 1 | The curve keeps going along the slope it had at the nearest key. |
| **CYCLE** = 2 | The curve repeats from its beginning, so the animation loops. |
| **PING_PONG** = 3 | The curve repeats backwards and forwards in turn. |
| **NUM_EXTRAPOLATION_TYPES** = 4 | Number of extrapolation modes. |

### Properties

## 🔒︎ AnimationCurve.TYPE Type

The type of the animation curve.
## 🔒︎ string TypeName

The name of the animation curve type.
### Members

---

## static float WrapSourceTime ( float t , float duration , AnimationCurve.EXTRAPOLATION pre_infinity , AnimationCurve.EXTRAPOLATION post_infinity )

Maps a moment that falls outside the span the keys cover back into it, the way the given extrapolation modes prescribe. It answers where a looping or a mirrored curve is read from when the playhead runs past its content.
### Arguments

- *float* **t** - Moment to be wrapped, in seconds.
- *float* **duration** - Length of the span the keys cover, in seconds.
- *[AnimationCurve.EXTRAPOLATION](../../../../api/library/animations/timeline/class.animationcurve_cs.md#EXTRAPOLATION)* **pre_infinity** - Way the curve behaves before its first key.
- *[AnimationCurve.EXTRAPOLATION](../../../../api/library/animations/timeline/class.animationcurve_cs.md#EXTRAPOLATION)* **post_infinity** - Way the curve behaves after its last key.

### Return value

Moment inside the span the keys cover, in seconds.
