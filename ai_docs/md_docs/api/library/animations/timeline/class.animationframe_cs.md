# Unigine::AnimationFrame Class (CS)


This class enables you to manage [animation frames](../../../../principles/animations/index.md#animation_frame). A frame can be thought of as a vertical slice of values of all modifiers of all tracks played at a certain moment.


## AnimationFrame Class

### Members

---

## AnimationFrame ( )

Constructor. Creates an empty animation frame.
## void Copy ( AnimationFrame frame )

Copies the data from the specified source frame to the frame.
### Arguments

- *[AnimationFrame](../../../../api/library/animations/timeline/class.animationframe_cs.md)* **frame** - Source frame.

## void Clear ( )

Clears animation frame data.
## int GetModifierInfos ( AnimationModifierInfo [] OUT_infos )

Collects information on all [modifiers](../../../../principles/animations/index.md#animation_modifier) that are active in this frame and puts it to the specified output buffer.
### Arguments

- *[AnimationModifierInfo](../../../../api/library/animations/timeline/class.animationmodifierinfo_cs.md)[]* **OUT_infos** - Output buffer for information on all modifiers that are active in this frame. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of modifiers.
## void Interpolate ( AnimationFrame frame , float k )

Interpolates values of all modifiers of the frame between the current frame and the specified one with the given interpolation coefficient and updates all frame modifiers with interpolated values: **`val = interpolate(val, frame_val, k)`**.
### Arguments

- *[AnimationFrame](../../../../api/library/animations/timeline/class.animationframe_cs.md)* **frame** - Target animation frame.
- *float* **k** - Interpolation coefficient.

## void Interpolate ( AnimationFrame frame , float k , AnimationMask exclude_mask )

Interpolates values of all modifiers of the frame between the current frame and the specified one with the given interpolation coefficient. Values of modifiers that belong to the specified exclusion mask are ignored and kept unchanged. All frame modifiers are updated with interpolated values: **`val = interpolate(val, frame_val, k)`**.
### Arguments

- *[AnimationFrame](../../../../api/library/animations/timeline/class.animationframe_cs.md)* **frame** - Target animation frame.
- *float* **k** - Interpolation coefficient.
- *[AnimationMask](../../../../api/library/animations/timeline/class.animationmask_cs.md)* **exclude_mask** - Animation mask to be excluded from interpolation.
