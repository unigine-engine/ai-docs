# Unigine::ImportSurface Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class represents an individual surface within an [ImportGeometry](../../../../api/library/common/import/class.importgeometry_usc.md) - a renderable part of the geometry with its own [material](../../../../api/library/common/import/class.importmaterial_usc.md), visibility and fade distance settings, and bounding box.


## ImportSurface Class

### Members

## void setBoundBox ( WorldBoundBox box )

Sets a new bounding box of the geometry element.
### Arguments

- *WorldBoundBox* **box** - The geometry element bounding box.

## WorldBoundBox getBoundBox () const

Returns the current bounding box of the geometry element.
### Return value

Current geometry element bounding box.
## void setData ( vptr data )

Sets a new metadata of the imported surface.
### Arguments

- *vptr* **data** - The surface metadata.

## vptr getData () const

Returns the current metadata of the imported surface.
### Return value

Current surface metadata.
## void setName ( string name )

Sets a new name of the imported surface.
### Arguments

- *string* **name** - The surface name.

## const char * getName () const

Returns the current name of the imported surface.
### Return value

Current surface name.
## void setMaterial ( ImportMaterial material )

Sets a new material assigned to the imported surface.
### Arguments

- *[ImportMaterial](../../../../api/library/common/import/class.importmaterial_usc.md)* **material** - The surface material: *[ImportMaterial](../../../../api/library/common/import/class.importmaterial_usc.md)* class instance if a material is assigned to the imported surface; otherwise, **nullptr**

## ImportMaterial getMaterial () const

Returns the current material assigned to the imported surface.
### Return value

Current surface material: *[ImportMaterial](../../../../api/library/common/import/class.importmaterial_usc.md)* class instance if a material is assigned to the imported surface; otherwise, **nullptr**
## void setMaxFadeDistance ( float distance )

Sets a new [Maximum Fade Distance](../../../../principles/world_management/index.md#max_fade) for the imported surface.
### Arguments

- *float* **distance** - The maximum fade distance, in units.

## float getMaxFadeDistance () const

Returns the current [Maximum Fade Distance](../../../../principles/world_management/index.md#max_fade) for the imported surface.
### Return value

Current maximum fade distance, in units.
## void setMinFadeDistance ( float distance )

Sets a new [Minimum Fade Distance](../../../../principles/world_management/index.md#min_fade) for the imported surface.
### Arguments

- *float* **distance** - The minimum fade distance, in units.

## float getMinFadeDistance () const

Returns the current [Minimum Fade Distance](../../../../principles/world_management/index.md#min_fade) for the imported surface.
### Return value

Current minimum fade distance, in units.
## void setMaxVisibleDistance ( float distance )

Sets a new [Maximum Visibility Distance](../../../../principles/world_management/index.md#min_visible) for the imported surface.
### Arguments

- *float* **distance** - The maximum visibility distance, in units.

## float getMaxVisibleDistance () const

Returns the current [Maximum Visibility Distance](../../../../principles/world_management/index.md#min_visible) for the imported surface.
### Return value

Current maximum visibility distance, in units.
## void setMinVisibleDistance ( float distance )

Sets a new [Minimum Visibility Distance](../../../../principles/world_management/index.md#min_visible) for the imported surface.
### Arguments

- *float* **distance** - The minimum visibility distance, in units.

## float getMinVisibleDistance () const

Returns the current [Minimum Visibility Distance](../../../../principles/world_management/index.md#min_visible) for the imported surface.
### Return value

Current minimum visibility distance, in units.
## void setSourceIndex ( int index )

Sets a new index of the surface in the source file (FBX, glTF).
### Arguments

- *int* **index** - The surface index in the source file (FBX, glTF).

## int getSourceIndex () const

Returns the current index of the surface in the source file (FBX, glTF).
### Return value

Current surface index in the source file (FBX, glTF).
## void setTargetSurface ( int surface )

Sets a new number of the morph target surface for the imported surface.
### Arguments

- *int* **surface** - The morph target surface number if any; otherwise, -1.

## int getTargetSurface () const

Returns the current number of the morph target surface for the imported surface.
### Return value

Current morph target surface number if any; otherwise, -1.
---

## void copyFrom ( ImportSurface o )

Copies the data from the specified source surface.
### Arguments

- *[ImportSurface](../../../../api/library/common/import/class.importsurface_usc.md)* **o** - Source surface.
