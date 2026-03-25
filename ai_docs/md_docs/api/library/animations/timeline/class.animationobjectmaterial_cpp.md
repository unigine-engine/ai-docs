# Unigine::AnimationObjectMaterial Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationObject


This class enables you to manage proxy [animation objects](../../../../principles/animations/index.md#animation_object) used to animate materials. Binding to a specific material in the framework of a specific [playback](../../../../principles/animations/index.md#animation_playback) is performed via an instance of the *[AnimationBindMaterial](../../../../api/library/animations/timeline/class.animationbindmaterial_cpp.md)* class.


## AnimationObjectMaterial Class

### Members

## void setBind ( const Ptr < AnimationBindMaterial >& bind )

Sets a new binding of this proxy-object to a specific material to be animated.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationBindMaterial](../../../../api/library/animations/timeline/class.animationbindmaterial_cpp.md)>&* **bind** - The binding to a specific material to be animated.

## Ptr < AnimationBindMaterial > getBind () const

Returns the current binding of this proxy-object to a specific material to be animated.
### Return value

Current binding to a specific material to be animated.
---

## AnimationObjectMaterial ( const char * name )

Constructor. Creates a new material animation object with the specified name.
### Arguments

- *const char ** **name** - Material animation object name.

## void setPlaybackOverriddenBind ( const Ptr < AnimationPlayback > & playback , const Ptr < AnimationBindMaterial > & bind )

Sets a new binding of the animation object to a specific material for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_cpp.md)> &* **playback** - Animation playback for which a new binding of the animation object is to be added.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationBindMaterial](../../../../api/library/animations/timeline/class.animationbindmaterial_cpp.md)> &* **bind** - Binding to a specific material to be animated.

## Ptr < AnimationBindMaterial > getPlaybackOverriddenBind ( const Ptr < AnimationPlayback > & playback )

Returns the current binding of the animation object to a specific material for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_cpp.md)> &* **playback** - Animation playback for which a material binding of the animation object is to be retrieved.

### Return value

Overridden binding to a specific animated material.
