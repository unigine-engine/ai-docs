# Unigine.Decal Class (CPP)

**Header:** #include <UnigineDecals.h>

**Inherits from:** Node


Decal class is used for base [decals](../../../objects/decals/index.md) operation. To create, modify or get information on special types of the decals, use [decal-related classes](../../../api/library/decals/index.md).


## Decal Class

### Members

---

## void setMaterial ( const Ptr < Material > & mat )

Sets a new material for the decal.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **mat** - Smart pointer to the material to be used for the decal.

## Ptr < Material > getMaterial ( ) const

Returns the material used for the decal.
### Return value

Smart pointer to the material used for the decal.
## Ptr < Material > getMaterialInherit ( ) const

Inherits material for the decal (i.e. creates a material instance). Modifications made in a new material instance will not affect the source material.
> **Notice:** A child material will be created only once, all subsequent calls to this method will return the first created child material.


### Return value

Smart pointer to the inherited material.
## int isMaterialInherited ( ) const

Returns the value indicating if a given material is inherited (instanced). Modifications made in a material instance do not affect the source material.
### Return value

1 if the material is inherited successfully; otherwise, 0.
## void setMaxFadeDistance ( float distance )

Updates a maximum fade-out distance, across which the decal smoothly becomes invisible due to the [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [maximum visibility distance](#getMaxVisibleDistance_float) value.
### Arguments

- *float* **distance** - A new minimum fade-out distance, in units. If a negative value is provided, 0 will be used instead.

## float getMaxFadeDistance ( ) const

Returns a maximum fade-out distance, across which the decal smoothly becomes invisible due to the [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [maximum visibility distance](#getMaxVisibleDistance_float) value.
### Return value

Distance value, in units.
## void setMaxVisibleDistance ( float distance )

Updates the maximum visibility distance, starting at which the decal begins to fade out until becomes completely invisible.
### Arguments

- *float* **distance** - A maximum visibility distance, in units. If a negative value is provided, **0** will be used instead.

## float getMaxVisibleDistance ( ) const

Returns a maximum visibility distance, starting at which the decal begins to [fade out](#getMaxFadeDistance_float) until becomes completely invisible.
### Return value

Distance value, in units.
## void setMinFadeDistance ( float distance )

Updates a minimum fade-in distance, across which the decal smoothly becomes visible due to the [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [minimum visibility distance](#getMinVisibleDistance_float) value.
### Arguments

- *float* **distance** - A new minimum fade-in distance, in units. If a negative value is provided, 0 will be used instead.

## float getMinFadeDistance ( ) const

Returns a minimum fade-in distance, across which the decal smoothly becomes visible due to the [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [minimum visibility distance](#getMinVisibleDistance_float) value.
### Return value

Distance value, in units.
## void setMinVisibleDistance ( float distance )

Updates a minimum visibility distance, starting at which the decal begins to [fade in](#getMinFadeDistance_float) and then becomes completely visible.
### Arguments

- *float* **distance** - A new minimum visibility distance, in units. If a negative value is provided, 0 will be used instead.

## float getMinVisibleDistance ( ) const

Returns the minimum visibility distance, starting at which the decal begins to [fade in](#getMinFadeDistance_float) and then becomes completely visible.
### Return value

Distance value, in units.
## void setOpacity ( float opacity )

Sets opacity for the decal. This parameter enables you to control whether the decal should be opaque or semi-transparent.
### Arguments

- *float* **opacity** - New opacity value to be set in the [0.0f; 1.0f] range (1.0f - the decal is fully opaque).

## float getOpacity ( ) const

Returns the current opacity for the decal.
### Return value

Current opacity value in the [0.0f; 1.0f] range (1.0f - the decal is fully opaque).
## void setRadius ( float radius )

Sets the new height of the projection box/pyramid along the *Z* axis.
### Arguments

- *float* **radius** - Height of the projection box/pyramid along the *Z* axis, in units.

## float getRadius ( ) const

Returns the current height of the projection box along the Z axis.
### Return value

The height of the projection box along the Z axis, in units.
## void setViewportMask ( int mask )

Sets a bit mask for rendering a decal into the viewport. The decal is rendered, if its mask matches the camera viewport mask and the viewport mask of the decal's material.
### Arguments

- *int* **mask** - An integer value, each bit of which is used to set a mask.

## int getViewportMask ( ) const

Returns the current bit mask for rendering into the viewport. The decal is rendered, if its mask matches the camera viewport mask and the viewport mask of the decal's material.
### Return value

The integer value, each bit of which is used to set a mask.
## void setIntersectionMask ( int mask )

Sets a new intersection mask for the decal. This mask can be used to cut out areas intersected by the decal from [grass](../../../api/library/objects/class.objectgrass_cpp.md#setCutoutIntersectionMask_int_void), [mesh clutter](../../../api/library/objects/class.objectmeshclutter_cpp.md#setCutoutIntersectionMask_int_void) and [world clutter](../../../api/library/worlds/class.worldclutter_cpp.md#setCutoutIntersectionMask_int_void) (e.g. to remove grass or forest from the surface of roads projected using decals).
> **Notice:** The areas will be cut out only if intersection masks of grass and clutter objects matches this mask (one bit at least).


### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getIntersectionMask ( ) const

Returns the current intersection mask of the decal. This mask can be used to cut out areas intersected by the decal from [grass](../../../api/library/objects/class.objectgrass_cpp.md#setCutoutIntersectionMask_int_void), [mesh clutter](../../../api/library/objects/class.objectmeshclutter_cpp.md#setCutoutIntersectionMask_int_void) and [world clutter](../../../api/library/worlds/class.worldclutter_cpp.md#setCutoutIntersectionMask_int_void) (e.g. to remove grass or forest from the surface of roads projected using decals).
> **Notice:** The areas will be cut out only if intersection masks of grass and clutter objects matches this mask (one bit at least).


### Return value

Integer, each bit of which is a mask.
## int isTerrainHole ( ) const

Returns a value indicating if the decal is used to create a hole in the terrain.
### Return value

1 if the decal is used to create a terrain hole; otherwise, 0.
## int inside ( const Math::vec3& p )

Returns a value indicating if the point with the given coordinates is inside the decal (in object-space).
### Arguments

- *const  Math::vec3&* **p** - Point coordinates.

### Return value

1 if the point is inside the decal; otherwise, 0.
## void setMaterialFilePath ( const char * path )

Sets the material for the decal by file path.
### Arguments

- *const char ** **path** - Material file path.

## String getMaterialFilePath ( ) const

Returns the path to the material file used for the decal.
### Return value

Material file path.
## void setMaterialGUID ( const UGUID& materialguid )

Sets the material for the decal by [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
### Arguments

- *const UGUID&* **materialguid** - Material [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

## UGUID getMaterialGUID ( ) const

Returns the [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the material used for the decal.
### Return value

Material [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
## void setCastBakedGlobalIllumination ( bool illumination )

Sets a value indicating if the decal is to be ignored when baking *Global Illumination* (lightmaps and probes). When enabled, the decal behaves the same way as surfaces with the *Dynamic Lighting Mode* selected: they are invisible for *Voxel Probes* and *Environment Probes* and are not baked into lightmaps.
### Arguments

- *bool* **illumination** - true to ignore the decal when baking *Global Illumination* (lightmaps and probes); false to bake the decal to lightmaps and probes.

## bool isCastBakedGlobalIllumination ( ) const

Returns a value indicating if the decal is to be ignored when baking *Global Illumination* (lightmaps and probes). When enabled, the decal behaves the same way as surfaces with the *Dynamic Lighting Mode* selected: they are invisible for *Voxel Probes* and *Environment Probes* and are not baked into lightmaps.
### Return value

true if the decal is to be ignored when baking *Global Illumination* (lightmaps and probes); otherwise, false.
## float getSurfaceRenderCustomParameterFloat ( const char * name ) const

Returns the current value of the custom surface parameter with the given name for the decal. If the parameter is not overridden for the decal, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *const char ** **name** - Parameter name.

### Return value

Current parameter value, or 0 if no parameter with this name exists.
## float getSurfaceRenderCustomParameterFloat ( int param ) const

Returns the current value of the custom surface parameter with the given number for the decal. If the parameter is not overridden for the decal, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **param** - Parameter number.

### Return value

Current parameter value.
## int getSurfaceRenderCustomParameterInt ( const char * name ) const

Returns the current value of the custom surface parameter with the given name for the decal. If the parameter is not overridden for the decal, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *const char ** **name** - Parameter name.

### Return value

Current parameter value, or 0 if no parameter with this name exists.
## int getSurfaceRenderCustomParameterInt ( int param ) const

Returns the current value of the custom surface parameter with the given number for the decal. If the parameter is not overridden for the decal, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **param** - Parameter number.

### Return value

Current parameter value.
## unsigned int getSurfaceRenderCustomParameterUInt ( const char * name ) const

Returns the current value of the custom surface parameter with the given name for the decal. If the parameter is not overridden for the decal, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *const char ** **name** - Parameter name.

### Return value

Current parameter value, or 0 if no parameter with this name exists.
## unsigned int getSurfaceRenderCustomParameterUInt ( int param ) const

Returns the current value of the custom surface parameter with the given number for the decal. If the parameter is not overridden for the decal, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **param** - Parameter number.

### Return value

Current parameter value.
## bool isSurfaceRenderCustomParameterOverridden ( int param ) const

Checks if the custom surface parameter with the given number is overridden for the decal.
### Arguments

- *int* **param** - Parameter number.

### Return value

true if the parameter is overridden for the decal; otherwise, false.
## void resetSurfaceRenderCustomParameter ( int param )

Resets the override of the custom surface parameter with the given number: the decal uses the default value from the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)* again.
### Arguments

- *int* **param** - Parameter number.

## void resetSurfaceRenderCustomParameters ( )

Resets the overrides of all custom surface parameters of the decal.
## void setSurfaceRenderCustomParameterFloat ( const char * name , float value )

Sets a new value of the custom surface parameter with the given name for the decal. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)*. If no parameter with this name exists in the layout, the method does nothing.
### Arguments

- *const char ** **name** - Parameter name.
- *float* **value** - New parameter value.

## void setSurfaceRenderCustomParameterFloat ( int param , float value )

Sets a new value of the custom surface parameter with the given number for the decal. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)*.
### Arguments

- *int* **param** - Parameter number.
- *float* **value** - New parameter value.

## void setSurfaceRenderCustomParameterInt ( const char * name , int value )

Sets a new value of the custom surface parameter with the given name for the decal. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)*. If no parameter with this name exists in the layout, the method does nothing.
### Arguments

- *const char ** **name** - Parameter name.
- *int* **value** - New parameter value.

## void setSurfaceRenderCustomParameterInt ( int param , int value )

Sets a new value of the custom surface parameter with the given number for the decal. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)*.
### Arguments

- *int* **param** - Parameter number.
- *int* **value** - New parameter value.

## void setSurfaceRenderCustomParameterUInt ( const char * name , unsigned int value )

Sets a new value of the custom surface parameter with the given name for the decal. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)*. If no parameter with this name exists in the layout, the method does nothing.
### Arguments

- *const char ** **name** - Parameter name.
- *unsigned int* **value** - New parameter value.

## void setSurfaceRenderCustomParameterUInt ( int param , unsigned int value )

Sets a new value of the custom surface parameter with the given number for the decal. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)*.
### Arguments

- *int* **param** - Parameter number.
- *unsigned int* **value** - New parameter value.
