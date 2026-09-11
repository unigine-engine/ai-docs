# Unigine::AnimationBindMaterial Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationBind


This binding points a channel at a material, so that a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cpp.md) animates a material parameter such as a color, an albedo scale or a texture shift.


The material is reached in one of two ways: straight from a material asset, which writes into the asset and shows on everything that uses it, or through a surface of an object, which gives that surface a child material and leaves the rest of the scene alone.


## AnimationBindMaterial Class

### Enums

## ACCESS

Access mode. It decides the way the animated material is obtained.
| Name | Description |
|---|---|
| **ACCESS_UNKNOWN** = -1 | The way to obtain the material is not set. |
| **ACCESS_FROM_ASSET** = 0 | The material is taken from a material asset, so the animation writes into the asset itself and reaches everything that uses it. |
| **ACCESS_FROM_SURFACE** = 1 | The material is taken from a surface of an object, which gives a child material of its own to that surface, so the animation touches nothing else. |

### Members

## void setAccess ( AnimationBindMaterial::ACCESS access )

Sets a new access mode of the binding. It decides the way the animated material is obtained.
### Arguments

- *[AnimationBindMaterial::ACCESS](../../../../api/library/animations/timeline/class.animationbindmaterial_cpp.md#ACCESS)* **access** - The access mode of the binding

## AnimationBindMaterial::ACCESS getAccess () const

Returns the current access mode of the binding. It decides the way the animated material is obtained.
### Return value

Current access mode of the binding
## void setSurfacePattern ( const char * pattern )

Sets a new pattern the surface names are matched against. It picks the surfaces the binding works on inside every object the target resolves to.
### Arguments

- *const char ** **pattern** - The pattern the surface names are matched against

## const char * getSurfacePattern () const

Returns the current pattern the surface names are matched against. It picks the surfaces the binding works on inside every object the target resolves to.
### Return value

Current pattern the surface names are matched against
---

## AnimationBindMaterial ( )

Constructor. Creates an empty material binding.
## void setObjects ( Vector < Ptr < Node >> OUT_nodes )

Points the binding at a set of objects at once, so that one channel drives every one of them.
### Arguments

- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)>>* **OUT_nodes** - Nodes the binding is to point at. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void setAssets ( Vector < UGUID > OUT_file_guids )

Points the binding at a set of assets at once.
### Arguments

- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[UGUID](../../../../api/library/filesystem/class.uguid_cpp.md)>* **OUT_file_guids** - File GUIDs of the assets. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## int getNumTargetSurfaceMatches ( int i ) const

Returns how many surfaces the specified target resolves to, which is what tells a surface pattern that found nothing from one that found many.
### Arguments

- *int* **i** - Target number.

### Return value

Number of surfaces the target resolves to.
## Ptr < Object > getTargetResolvedObject ( int i ) const

Returns the object the specified target of the binding resolves to in the loaded scene.
### Arguments

- *int* **i** - Target number.

### Return value

Object the target resolves to, or NULL (null in C#) if it resolves to none.
