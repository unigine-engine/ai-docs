# Unigine::AnimationObjectNode Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationObject


This class enables you to manage proxy [animation objects](../../../../principles/animations/index.md#animation_object) used to animate nodes. Binding to a specific node in the framework of a specific [playback](../../../../principles/animations/index.md#animation_playback) is performed via an instance of the *[AnimationBindNode](../../../../api/library/animations/timeline/class.animationbindnode_cpp.md)* class.


## AnimationObjectNode Class

### Members

## void setBind ( const Ptr < AnimationBindNode >& bind )

Sets a new binding of this proxy-object to a specific node to be animated.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationBindNode](../../../../api/library/animations/timeline/class.animationbindnode_cpp.md)>&* **bind** - The binding to a specific node to be animated.

## Ptr < AnimationBindNode > getBind () const

Returns the current binding of this proxy-object to a specific node to be animated.
### Return value

Current binding to a specific node to be animated.
---

## AnimationObjectNode ( const char * name )

Constructor. Creates a new node animation object with the specified name.
### Arguments

- *const char ** **name** - Node animation object name.

## void setPlaybackOverriddenBind ( const Ptr < AnimationPlayback > & playback , const Ptr < AnimationBindNode > & bind )

Sets a new binding of the animation object to a specific node for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_cpp.md)> &* **playback** - Animation playback for which a new binding of the animation object is to be added.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationBindNode](../../../../api/library/animations/timeline/class.animationbindnode_cpp.md)> &* **bind** - Binding to a specific node to be animated.

## Ptr < AnimationBindNode > getPlaybackOverriddenBind ( const Ptr < AnimationPlayback > & playback )

Returns the current binding of the animation object to a specific node for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_cpp.md)> &* **playback** - Animation playback for which a node binding of the animation object is to be retrieved.

### Return value

Overridden binding to a specific node animated.
