# Unigine::ImportAnimation Class (CS)


This class is an intermediate representation of an animation clip from a source file. It stores the animation time range and references the associated [skeleton](../../../../api/library/common/import/class.importskeleton_cs.md). During import, it is used together with an [ImportMeshSkinned](../../../../api/library/common/import/class.importmeshskinned_cs.md) to produce a [MeshSkinnedAnimation](../../../../api/library/rendering/class.meshskinnedanimation_cs.md).


## ImportAnimation Class

### Properties

## IntPtr Data

The metadata of the animation.
## string Filepath

The path to the output animation file.
## string Name

The name of the animation.
## float MaxTime

The end time of the animation.
## float MinTime

The start time of the animation.
## ImportSkeleton Skeleton

The [import skeleton](../../../../api/library/common/import/class.importskeleton_cs.md) associated with the animation.
### Members

---

## ImportAnimation ( )

Constructor. Creates an empty *ImportAnimation* instance.
