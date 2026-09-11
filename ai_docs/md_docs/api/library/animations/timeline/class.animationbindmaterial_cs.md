# Unigine::AnimationBindMaterial Class (CS)

**Inherits from:** AnimationBind


This binding points a channel at a material, so that a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cs.md) animates a material parameter such as a color, an albedo scale or a texture shift.


The material is reached in one of two ways: straight from a material asset, which writes into the asset and shows on everything that uses it, or through a surface of an object, which gives that surface a child material and leaves the rest of the scene alone.


## AnimationBindMaterial Class

### Enums

## ACCESS

Access mode. It decides the way the animated material is obtained.
| Name | Description |
|---|---|
| **UNKNOWN** = -1 | The way to obtain the material is not set. |
| **FROM_ASSET** = 0 | The material is taken from a material asset, so the animation writes into the asset itself and reaches everything that uses it. |
| **FROM_SURFACE** = 1 | The material is taken from a surface of an object, which gives a child material of its own to that surface, so the animation touches nothing else. |

### Properties

## AnimationBindMaterial.ACCESS Access

The access mode of the binding. It decides the way the animated material is obtained.
## string SurfacePattern

The pattern the surface names are matched against. It picks the surfaces the binding works on inside every object the target resolves to.
### Members

---

## AnimationBindMaterial ( )

Constructor. Creates an empty material binding.
## void SetObjects ( Node [] OUT_nodes )

Points the binding at a set of objects at once, so that one channel drives every one of them.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Nodes the binding is to point at. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetAssets ( UGUID [] OUT_file_guids )

Points the binding at a set of assets at once.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)[]* **OUT_file_guids** - File GUIDs of the assets. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## int GetNumTargetSurfaceMatches ( int i )

Returns how many surfaces the specified target resolves to, which is what tells a surface pattern that found nothing from one that found many.
### Arguments

- *int* **i** - Target number.

### Return value

Number of surfaces the target resolves to.
## Object GetTargetResolvedObject ( int i )

Returns the object the specified target of the binding resolves to in the loaded scene.
### Arguments

- *int* **i** - Target number.

### Return value

Object the target resolves to, or NULL (null in C#) if it resolves to none.
