# Unigine::AnimationFrame Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class enables you to manage [animation frames](../../../../principles/animations/index.md#animation_frame). A frame can be thought of as a vertical slice of values of all modifiers of all tracks played at a certain moment.


## AnimationFrame Class

---

## AnimationFrame ( )

Constructor. Creates an empty animation frame.
## void copy ( AnimationFrame frame )

Copies the data from the specified source frame to the frame.
### Arguments

- *[AnimationFrame](../../../../api/library/animations/timeline/class.animationframe_usc.md)* **frame** - Source frame.

## void clear ( )

Clears animation frame data.
## int getModifierInfos ( Vector< AnimationModifierInfo >& OUT_infos )

Collects information on all [modifiers](../../../../principles/animations/index.md#animation_modifier) that are active in this frame and puts it to the specified output buffer.
### Arguments

- *Vector<[AnimationModifierInfo](../../../../api/library/animations/timeline/class.animationmodifierinfo_usc.md)>&* **OUT_infos** - Output buffer for information on all modifiers that are active in this frame. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of modifiers.
## void interpolate ( AnimationFrame frame , float k )

Interpolates values of all modifiers of the frame between the current frame and the specified one with the given interpolation coefficient and updates all frame modifiers with interpolated values: **`val = interpolate(val, frame_val, k)`**.
### Arguments

- *[AnimationFrame](../../../../api/library/animations/timeline/class.animationframe_usc.md)* **frame** - Target animation frame.
- *float* **k** - Interpolation coefficient.

## void interpolate ( AnimationFrame frame , float k , AnimationMask exclude_mask )

Interpolates values of all modifiers of the frame between the current frame and the specified one with the given interpolation coefficient. Values of modifiers that belong to the specified exclusion mask are ignored and kept unchanged. All frame modifiers are updated with interpolated values: **`val = interpolate(val, frame_val, k)`**.
### Arguments

- *[AnimationFrame](../../../../api/library/animations/timeline/class.animationframe_usc.md)* **frame** - Target animation frame.
- *float* **k** - Interpolation coefficient.
- *[AnimationMask](../../../../api/library/animations/timeline/class.animationmask_usc.md)* **exclude_mask** - Animation mask to be excluded from interpolation.
