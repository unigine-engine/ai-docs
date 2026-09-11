# Unigine.Decal Class (CS)

**Inherits from:** Node


Decal class is used for base [decals](../../../objects/decals/index.md) operation. To create, modify or get information on special types of the decals, use [decal-related classes](../../../api/library/decals/index.md).


## Decal Class

### Properties

## int IntersectionMask

The current intersection mask of the decal. this mask can be used to cut out areas intersected by the decal from [grass](../../../api/library/objects/class.objectgrass_cs.md#setCutoutIntersectionMask_int_void), [mesh clutter](../../../api/library/objects/class.objectmeshclutter_cs.md#setCutoutIntersectionMask_int_void) and [world clutter](../../../api/library/worlds/class.worldclutter_cs.md#setCutoutIntersectionMask_int_void) (e.g. to remove grass or forest from the surface of roads projected using decals).
> **Notice:** The areas will be cut out only if intersection masks of grass and clutter objects matches this mask (one bit at least).


## int ViewportMask

The current bit mask for rendering into the viewport. the decal is rendered, if its mask matches the camera viewport mask and the viewport mask of the decal's material.
## float MinVisibleDistance

The minimum visibility distance, starting at which the decal begins to [fade in](#getMinFadeDistance_float) and then becomes completely visible.
## float MinFadeDistance

The minimum fade-in distance, across which the decal smoothly becomes visible due to the [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [minimum visibility distance](#getMinVisibleDistance_float) value.
## float MaxVisibleDistance

The maximum visibility distance, starting at which the decal begins to [fade out](#getMaxFadeDistance_float) until becomes completely invisible.
## float MaxFadeDistance

The maximum fade-out distance, across which the decal smoothly becomes invisible due to the [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [maximum visibility distance](#getMaxVisibleDistance_float) value.
## float Opacity

The opacity for the decal in the [0.0f; 1.0f] range (1.0f - the decal is fully opaque). This parameter enables you to control whether the decal should be opaque or semi-transparent.
## float Radius

The current height of the projection box/pyramid along the z axis.
## Material Material

The material used for the decal.
## 🔒︎ Material MaterialInherit

The inherited material for the decal (i.e. creates a material instance). Modifications made in a new material instance will not affect the source material.
> **Notice:** A child material will be created only once, all subsequent calls to this method will return the first created child material.


## UGUID MaterialGUID

The [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the material used for the decal.
## string MaterialFilePath

The path to the material file used for the decal.
## bool CastBakedGlobalIllumination

The value indicating if the decal is to be ignored when baking *Global Illumination* (lightmaps and probes). When enabled, the decal behaves the same way as surfaces with the *Dynamic Lighting Mode* selected: they are invisible for *Voxel Probes* and *Environment Probes* and are not baked into lightmaps.
### Members

---

## int IsMaterialInherited ( )

Returns the value indicating if a given material is inherited (instanced). Modifications made in a material instance do not affect the source material.
### Return value

1 if the material is inherited successfully; otherwise, 0.
## int IsTerrainHole ( )

Returns a value indicating if the decal is used to create a hole in the terrain.
### Return value

1 if the decal is used to create a terrain hole; otherwise, 0.
## int Inside ( vec3 p )

Returns a value indicating if the point with the given coordinates is inside the decal (in object-space).
### Arguments

- *vec3* **p** - Point coordinates.

### Return value

1 if the point is inside the decal; otherwise, 0.
## void SetCastBakedGlobalIllumination ( bool illumination )

Sets a value indicating if the decal is to be ignored when baking *Global Illumination* (lightmaps and probes). When enabled, the decal behaves the same way as surfaces with the *Dynamic Lighting Mode* selected: they are invisible for *Voxel Probes* and *Environment Probes* and are not baked into lightmaps.
### Arguments

- *bool* **illumination** - true to ignore the decal when baking *Global Illumination* (lightmaps and probes); false to bake the decal to lightmaps and probes.

## bool IsCastBakedGlobalIllumination ( )

Returns a value indicating if the decal is to be ignored when baking *Global Illumination* (lightmaps and probes). When enabled, the decal behaves the same way as surfaces with the *Dynamic Lighting Mode* selected: they are invisible for *Voxel Probes* and *Environment Probes* and are not baked into lightmaps.
### Return value

true if the decal is to be ignored when baking *Global Illumination* (lightmaps and probes); otherwise, false.
## float GetSurfaceRenderCustomParameterFloat ( string name )

Returns the current value of the custom surface parameter with the given name for the decal. If the parameter is not overridden for the decal, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *string* **name** - Parameter name.

### Return value

Current parameter value, or 0 if no parameter with this name exists.
## float GetSurfaceRenderCustomParameterFloat ( int param )

Returns the current value of the custom surface parameter with the given number for the decal. If the parameter is not overridden for the decal, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **param** - Parameter number.

### Return value

Current parameter value.
## int GetSurfaceRenderCustomParameterInt ( string name )

Returns the current value of the custom surface parameter with the given name for the decal. If the parameter is not overridden for the decal, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *string* **name** - Parameter name.

### Return value

Current parameter value, or 0 if no parameter with this name exists.
## int GetSurfaceRenderCustomParameterInt ( int param )

Returns the current value of the custom surface parameter with the given number for the decal. If the parameter is not overridden for the decal, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **param** - Parameter number.

### Return value

Current parameter value.
## uint GetSurfaceRenderCustomParameterUInt ( string name )

Returns the current value of the custom surface parameter with the given name for the decal. If the parameter is not overridden for the decal, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *string* **name** - Parameter name.

### Return value

Current parameter value, or 0 if no parameter with this name exists.
## uint GetSurfaceRenderCustomParameterUInt ( int param )

Returns the current value of the custom surface parameter with the given number for the decal. If the parameter is not overridden for the decal, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **param** - Parameter number.

### Return value

Current parameter value.
## bool IsSurfaceRenderCustomParameterOverridden ( int param )

Checks if the custom surface parameter with the given number is overridden for the decal.
### Arguments

- *int* **param** - Parameter number.

### Return value

true if the parameter is overridden for the decal; otherwise, false.
## void ResetSurfaceRenderCustomParameter ( int param )

Resets the override of the custom surface parameter with the given number: the decal uses the default value from the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)* again.
### Arguments

- *int* **param** - Parameter number.

## void ResetSurfaceRenderCustomParameters ( )

Resets the overrides of all custom surface parameters of the decal.
## void SetSurfaceRenderCustomParameterFloat ( string name , float value )

Sets a new value of the custom surface parameter with the given name for the decal. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)*. If no parameter with this name exists in the layout, the method does nothing.
### Arguments

- *string* **name** - Parameter name.
- *float* **value** - New parameter value.

## void SetSurfaceRenderCustomParameterFloat ( int param , float value )

Sets a new value of the custom surface parameter with the given number for the decal. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)*.
### Arguments

- *int* **param** - Parameter number.
- *float* **value** - New parameter value.

## void SetSurfaceRenderCustomParameterInt ( string name , int value )

Sets a new value of the custom surface parameter with the given name for the decal. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)*. If no parameter with this name exists in the layout, the method does nothing.
### Arguments

- *string* **name** - Parameter name.
- *int* **value** - New parameter value.

## void SetSurfaceRenderCustomParameterInt ( int param , int value )

Sets a new value of the custom surface parameter with the given number for the decal. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)*.
### Arguments

- *int* **param** - Parameter number.
- *int* **value** - New parameter value.

## void SetSurfaceRenderCustomParameterUInt ( string name , uint value )

Sets a new value of the custom surface parameter with the given name for the decal. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)*. If no parameter with this name exists in the layout, the method does nothing.
### Arguments

- *string* **name** - Parameter name.
- *uint* **value** - New parameter value.

## void SetSurfaceRenderCustomParameterUInt ( int param , uint value )

Sets a new value of the custom surface parameter with the given number for the decal. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)*.
### Arguments

- *int* **param** - Parameter number.
- *uint* **value** - New parameter value.
