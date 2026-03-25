# Unigine::AnimationObjectNode Class (CS)

**Inherits from:** AnimationObject


This class enables you to manage proxy [animation objects](../../../../principles/animations/index.md#animation_object) used to animate nodes. Binding to a specific node in the framework of a specific [playback](../../../../principles/animations/index.md#animation_playback) is performed via an instance of the *[AnimationBindNode](../../../../api/library/animations/timeline/class.animationbindnode_cs.md)* class.


## AnimationObjectNode Class

### Properties

## AnimationBindNode Bind

The binding of this proxy-object to a specific node to be animated.
### Members

---

## AnimationObjectNode ( string name )

Constructor. Creates a new node animation object with the specified name.
### Arguments

- *string* **name** - Node animation object name.

## void SetPlaybackOverriddenBind ( AnimationPlayback playback , AnimationBindNode bind )

Sets a new binding of the animation object to a specific node for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_cs.md)* **playback** - Animation playback for which a new binding of the animation object is to be added.
- *[AnimationBindNode](../../../../api/library/animations/timeline/class.animationbindnode_cs.md)* **bind** - Binding to a specific node to be animated.

## AnimationBindNode GetPlaybackOverriddenBind ( AnimationPlayback playback )

Returns the current binding of the animation object to a specific node for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_cs.md)* **playback** - Animation playback for which a node binding of the animation object is to be retrieved.

### Return value

Overridden binding to a specific node animated.
