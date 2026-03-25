# Unigine::AnimationObject Class (CPP)

**Header:** #include <UnigineAnimation.h>


This class is used to manage [animation objects](../../../../principles/animations/index.md#animation_object) via code.


## AnimationObject Class

### Enums

## TYPE

Type of the animation object.
| Name | Description |
|---|---|
| **ANIMATION_OBJECT** = 0 | Generic animation object. |
| **ANIMATION_OBJECT_NODE** = 1 | Animation object used to animate a node (see the *[AnimationObjectNode](../../../../api/library/animations/timeline/class.animationobjectnode_cpp.md)* class). |
| **ANIMATION_OBJECT_MATERIAL** = 2 | Animation object used to animate a material (see the *[AnimationObjectMaterial](../../../../api/library/animations/timeline/class.animationobjectmaterial_cpp.md)* class). |
| **ANIMATION_OBJECT_PROPERTY_PARAMETER** = 3 | Animation object used to animate a parameter of a property (see the *[AnimationObjectPropertyParameter](../../../../api/library/animations/timeline/class.animationobjectpropertyparameter_cpp.md)* class). |
| **ANIMATION_OBJECT_RUNTIME** = 4 | Animation object used to animate a runtime object (see the *[AnimationObjectRuntime](../../../../api/library/animations/timeline/class.animationobjectruntime_cpp.md)* class). |
| **ANIMATION_OBJECT_TRACK** = 5 | Animation object used to animate an animation track (see the *[AnimationObjectTrack](../../../../api/library/animations/timeline/class.animationobjecttrack_cpp.md)* class). |

### Members

## AnimationObject::TYPE getType () const

Returns the current type of the animation object.
### Return value

Current animation object type.
## const char * getTypeName () const

Returns the current name of the animation object's type.
### Return value

Current animation object type name.
## getID () const

Returns the current identifier of the animation object.
### Return value

Current animation object identifier.
## void setName ( const char * name )

Sets a new name of the animation object.
### Arguments

- *const char ** **name** - The animation object name.

## const char * getName () const

Returns the current name of the animation object.
### Return value

Current animation object name.
