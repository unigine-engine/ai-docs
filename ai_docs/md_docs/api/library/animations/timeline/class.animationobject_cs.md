# Unigine::AnimationObject Class (CS)


This class is used to manage [animation objects](../../../../principles/animations/index.md#animation_object) via code.


## AnimationObject Class

### Enums

## TYPE

Type of the animation object.
| Name | Description |
|---|---|
| **ANIMATION_OBJECT** = 0 | Generic animation object. |
| **ANIMATION_OBJECT_NODE** = 1 | Animation object used to animate a node (see the *[AnimationObjectNode](../../../../api/library/animations/timeline/class.animationobjectnode_cs.md)* class). |
| **ANIMATION_OBJECT_MATERIAL** = 2 | Animation object used to animate a material (see the *[AnimationObjectMaterial](../../../../api/library/animations/timeline/class.animationobjectmaterial_cs.md)* class). |
| **ANIMATION_OBJECT_PROPERTY_PARAMETER** = 3 | Animation object used to animate a parameter of a property (see the *[AnimationObjectPropertyParameter](../../../../api/library/animations/timeline/class.animationobjectpropertyparameter_cs.md)* class). |
| **ANIMATION_OBJECT_RUNTIME** = 4 | Animation object used to animate a runtime object (see the *[AnimationObjectRuntime](../../../../api/library/animations/timeline/class.animationobjectruntime_cs.md)* class). |
| **ANIMATION_OBJECT_TRACK** = 5 | Animation object used to animate an animation track (see the *[AnimationObjectTrack](../../../../api/library/animations/timeline/class.animationobjecttrack_cs.md)* class). |

### Properties

## 🔒︎ AnimationObject.TYPE Type

The type of the animation object.
## 🔒︎ string TypeName

The name of the animation object's type.
## 🔒︎ int ID

The identifier of the animation object.
## string Name

The name of the animation object.
