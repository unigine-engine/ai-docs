# Unigine::ImportSurface Class (CS)


This class represents an individual surface within an [ImportGeometry](../../../../api/library/common/import/class.importgeometry_cs.md) - a renderable part of the geometry with its own [material](../../../../api/library/common/import/class.importmaterial_cs.md), visibility and fade distance settings, and bounding box.


## ImportSurface Class

### Properties

## WorldBoundBox BoundBox

The bounding box of the geometry element.
## IntPtr Data

The metadata of the imported surface.
## string Name

The name of the imported surface.
## ImportMaterial Material

The material assigned to the imported surface.
## float MaxFadeDistance

The [Maximum Fade Distance](../../../../principles/world_management/index.md#max_fade) for the imported surface.
## float MinFadeDistance

The [Minimum Fade Distance](../../../../principles/world_management/index.md#min_fade) for the imported surface.
## float MaxVisibleDistance

The [Maximum Visibility Distance](../../../../principles/world_management/index.md#min_visible) for the imported surface.
## float MinVisibleDistance

The [Minimum Visibility Distance](../../../../principles/world_management/index.md#min_visible) for the imported surface.
## int SourceIndex

The index of the surface in the source file (FBX, glTF).
## int TargetSurface

The number of the morph target surface for the imported surface.
### Members

---

## void CopyFrom ( ImportSurface o )

Copies the data from the specified source surface.
### Arguments

- *[ImportSurface](../../../../api/library/common/import/class.importsurface_cs.md)* **o** - Source surface.
