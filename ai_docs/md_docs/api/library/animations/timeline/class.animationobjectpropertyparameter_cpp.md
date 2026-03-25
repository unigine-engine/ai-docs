# Unigine::AnimationObjectPropertyParameter Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationObject


This class enables you to manage proxy [animation objects](../../../../principles/animations/index.md#animation_object) used to animate property parameters. Binding to a specific property parameter in the framework of a specific [playback](../../../../principles/animations/index.md#animation_playback) is performed via an instance of the *[AnimationBindPropertyParameter](../../../../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md)* class.


## AnimationObjectPropertyParameter Class

### Members

## void setBind ( const Ptr < AnimationBindPropertyParameter >& bind )

Sets a new binding of this proxy-object to a specific property parameter to be animated.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationBindPropertyParameter](../../../../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md)>&* **bind** - The binding to a specific property parameter to be animated.

## Ptr < AnimationBindPropertyParameter > getBind () const

Returns the current binding of this proxy-object to a specific property parameter to be animated.
### Return value

Current binding to a specific property parameter to be animated.
---

## AnimationObjectPropertyParameter ( const char * name )

Constructor. Creates a new property parameter animation object with the specified name.
### Arguments

- *const char ** **name** - Property parameter animation object name.

## void setPlaybackOverriddenBind ( const Ptr < AnimationPlayback > & playback , const Ptr < AnimationBindPropertyParameter > & bind )

Sets a new binding of the animation object to a specific property parameter for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_cpp.md)> &* **playback** - Animation playback for which a new binding of the animation object is to be added.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationBindPropertyParameter](../../../../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md)> &* **bind** - Binding to a specific property parameter to be animated.

## Ptr < AnimationBindPropertyParameter > getPlaybackOverriddenBind ( const Ptr < AnimationPlayback > & playback )

Returns the current binding of the animation object to a specific property parameter for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_cpp.md)> &* **playback** - Animation playback for which a property parameter binding of the animation object is to be retrieved.

### Return value

Overridden binding to a specific property parameter animated.
