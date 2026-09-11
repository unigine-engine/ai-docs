# Unigine.Decal Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


Decal class is used for base [decals](../../../objects/decals/index.md) operation. To create, modify or get information on special types of the decals, use [decal-related classes](../../../api/library/decals/index.md).


## Decal Class

### Members

---

## void setMaterial ( )

Sets a new material for the decal.
### Arguments

## Material getMaterial ( )

Returns the material used for the decal.
### Return value

Material used for the decal.
## Material getMaterialInherit ( )

Inherits material for the decal (i.e. creates a material instance). Modifications made in a new material instance will not affect the source material.
> **Notice:** A child material will be created only once, all subsequent calls to this method will return the first created child material.


### Return value

The inherited material.
## int isMaterialInherited ( )

Returns the value indicating if a given material is inherited (instanced). Modifications made in a material instance do not affect the source material.
### Return value

Positive number if the material is inherited; otherwise, **0**.
## void setMaxFadeDistance ( float distance )

Updates a maximum fade-out distance, across which the decal smoothly becomes invisible due to the [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [maximum visibility distance](#getMaxVisibleDistance_float) value.
### Arguments

- *float* **distance** - A new minimum fade-out distance, in units. If a negative value is provided, 0 will be used instead.

## float getMaxFadeDistance ( )

Returns a maximum fade-out distance, across which the decal smoothly becomes invisible due to the [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [maximum visibility distance](#getMaxVisibleDistance_float) value.
### Return value

Distance value, in units.
## void setMaxVisibleDistance ( float distance )

Updates the maximum visibility distance, starting at which the decal begins to fade out until becomes completely invisible.
### Arguments

- *float* **distance** - A maximum visibility distance, in units. If a negative value is provided, **0** will be used instead.

## float getMaxVisibleDistance ( )

Returns a maximum visibility distance, starting at which the decal begins to [fade out](#getMaxFadeDistance_float) until becomes completely invisible.
### Return value

Distance value, in units.
## void setMinFadeDistance ( float distance )

Updates a minimum fade-in distance, across which the decal smoothly becomes visible due to the [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [minimum visibility distance](#getMinVisibleDistance_float) value.
### Arguments

- *float* **distance** - A new minimum fade-in distance, in units. If a negative value is provided, 0 will be used instead.

## float getMinFadeDistance ( )

Returns a minimum fade-in distance, across which the decal smoothly becomes visible due to the [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [minimum visibility distance](#getMinVisibleDistance_float) value.
### Return value

Distance value, in units.
## void setMinVisibleDistance ( float distance )

Updates a minimum visibility distance, starting at which the decal begins to [fade in](#getMinFadeDistance_float) and then becomes completely visible.
### Arguments

- *float* **distance** - A new minimum visibility distance, in units. If a negative value is provided, 0 will be used instead.

## float getMinVisibleDistance ( )

Returns the minimum visibility distance, starting at which the decal begins to [fade in](#getMinFadeDistance_float) and then becomes completely visible.
### Return value

Distance value, in units.
## void setOpacity ( float opacity )

Sets opacity for the decal. This parameter enables you to control whether the decal should be opaque or semi-transparent.
### Arguments

- *float* **opacity** - New opacity value to be set in the [0.0f; 1.0f] range (1.0f - the decal is fully opaque).

## float getOpacity ( )

Returns the current opacity for the decal.
### Return value

Current opacity value in the [0.0f; 1.0f] range (1.0f - the decal is fully opaque).
## void setRadius ( float radius )

Sets the new height of the projection box/pyramid along the *Z* axis.
### Arguments

- *float* **radius** - Height of the projection box/pyramid along the *Z* axis, in units.

## float getRadius ( )

Returns the current height of the projection box along the Z axis.
### Return value

The height of the projection box along the Z axis, in units.
## void setViewportMask ( int mask )

Sets a bit mask for rendering a decal into the viewport. The decal is rendered, if its mask matches the camera viewport mask and the viewport mask of the decal's material.
### Arguments

- *int* **mask** - An integer value, each bit of which is used to set a mask.

## int getViewportMask ( )

Returns the current bit mask for rendering into the viewport. The decal is rendered, if its mask matches the camera viewport mask and the viewport mask of the decal's material.
### Return value

The integer value, each bit of which is used to set a mask.
## void setIntersectionMask ( int mask )

Sets a new intersection mask for the decal. This mask can be used to cut out areas intersected by the decal from [grass](../../../api/library/objects/class.objectgrass_usc.md#setCutoutIntersectionMask_int_void), [mesh clutter](../../../api/library/objects/class.objectmeshclutter_usc.md#setCutoutIntersectionMask_int_void) and [world clutter](../../../api/library/worlds/class.worldclutter_usc.md#setCutoutIntersectionMask_int_void) (e.g. to remove grass or forest from the surface of roads projected using decals).
> **Notice:** The areas will be cut out only if intersection masks of grass and clutter objects matches this mask (one bit at least).


### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getIntersectionMask ( )

Returns the current intersection mask of the decal. This mask can be used to cut out areas intersected by the decal from [grass](../../../api/library/objects/class.objectgrass_usc.md#setCutoutIntersectionMask_int_void), [mesh clutter](../../../api/library/objects/class.objectmeshclutter_usc.md#setCutoutIntersectionMask_int_void) and [world clutter](../../../api/library/worlds/class.worldclutter_usc.md#setCutoutIntersectionMask_int_void) (e.g. to remove grass or forest from the surface of roads projected using decals).
> **Notice:** The areas will be cut out only if intersection masks of grass and clutter objects matches this mask (one bit at least).


### Return value

Integer, each bit of which is a mask.
## int isTerrainHole ( )

Returns a value indicating if the decal is used to create a hole in the terrain.
### Return value

1 if the decal is used to create a terrain hole; otherwise, 0.
## int inside ( vec3 p )

Returns a value indicating if the point with the given coordinates is inside the decal (in object-space).
### Arguments

- *vec3* **p** - Point coordinates.

### Return value

1 if the point is inside the decal; otherwise, 0.
## void setMaterialFilePath ( string path )

Sets the material for the decal by file path.
### Arguments

- *string* **path** - Material file path.

## string getMaterialFilePath ( )

Returns the path to the material file used for the decal.
### Return value

Material file path.
## void setMaterialGUID ( UGUID materialguid )

Sets the material for the decal by [GUID](../../../api/library/filesystem/class.uguid_usc.md).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **materialguid** - Material [GUID](../../../api/library/filesystem/class.uguid_usc.md).

## UGUID getMaterialGUID ( )

Returns the [GUID](../../../api/library/filesystem/class.uguid_usc.md) of the material used for the decal.
### Return value

Material [GUID](../../../api/library/filesystem/class.uguid_usc.md).
## void setCastBakedGlobalIllumination ( int illumination )

Sets a value indicating if the decal is to be ignored when baking *Global Illumination* (lightmaps and probes). When enabled, the decal behaves the same way as surfaces with the *Dynamic Lighting Mode* selected: they are invisible for *Voxel Probes* and *Environment Probes* and are not baked into lightmaps.
### Arguments

- *int* **illumination** - **1** to ignore the decal when baking *Global Illumination* (lightmaps and probes); **0** to bake the decal to lightmaps and probes.

## int isCastBakedGlobalIllumination ( )

Returns a value indicating if the decal is to be ignored when baking *Global Illumination* (lightmaps and probes). When enabled, the decal behaves the same way as surfaces with the *Dynamic Lighting Mode* selected: they are invisible for *Voxel Probes* and *Environment Probes* and are not baked into lightmaps.
### Return value

**1** if the decal is to be ignored when baking *Global Illumination* (lightmaps and probes); otherwise, **0**.
## bool isSurfaceRenderCustomParameterOverridden ( int param )

Checks if the custom surface parameter with the given number is overridden for the decal.
### Arguments

- *int* **param** - Parameter number.

### Return value

**1** if the parameter is overridden for the decal; otherwise, **0**.
## void resetSurfaceRenderCustomParameter ( int param )

Resets the override of the custom surface parameter with the given number: the decal uses the default value from the *[surface parameters layout](../../../api/library/rendering/class.render_usc.md#getSurfaceParameters_CustomParameterLayout)* again.
### Arguments

- *int* **param** - Parameter number.

## void resetSurfaceRenderCustomParameters ( )

Resets the overrides of all custom surface parameters of the decal.
