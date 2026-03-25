# Unigine::AnimationObjectNode Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** AnimationObject


This class enables you to manage proxy [animation objects](../../../../principles/animations/index.md#animation_object) used to animate nodes. Binding to a specific node in the framework of a specific [playback](../../../../principles/animations/index.md#animation_playback) is performed via an instance of the *[AnimationBindNode](../../../../api/library/animations/timeline/class.animationbindnode_usc.md)* class.


## AnimationObjectNode Class

### Members

## void setBind ( AnimationBindNode bind )

Sets a new binding of this proxy-object to a specific node to be animated.
### Arguments

- *[AnimationBindNode](../../../../api/library/animations/timeline/class.animationbindnode_usc.md)* **bind** - The binding to a specific node to be animated.

## AnimationBindNode getBind () const

Returns the current binding of this proxy-object to a specific node to be animated.
### Return value

Current binding to a specific node to be animated.
---

## AnimationObjectNode ( string name )

Constructor. Creates a new node animation object with the specified name.
### Arguments

- *string* **name** - Node animation object name.

## void setPlaybackOverriddenBind ( AnimationPlayback playback , AnimationBindNode bind )

Sets a new binding of the animation object to a specific node for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_usc.md)* **playback** - Animation playback for which a new binding of the animation object is to be added.
- *[AnimationBindNode](../../../../api/library/animations/timeline/class.animationbindnode_usc.md)* **bind** - Binding to a specific node to be animated.

## AnimationBindNode getPlaybackOverriddenBind ( AnimationPlayback playback )

Returns the current binding of the animation object to a specific node for the specified [playback](../../../../principles/animations/index.md#animation_playback) (binding override).
### Arguments

- *[AnimationPlayback](../../../../api/library/animations/timeline/class.animationplayback_usc.md)* **playback** - Animation playback for which a node binding of the animation object is to be retrieved.

### Return value

Overridden binding to a specific node animated.
