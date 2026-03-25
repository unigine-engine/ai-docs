# Unigine::AnimationObjectRuntime Class (CS)

**Inherits from:** AnimationObject


This class enables you to manage proxy [animation objects](../../../../principles/animations/index.md#animation_object) used to animate runtime objects. Binding to a specific runtime object in the framework of a specific [playback](../../../../principles/animations/index.md#animation_playback) is performed via an instance of the *[AnimationBindRuntime](../../../../api/library/animations/timeline/class.animationbindruntime_cs.md)* class.


## AnimationObjectRuntime Class

### Properties

## AnimationBindRuntime Bind

The binding of this proxy-object to a specific runtime object to be animated.
### Members

---

## AnimationObjectRuntime ( string name )

Constructor. Creates a new runtime animation object with the specified name.
### Arguments

- *string* **name** - Property parameter animation object name.

## void SetPlaybackOverriddenBind ( AnimationPlayback playback , AnimationBindRuntime bind )

Sets a new binding of the animation object to a specific runtime object for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_cs.md)* **playback** - Animation playback for which a new binding of the animation object is to be added.
- *[AnimationBindRuntime](../../../../api/library/animations/timeline/class.animationbindruntime_cs.md)* **bind** - Binding to a specific runtime object to be animated.

## AnimationBindRuntime GetPlaybackOverriddenBind ( AnimationPlayback playback )

Returns the current binding of the animation object to a specific runtime object for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_cs.md)* **playback** - Animation playback for which a runtime object binding of the animation object is to be retrieved.

### Return value

Overridden binding to a specific runtime object animated.
