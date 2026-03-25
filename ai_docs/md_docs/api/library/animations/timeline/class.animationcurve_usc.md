# Unigine::AnimationCurve Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This is a base class for all [animation curves](../../../../principles/animations/index.md#animation_curve). Animation curves define changes of values of certain types (*bool, float, integer, quat*, etc.) over time.


## AnimationCurve Class

### Members

## int getType () const

Returns the current type of the animation curve.
### Return value

Current type of the animation curve.
## const char * getTypeName () const

Returns the current name of the animation curve type.
### Return value

Current name of the animation curve type.
