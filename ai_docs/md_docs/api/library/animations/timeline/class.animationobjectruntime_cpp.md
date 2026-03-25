# Unigine::AnimationObjectRuntime Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationObject


This class enables you to manage proxy [animation objects](../../../../principles/animations/index.md#animation_object) used to animate runtime objects. Binding to a specific runtime object in the framework of a specific [playback](../../../../principles/animations/index.md#animation_playback) is performed via an instance of the *[AnimationBindRuntime](../../../../api/library/animations/timeline/class.animationbindruntime_cpp.md)* class.


## AnimationObjectRuntime Class

### Members

## void setBind ( const Ptr < AnimationBindRuntime >& bind )

Sets a new binding of this proxy-object to a specific runtime object to be animated.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationBindRuntime](../../../../api/library/animations/timeline/class.animationbindruntime_cpp.md)>&* **bind** - The binding to a specific runtime object to be animated.

## Ptr < AnimationBindRuntime > getBind () const

Returns the current binding of this proxy-object to a specific runtime object to be animated.
### Return value

Current binding to a specific runtime object to be animated.
---

## AnimationObjectRuntime ( const char * name )

Constructor. Creates a new runtime animation object with the specified name.
### Arguments

- *const char ** **name** - Property parameter animation object name.

## void setPlaybackOverriddenBind ( const Ptr < AnimationPlayback > & playback , const Ptr < AnimationBindRuntime > & bind )

Sets a new binding of the animation object to a specific runtime object for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_cpp.md)> &* **playback** - Animation playback for which a new binding of the animation object is to be added.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationBindRuntime](../../../../api/library/animations/timeline/class.animationbindruntime_cpp.md)> &* **bind** - Binding to a specific runtime object to be animated.

## Ptr < AnimationBindRuntime > getPlaybackOverriddenBind ( const Ptr < AnimationPlayback > & playback )

Returns the current binding of the animation object to a specific runtime object for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_cpp.md)> &* **playback** - Animation playback for which a runtime object binding of the animation object is to be retrieved.

### Return value

Overridden binding to a specific runtime object animated.
