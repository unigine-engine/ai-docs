# Unigine::AnimationFrame Class (CPP)

**Header:** #include <UnigineAnimation.h>


This class enables you to manage [animation frames](../../../../principles/animations/index.md#animation_frame). A frame can be thought of as a vertical slice of values of all modifiers of all tracks played at a certain moment.


## AnimationFrame Class

---

## AnimationFrame ( )

Constructor. Creates an empty animation frame.
## void copy ( const Ptr < AnimationFrame > & frame )

Copies the data from the specified source frame to the frame.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationFrame](../../../../api/library/animations/timeline/class.animationframe_cpp.md)> &* **frame** - Source frame.

## void clear ( )

Clears animation frame data.
## int getModifierInfos ( Vector < Ptr < AnimationModifierInfo >> & OUT_infos )

Collects information on all [modifiers](../../../../principles/animations/index.md#animation_modifier) that are active in this frame and puts it to the specified output buffer.
### Arguments

- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifierInfo](../../../../api/library/animations/timeline/class.animationmodifierinfo_cpp.md)>> &* **OUT_infos** - Output buffer for information on all modifiers that are active in this frame. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of modifiers.
## void interpolate ( const Ptr < AnimationFrame > & frame , float k )

Interpolates values of all modifiers of the frame between the current frame and the specified one with the given interpolation coefficient and updates all frame modifiers with interpolated values: **`val = interpolate(val, frame_val, k)`**.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationFrame](../../../../api/library/animations/timeline/class.animationframe_cpp.md)> &* **frame** - Target animation frame.
- *float* **k** - Interpolation coefficient.

## void interpolate ( const Ptr < AnimationFrame > & frame , float k , const Ptr < AnimationMask > & exclude_mask )

Interpolates values of all modifiers of the frame between the current frame and the specified one with the given interpolation coefficient. Values of modifiers that belong to the specified exclusion mask are ignored and kept unchanged. All frame modifiers are updated with interpolated values: **`val = interpolate(val, frame_val, k)`**.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationFrame](../../../../api/library/animations/timeline/class.animationframe_cpp.md)> &* **frame** - Target animation frame.
- *float* **k** - Interpolation coefficient.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationMask](../../../../api/library/animations/timeline/class.animationmask_cpp.md)> &* **exclude_mask** - Animation mask to be excluded from interpolation.
