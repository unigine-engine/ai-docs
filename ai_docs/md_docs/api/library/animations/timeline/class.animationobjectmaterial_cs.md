# Unigine::AnimationObjectMaterial Class (CS)

**Inherits from:** AnimationObject


This class enables you to manage proxy [animation objects](../../../../principles/animations/index.md#animation_object) used to animate materials. Binding to a specific material in the framework of a specific [playback](../../../../principles/animations/index.md#animation_playback) is performed via an instance of the *[AnimationBindMaterial](../../../../api/library/animations/timeline/class.animationbindmaterial_cs.md)* class.


## AnimationObjectMaterial Class

### Properties

## AnimationBindMaterial Bind

The binding of this proxy-object to a specific material to be animated.
### Members

---

## AnimationObjectMaterial ( string name )

Constructor. Creates a new material animation object with the specified name.
### Arguments

- *string* **name** - Material animation object name.

## void SetPlaybackOverriddenBind ( AnimationPlayback playback , AnimationBindMaterial bind )

Sets a new binding of the animation object to a specific material for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_cs.md)* **playback** - Animation playback for which a new binding of the animation object is to be added.
- *[AnimationBindMaterial](../../../../api/library/animations/timeline/class.animationbindmaterial_cs.md)* **bind** - Binding to a specific material to be animated.

## AnimationBindMaterial GetPlaybackOverriddenBind ( AnimationPlayback playback )

Returns the current binding of the animation object to a specific material for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_cs.md)* **playback** - Animation playback for which a material binding of the animation object is to be retrieved.

### Return value

Overridden binding to a specific animated material.
