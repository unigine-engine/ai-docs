# Unigine::AnimationObjectPropertyParameter Class (CS)

**Inherits from:** AnimationObject


This class enables you to manage proxy [animation objects](../../../../principles/animations/index.md#animation_object) used to animate property parameters. Binding to a specific property parameter in the framework of a specific [playback](../../../../principles/animations/index.md#animation_playback) is performed via an instance of the *[AnimationBindPropertyParameter](../../../../api/library/animations/timeline/class.animationbindpropertyparameter_cs.md)* class.


## AnimationObjectPropertyParameter Class

### Properties

## AnimationBindPropertyParameter Bind

The binding of this proxy-object to a specific property parameter to be animated.
### Members

---

## AnimationObjectPropertyParameter ( string name )

Constructor. Creates a new property parameter animation object with the specified name.
### Arguments

- *string* **name** - Property parameter animation object name.

## void SetPlaybackOverriddenBind ( AnimationPlayback playback , AnimationBindPropertyParameter bind )

Sets a new binding of the animation object to a specific property parameter for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_cs.md)* **playback** - Animation playback for which a new binding of the animation object is to be added.
- *[AnimationBindPropertyParameter](../../../../api/library/animations/timeline/class.animationbindpropertyparameter_cs.md)* **bind** - Binding to a specific property parameter to be animated.

## AnimationBindPropertyParameter GetPlaybackOverriddenBind ( AnimationPlayback playback )

Returns the current binding of the animation object to a specific property parameter for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_cs.md)* **playback** - Animation playback for which a property parameter binding of the animation object is to be retrieved.

### Return value

Overridden binding to a specific property parameter animated.
