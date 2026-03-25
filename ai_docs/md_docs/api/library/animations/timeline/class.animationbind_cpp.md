# Unigine::AnimationBind Class (CPP)

**Header:** #include <UnigineAnimation.h>


This class is used to manage [bindings](../../../../principles/animations/index.md#animation_binding) of [animation objects](../../../../principles/animations/index.md#animation_object) via code. Animation objects serve as proxies in animation sequences and are bound to specific objects (materials, nodes, property parameters, or runtime objects) at the playback stage.


## AnimationBind Class

### Enums

## TYPE

Binding type.
| Name | Description |
|---|---|
| **ANIMATION_BIND** = 0 | Generic binding. |
| **ANIMATION_BIND_NODE** = 1 | Binding to a node. |
| **ANIMATION_BIND_PROPERTY_PARAMETER** = 2 | Binding to a property parameter. |
| **ANIMATION_BIND_MATERIAL** = 3 | Binding to a material. |
| **ANIMATION_BIND_RUNTIME** = 4 | Binding to a runtime object. |

### Members

## AnimationBind::TYPE getType () const

Returns the current binding type.
### Return value

Current binding type.
## const char * getTypeName () const

Returns the current binding type name.
### Return value

Current binding type name.
