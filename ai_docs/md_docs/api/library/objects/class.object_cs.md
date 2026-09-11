# Object Class (CS)

**Inherits from:** Node


An [object](../../../objects/index.md) with a set of [surfaces](../../../principles/world_structure/index.md#surfaces) to represent geometry. Rendering materials are [assigned](#setMaterial_Material_int_void) per object surface. An object can be assigned a [physical body](#setBody_Body_int_int).


## Object Class

### Enums

## SURFACE_SHADOW_MODE

| Name | Description |
|---|---|
| **MIXED** = 0 | Mode to cast shadows from both static and dynamic light sources. |
| **DYNAMIC** = 1 | Mode to cast shadows only if the surface is lit by a dynamic light source. |

## SURFACE_LIGHTING_MODE

| Name | Description |
|---|---|
| **STATIC** = 0 | Optimized for use in static GI, static reflections and cached shadows. |
| **DYNAMIC** = 1 | Excludes the surface from use in static GI and static reflections and is suitable for dynamic shadows. |
| **ADVANCED** = 2 | Enables manual adjustment of all lighting-related settings. |

### Properties

## 🔒︎ int NumSurfaces

The number of surfaces of the object.
> **Notice:** For your convenience, *[ObjectMeshDynamic()](../../../api/library/objects/class.objectmeshdynamic_cs.md#ObjectMeshDynamic_constPtrMesh_int)* initializes the object with one internal surface named "`dynamic`". The first call to *[AddSurface()](../../../api/library/objects/class.objectmeshdynamic_cs.md#addSurface_cstr_void)* simply assigns a user-defined name to this surface without changing the total surface count. To create additional surfaces, call *[AddSurface()](../../../api/library/objects/class.objectmeshdynamic_cs.md#addSurface_cstr_void)* again.


## bool Enabled

The value indicating if the node and its parent nodes are enabled.
## 🔒︎ BodyRigid BodyRigid

The rigid body assigned to the object.
## Body Body

The physical body assigned to the object, or **NULL** (**0**) if no body is assigned.
## 🔒︎ bool IsVisibleShadow

The value indicating if the object's shadow is rendered.
## 🔒︎ bool IsVisibleCamera

The value indicating if the object is rendered.
### Members

---

## bool SetBody ( Body body , bool update = 1 )

Assigns a physical body to the object.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body** - Physical body to be assigned to the object.
- *bool* **update** - Update flag. Set this flag to update the object after assigning the specified body to it.

### Return value

true if the specified body is set successfully; otherwise, false.
## BoundBox GetBoundBox ( int surface )

Returns the bounding box of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Bounding box.
## BoundSphere GetBoundSphere ( int surface )

Returns the bounding sphere of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Bounding sphere.
## void SetBakeToEnvProbe ( bool enabled , int surface )

Sets a value indicating if the specified surface is to be baked to environment probes.
### Arguments

- *bool* **enabled** - **1** to enable baking of the specified surface to environment probes, **0** - to disable it.
- *int* **surface** - Surface number.

## bool GetBakeToEnvProbe ( int surface )

Returns a value indicating if the specified surface is to be baked to environment probes.
### Arguments

- *int* **surface** - Surface number.

### Return value

true if the specified surface is to be baked to environment probes; otherwise, false.
## void SetBakeToGI ( bool enabled , int surface )

Sets a value indicating if the specified surface is to be baked to GI (voxel probes and lightmaps).
### Arguments

- *bool* **enabled** - **1** to enable baking of the specified surface to GI, **0** - to disable it.
- *int* **surface** - Surface number.

## bool GetBakeToGI ( int surface )

Returns a value indicating if the specified surface is to be baked to GI (voxel probes and lightmaps).
### Arguments

- *int* **surface** - Surface number.

### Return value

**1** if the specified surface is to be baked to GI; otherwise, **0**.
## void SetCastEnvProbeShadow ( bool enabled , int surface )

Enables or disables casting shadows from environment probes by the specified surface.
### Arguments

- *bool* **enabled** - **1** to enable casting shadows from environment probes by the specified surface, **0** to disable it.
- *int* **surface** - Surface number.

## bool GetCastEnvProbeShadow ( int surface )

Returns a value indicating if casting shadows from environment probes by the specified surface is enabled.
### Arguments

- *int* **surface** - Surface number.

### Return value

**1** if casting shadows from environment probes by the specified surface is enabled; otherwise, **0**.
## void SetCastShadow ( bool enabled , int surface )

Enables or disables casting shadows from non-world lights for a given surface.
### Arguments

- *bool* **enabled** - **1** if shadows are to be cast by a given surface; otherwise, **0**.
- *int* **surface** - Surface number.

## bool GetCastShadow ( int surface )

Returns the surface cast shadow flag, which indicates if a given surface should cast shadows from non-world lights.
### Arguments

- *int* **surface** - Surface number.

### Return value

Positive number if shadows are cast by a given surface; otherwise, **0**.
## void SetCastWorldShadow ( bool enabled , int surface )

Enables or disables casting shadows from world lights for a given surface.
### Arguments

- *bool* **enabled** - true if world shadows are to be cast by a given surface; otherwise, false.
- *int* **surface** - Surface number.

## bool GetCastWorldShadow ( int surface )

Returns the surface cast world shadow flag, which indicates if a given surface should cast shadows from world lights.
### Arguments

- *int* **surface** - Surface number.

### Return value

Positive number if world shadows are cast by a given surface; otherwise, **0**.
## void SetCollision ( bool enabled , int surface )

Enables or disables [collision detection](../../../principles/physics/collision/index.md) for a given surface.
### Arguments

- *bool* **enabled** - **1** if collision detection is enabled for a given surface; otherwise, **0**.
- *int* **surface** - Surface number.

## bool GetCollision ( int surface )

Returns the surface collision flag, which indicates if [collision detection](../../../principles/physics/collision/index.md) for a given surface is enabled.
### Arguments

- *int* **surface** - Surface number.

### Return value

Positive number if collision detection is enabled for a given surface; otherwise, **0**.
## void SetCollisionMask ( int mask , int surface )

Sets a collision mask for a given surface. Two objects collide, if they both have matching masks.
### Arguments

- *int* **mask** - Surface collision mask.
- *int* **surface** - Surface number.

## int GetCollisionMask ( int surface )

Returns the collision mask for a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface collision mask.
## void SetEnabled ( bool enabled , int surface )

Enables or disables a surface with the specified number. The disabled surface is not rendered, does not take part in collision detection, and does not cast shadows.
```csharp
// temporarily disable the first surface of the object (index 0)
obj.SetEnabled(false, 0);

//...

// enable the first surface again if it is disabled
if(!obj.IsEnabled(0))
	obj.SetEnabled(true, 0);

```


### Arguments

- *bool* **enabled** - true to enable the surface, false to disable it.
- *int* **surface** - Surface number.

## bool IsEnabled ( int surface )

Returns a value indicating if a given surface is enabled.
```csharp
// temporarily disable the first surface of the object (index 0)
obj.SetEnabled(false, 0);

//...

// enable the first surface again if it is disabled
if(!obj.IsEnabled(0))
	obj.SetEnabled(true, 0);

```


### Arguments

- *int* **surface** - Surface number.

### Return value

true if the surface is enabled; otherwise, false.
## void SetIntersection ( bool enabled , int surface )

Enables or disables intersections with a given surface.
### Arguments

- *bool* **enabled** - true to enable intersections with a given surface, false to disable them.
- *int* **surface** - Surface number.

## bool GetIntersection ( vec3 p0 , vec3 p1 , ObjectIntersectionTexCoord v , int surface )

Checks if there is an intersection between a line and a given surface. If the function returns true the data about the texture coordinates of the intersection point will be put to [ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_cs.md) object.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cs.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cs.md#intersections)*


### Arguments

- *vec3* **p0** - Line start point coordinates (local).
- *vec3* **p1** - Line end point coordinates (local).
- *[ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_cs.md)* **v** - [ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_cs.md) class instance to store corresponding intersection data.
- *int* **surface** - Surface number.

### Return value

true if there is an intersection with a given surface; otherwise, false.
## bool GetIntersection ( int surface )

Returns a surface intersection flag. This flag indicates if intersections with a given surface are enabled.
### Arguments

- *int* **surface** - Surface number.

### Return value

true if intersections with a given surface are enabled; otherwise, false.
## bool GetIntersection ( vec3 p0 , vec3 p1 , ObjectIntersectionNormal v , int surface )

Checks if there is an intersection between a line and a given surface. If the function returns true the data about the normal at the intersection point will be put to [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_cs.md) object.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cs.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cs.md#intersections)*

### Arguments

- *vec3* **p0** - Line start point coordinates (local).
- *vec3* **p1** - Line end point coordinates (local).
- *[ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_cs.md)* **v** - [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_cs.md) class instance to store corresponding intersection data.
- *int* **surface** - Surface number.

### Return value

true if there is an intersection with a given surface; otherwise, false.
## bool GetIntersection ( vec3 p0 , vec3 p1 , int mask , ObjectIntersection v , int[] ret_surface )

Checks if there is an intersection between a line and a surface with a given intersection mask. If the function returns true the data about the intersection point will be put to [ObjectIntersection](../../../api/library/objects/class.objectintersection_cs.md) object and the number of the first intersected surface will be put to the return variable.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cs.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cs.md#intersections)*

### Arguments

- *vec3* **p0** - Line start point coordinates (local).
- *vec3* **p1** - Line end point coordinates (local).
- *int* **mask** - Intersection mask.
- *[ObjectIntersection](../../../api/library/objects/class.objectintersection_cs.md)* **v** - [ObjectIntersection](../../../api/library/objects/class.objectintersection_cs.md) class instance to store corresponding intersection data.
- *int[]* **ret_surface** - Intersected surface index.

### Return value

true if there is an intersection; otherwise, false.
## bool GetIntersection ( vec3 p0 , vec3 p1 , ObjectIntersection v , int surface )

Checks if there is an intersection between a line and a given surface. If the function returns true the data about the intersection point will be put to [ObjectIntersection](../../../api/library/objects/class.objectintersection_cs.md) object.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cs.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cs.md#intersections)*

### Arguments

- *vec3* **p0** - Line start point coordinates (local).
- *vec3* **p1** - Line end point coordinates (local).
- *[ObjectIntersection](../../../api/library/objects/class.objectintersection_cs.md)* **v** - [ObjectIntersection](../../../api/library/objects/class.objectintersection_cs.md) class instance to store corresponding intersection data.
- *int* **surface** - Surface number.

### Return value

true if there is an intersection with a given surface; otherwise, false.
## bool GetIntersection ( vec3 p0 , vec3 p1 , int mask , ObjectIntersectionNormal v , int[] ret_surface )

Checks if there is an intersection between a line and a surface with a given intersection mask. If the function returns true the data about the normal at the intersection point will be put to [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_cs.md) object and the number of the first intersected surface will be put to the return variable.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cs.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cs.md#intersections)*

### Arguments

- *vec3* **p0** - Line start point coordinates (local).
- *vec3* **p1** - Line end point coordinates (local).
- *int* **mask** - Intersection mask.
- *[ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_cs.md)* **v** - [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_cs.md) class instance to store corresponding intersection data.
- *int[]* **ret_surface** - Intersected surface index.

### Return value

true if there is an intersection; otherwise, false.
## bool GetIntersection ( vec3 p0 , vec3 p1 , int mask , ObjectIntersectionTexCoord v , int[] ret_surface )

Checks if there is an intersection between a line and a surface with a given intersection mask. If the function returns true the data about the texture coordinates of the intersection point will be put to [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_cs.md) object and the number of the first intersected surface will be put to the return variable.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cs.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cs.md#intersections)*

### Arguments

- *vec3* **p0** - Line start point coordinates (local).
- *vec3* **p1** - Line end point coordinates (local).
- *int* **mask** - Intersection mask.
- *[ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_cs.md)* **v** - [ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_cs.md) class instance to store corresponding intersection data.
- *int[]* **ret_surface** - Intersected surface index.

### Return value

true if there is an intersection; otherwise, false.
## bool GetIntersection ( vec3 p0 , vec3 p1 , int mask , vec3[] ret_point , vec3[] OUT_ret_normal , vec4[] OUT_ret_texcoord , int[] ret_index , int[] OUT_ret_instance , int[] ret_surface )

Checks if there is an intersection between a line and a surface with a given intersection mask. If the function returns true the data about the intersection (point, normal and texture coordinates) and the number of the first intersected surface will be put to corresponding return variables.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cs.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cs.md#intersections)*

### Arguments

- *vec3* **p0** - Line start point coordinates (local).
- *vec3* **p1** - Line end point coordinates (local).
- *int* **mask** - Intersection mask.
- *vec3[]* **ret_point** - Intersection point coordinates (object's local coordinate system). Pass NULL if this parameter is not required.
- *vec3[]* **OUT_ret_normal** - Coordinates of the normal vector to the intersection point. Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *vec4[]* **OUT_ret_texcoord** - Texture coordinates of the intersection point (vec4, where vec4.xy is for the first (0) UV channel, vec4.zw is for the second (1) UV channel). Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int[]* **ret_index** - Intersected triangle number. Pass NULL if this parameter is not required.
- *int[]* **OUT_ret_instance** - Intersected instance number. Pass NULL if this parameter is not required. > **Notice:** Intersected instance number can be obtained for the following classes: > - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cs.md)* > - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cs.md)* > - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cs.md)* > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int[]* **ret_surface** - Intersected surface number. Pass NULL if this parameter is not required.

### Return value

true if there is at least one intersection found; otherwise, false.
## bool GetIntersection ( vec3 p0 , vec3 p1 , vec3[] ret_point , vec3[] OUT_ret_normal , vec4[] OUT_ret_texcoord , int[] ret_index , int[] OUT_ret_instance , int surface )

Checks if there is an intersection between a line and a given surface. If the function returns true the data about the intersection (point, normal and texture coordinates) will be put to corresponding return variables.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cs.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cs.md#intersections)*

### Arguments

- *vec3* **p0** - Line start point coordinates (local).
- *vec3* **p1** - Line end point coordinates (local).
- *vec3[]* **ret_point** - Intersection point coordinates (object's local coordinate system). Pass NULL if this parameter is not required.
- *vec3[]* **OUT_ret_normal** - Coordinates of the normal vector to the intersection point. Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *vec4[]* **OUT_ret_texcoord** - Texture coordinates of the intersection point (vec4, where vec4.xy is for the first (0) UV channel, vec4.zw is for the second (1) UV channel). Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int[]* **ret_index** - Intersected triangle number. Pass NULL if this parameter is not required.
- *int[]* **OUT_ret_instance** - Intersected instance number. Pass NULL if this parameter is not required. > **Notice:** Intersected instance number can be obtained for the following classes: > - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cs.md)* > - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cs.md)* > - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cs.md)* > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **surface** - Surface number.

### Return value

true if there is an intersection with a given surface; otherwise, false.
## void SetIntersectionMask ( int mask , int surface )

Sets an intersection mask for a given surface.
### Arguments

- *int* **mask** - Surface intersection mask.
- *int* **surface** - Surface number.

## int GetIntersectionMask ( int surface )

Returns the intersection mask for a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface intersection mask.
## void SetPhysicsIntersection ( bool enabled , int surface )

Enables or disables physics intersections (between physical objects with bodies and collider shapes, or ray intersections with collider geometry) for a given surface.
### Arguments

- *bool* **enabled** - true to enable physics intersections with a given surface, false to disable them.
- *int* **surface** - Surface number.

## bool GetPhysicsIntersection ( int surface )

Returns a surface physics intersection flag. This flag indicates if physics intersections (between physical objects with bodies and collider shapes, or ray intersections with collider geometry) with a given surface are enabled.
### Arguments

- *int* **surface** - Surface number.

### Return value

true if intersections with a given surface are enabled; otherwise, false.
## void SetPhysicsIntersectionMask ( int mask , int surface )

Sets the [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for a surface with the specified number.
### Arguments

- *int* **mask** - Surface physics intersection mask.
- *int* **surface** - Surface number.

## int GetPhysicsIntersectionMask ( int surface )

Returns the [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for a surface with the specified number.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface physics intersection mask set for the specified surface.
## void SetShadowMask ( int mask , int surface )

Sets a shadow mask for a given surface.
For the shadow from an object's surface to be rendered for a light source, this mask must match the following ones (one bit, at least):

- [Shadow mask of the light source](../../../api/library/lights/class.light_cs.md#setShadowMask_int_void)
- [Shadow mask of the material](../../../api/library/rendering/class.material_cs.md#setShadowMask_int_void) assigned to this surface


### Arguments

- *int* **mask** - Surface shadow mask.
- *int* **surface** - Surface number.

## int GetShadowMask ( int surface )

Returns the shadow mask for a given surface.
For the shadow from an object's surface to be rendered for a light source, this mask must match the following ones (one bit, at least):

- [Shadow mask of the light source](../../../api/library/lights/class.light_cs.md#setShadowMask_int_void)
- [Shadow mask of the material](../../../api/library/rendering/class.material_cs.md#setShadowMask_int_void) assigned to this surface


### Arguments

- *int* **surface** - Surface number.

### Return value

Surface shadow mask.
## Material GetMaterial ( int surface )

Returns a material used for a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Material smart pointer.
## Material GetMaterialInherit ( int surface )

Inherits the surface material (i.e. creates a material instance). Modifications made to a new material instance will not affect the source material.
> **Notice:** A child material will be created only once, all subsequent calls to this method will return the first created child material.


### Arguments

- *int* **surface** - Surface number.

### Return value

Inherited material smart pointer.
## bool IsMaterialInherited ( int surface )

Returns the value indicating if a given surface material is inherited. Modifications made in a material instance do not affect the source material.
### Arguments

- *int* **surface** - Surface number.

### Return value

Positive number if the material is inherited; otherwise, **0**.
## void ClearMaterialInherit ( int surface )

Removes the inherited material and sets back the source(parent) material for the specified surface.
### Arguments

- *int* **surface** - Surface number.

## void SetMaterialParameterInt ( string name , int parameter , int surface )

Sets the value of a given integer parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Parameter name.
- *int* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## int GetMaterialParameterInt ( string name , int surface )

Returns the value of a given integer parameter of the surface material.
### Arguments

- *string* **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void SetMaterialParameterInt2 ( string name , ivec2 parameter , int surface )

Sets the value of a given [*ivec2*](../../../api/library/math/class.ivec2_cs.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Parameter name.
- *ivec2* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## ivec2 GetMaterialParameterInt2 ( string name , int surface )

Returns the value of a given [*ivec2*](../../../api/library/math/class.ivec2_cs.md) parameter of the surface material.
### Arguments

- *string* **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void SetMaterialParameterInt3 ( string name , ivec3 parameter , int surface )

Sets the value of a given [*ivec3*](../../../api/library/math/class.ivec3_cs.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Parameter name.
- *ivec3* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## ivec3 GetMaterialParameterInt3 ( string name , int surface )

Returns the value of a given [*ivec3*](../../../api/library/math/class.ivec3_cs.md) parameter of the surface material.
### Arguments

- *string* **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void SetMaterialParameterInt4 ( string name , ivec4 parameter , int surface )

Sets the value of a given [*ivec4*](../../../api/library/math/class.ivec4_cs.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Parameter name.
- *ivec4* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## ivec4 GetMaterialParameterInt4 ( string name , int surface )

Returns the value of a given [*ivec4*](../../../api/library/math/class.ivec4_cs.md) parameter of the surface material.
### Arguments

- *string* **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void SetMaterialParameterFloat ( string name , float parameter , int surface )

Sets the value of a given float parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Parameter name.
- *float* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## float GetMaterialParameterFloat ( string name , int surface )

Returns the value of a given float parameter of the surface material.
### Arguments

- *string* **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void SetMaterialParameterFloat2 ( string name , vec2 parameter , int surface )

Sets the value of a given [*vec2*](../../../api/library/math/class.vec2_cs.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Parameter name.
- *vec2* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## vec2 GetMaterialParameterFloat2 ( string name , int surface )

Returns the value of a given [*vec2*](../../../api/library/math/class.vec2_cs.md) parameter of the surface material.
### Arguments

- *string* **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void SetMaterialParameterFloat3 ( string name , vec3 parameter , int surface )

Sets the value of a given [*vec3*](../../../api/library/math/class.vec3_cs.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Parameter name.
- *vec3* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## vec3 GetMaterialParameterFloat3 ( string name , int surface )

Returns the value of a given [*vec3*](../../../api/library/math/class.vec3_cs.md) parameter of the surface material.
### Arguments

- *string* **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void SetMaterialParameterFloat4 ( string name , vec4 parameter , int surface )

Sets the value of a given [*vec4*](../../../api/library/math/class.vec4_cs.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Parameter name.
- *vec4* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## vec4 GetMaterialParameterFloat4 ( string name , int surface )

Returns the value of a given [*vec4*](../../../api/library/math/class.vec4_cs.md) parameter of the surface material.
### Arguments

- *string* **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void SetMaterialState ( string name , int state , int surface )

Sets the state value for a given surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Material state name.
- *int* **state** - State value.
- *int* **surface** - Surface number.

## int GetMaterialState ( string name , int surface )

Returns the state value of a given surface material.
### Arguments

- *string* **name** - Material state name.
- *int* **surface** - Surface number.

### Return value

State value.
## void SetMaterialTexture ( string name , string texture , int surface )

Sets the path to a given texture of a given surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Material texture name.
- *string* **texture** - Path to the texture file.
- *int* **surface** - Surface number.

## string GetMaterialTexture ( string name , int surface )

Returns the path to a given texture of a given surface material.
### Arguments

- *string* **name** - Material texture name.
- *int* **surface** - Surface number.

### Return value

Path to the texture file.
## void SetMinVisibleDistance ( float distance , int surface )

Updates the minimum visibility distance of a given surface. It is the distance, starting from which the surface begins to [fade in](#setMinFadeDistance_float_int_void) until it becomes completely visible.
### Arguments

- *float* **distance** - Minimum visibility distance, in units. If a negative value is provided, **0** will be used instead. The default value is -inf.
- *int* **surface** - Surface number.

## float GetMinVisibleDistance ( int surface )

Returns minimum visibility distance of a given surface. It is the distance, starting from which the surface begins to [fade in](#setMinFadeDistance_float_int_void) until it becomes completely visible.
### Arguments

- *int* **surface** - Surface number.

### Return value

Minimum visibility distance, in units.
## void SetExperimentalNavigation ( bool enabled , int surface )

Sets a value indicating if a given surface contributes to the walkable surface when an [ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cs.md) is baked. Marking geometry is opt-in: a surface takes part in baking only when this flag is set, which keeps decoration and clutter out of the navigation mesh.
### Arguments

- *bool* **enabled** - Navigation flag. The default value is false.
- *int* **surface** - Surface number.

## bool GetExperimentalNavigation ( int surface )

Returns a value indicating if a given surface contributes to the walkable surface when a navigation mesh is baked.
### Arguments

- *int* **surface** - Surface number.

### Return value

true if the surface takes part in navigation mesh baking; otherwise, false.
## void SetExperimentalNavigationBakeMask ( int mask , int surface )

Sets the bake mask of a given surface. The surface is taken in only by the navigation meshes whose own bake mask shares at least one bit with this one, which is how one scene feeds several navigation meshes with different geometry.
### Arguments

- *int* **mask** - [Bake mask](../../../principles/bit_masking/index.md#bake_mask). The default value is 1.
- *int* **surface** - Surface number.

## int GetExperimentalNavigationBakeMask ( int surface )

Returns the bake mask of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Bake mask of the surface.
## void SetExperimentalNavigationArea ( int area , int surface )

Sets the area stamped onto the navigation mesh polygons baked from a given surface. It is how a road, a patch of mud, or a metal walkway gets its own traversal cost without a volume being placed over it.
### Arguments

- *int* **area** - Area index from the registry of the [ExperimentalNavigation](../../../api/library/pathfinding/class.experimentalnavigation_cs.md) singleton. The default value is 63.
- *int* **surface** - Surface number.

## int GetExperimentalNavigationArea ( int surface )

Returns the area stamped onto the navigation mesh polygons baked from a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Area index of the surface.
## void SetMaxVisibleDistance ( float distance , int surface )

Updates the maximum visibility distance of a given surface. It is the distance, starting from which the surface begins to [fade out](#setMaxFadeDistance_float_int_void) until it becomes completely invisible.
### Arguments

- *float* **distance** - Maximum visibility distance, in units. If a negative value is provided, **0** will be used instead. The default value is inf.
- *int* **surface** - Surface number.

## float GetMaxVisibleDistance ( int surface )

Returns the maximum visibility distance of a given surface. It is the distance, starting from which the surface begins to [fade out](#getMaxFadeDistance_int_float) until it becomes completely invisible.
### Arguments

- *int* **surface** - Surface number.

### Return value

Maximum visibility distance, in units.
## void SetMinFadeDistance ( float distance , int surface )

Updates the minimum fade-in distance of a given surface. Over this distance the surface smoothly becomes visible due to [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [minimum visibility distance](#getMinVisibleDistance_int_float).
### Arguments

- *float* **distance** - Minimum fade-in distance, in units. If a negative value is provided, **0** will be used instead. The default value is 0.
- *int* **surface** - Surface number.

## float GetMinFadeDistance ( int surface )

Returns the minimum fade-in distance of a given surface. Over this distance the surface smoothly becomes visible due to [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [minimum visibility distance](#getMinVisibleDistance_int_float).
### Arguments

- *int* **surface** - Surface number.

### Return value

Minimum fade-in distance, in units.
## void SetMaxFadeDistance ( float distance , int surface )

Updates the maximum fade-out distance of a given surface. Over this distance the surface smoothly becomes invisible due to [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted off starting from the [maximum visibility distance](#getMaxVisibleDistance_int_float).
### Arguments

- *float* **distance** - Maximum fade-out distance, in units. If a negative value is provided, **0** will be used instead. The default value is 0.
- *int* **surface** - Surface number.

## float GetMaxFadeDistance ( int surface )

Returns the maximum fade-out distance. Over this distance the surface smoothly becomes invisible due to [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [maximum visibility distance](#getMaxVisibleDistance_int_float).
### Arguments

- *int* **surface** - Surface number.

### Return value

Maximum fade-out distance, in units.
## void SetMinParent ( int parent , int surface )

Sets surface minimum LOD parent surface number.
### Arguments

- *int* **parent** - Number of hierarchy levels. If a negative value is provided, **0** will be used instead.
- *int* **surface** - Surface number.

## int GetMinParent ( int surface )

Returns the surface minimum LOD parent surface number.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface minimum LOD parent surface number.
## void SetMaxParent ( int parent , int surface )

Sets a surface maximum LOD parent surface number.
### Arguments

- *int* **parent** - Number of hierarchy levels. If a negative value is provided, **0** will be used instead.
- *int* **surface** - Surface number.

## int GetMaxParent ( int surface )

Returns the surface maximum LOD parent surface number.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface maximum LOD parent surface number.
## int GetNumTriangles ( int surface )

Returns the number of triangles comprising a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Number of triangles.
## void SetParent ( int parent , int surface )

Sets or clears the parent surface for a given surface.
### Arguments

- *int* **parent** - Number of the parent surface or **-1** to clear the parent.
- *int* **surface** - Surface number.

## int GetParent ( int surface )

Returns the number of the parent surface for a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Parent surface number. If -1 is returned, the parent surface is not specified for a given surface.
## int SetSurfaceProperty ( string name , string pattern )

Sets a new property for a given surface.
### Arguments

- *string* **name** - Name of the new property.
- *string* **pattern** - Pattern (string with a [regular expression](../../../api/library/common/class.regexp_cs.md#intro)), against which surface names will be matched.

### Return value

1 if the property is set successfully; otherwise, 0.
## int SetSurfaceProperty ( string name , int surface )

Sets a new property for the specified surface.
### Arguments

- *string* **name** - Name of the new property.
- *int* **surface** - Surface number.

### Return value

1 if the property is set successfully; otherwise, 0.
## int SetSurfaceProperty ( UGUID guid , int surface )

Sets a new property for the specified surface.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Property [GUID](../../../api/library/filesystem/class.uguid_cs.md).
- *int* **surface** - Surface number.

### Return value

1 if the property is set successfully; otherwise, 0.
## int SetSurfaceProperty ( UGUID guid , string pattern )

Sets a new property for the specified surface(s).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Property [GUID](../../../api/library/filesystem/class.uguid_cs.md).
- *string* **pattern** - Pattern (string with a [regular expression](../../../api/library/common/class.regexp_cs.md#intro)), against which surface names will be matched.

### Return value

1 if the property is set successfully; otherwise, 0.
## int SetSurfaceProperty ( Property property , int surface )

Sets a new property for the specified surface.
### Arguments

- *[Property](../../../api/library/common/class.property_cs.md)* **property** - Property to be set for the surface.
- *int* **surface** - Surface number.

### Return value

1 if the property is set successfully; otherwise, 0.
## int SetSurfaceProperty ( Property property , string pattern )

Sets a new property for the specified surface(s).
### Arguments

- *[Property](../../../api/library/common/class.property_cs.md)* **property** - Property to be set for the surface.
- *string* **pattern** - Pattern (string with a [regular expression](../../../api/library/common/class.regexp_cs.md#intro)), against which surface names will be matched.

### Return value

1 if the property is set successfully; otherwise, 0.
## Property GetSurfaceProperty ( int surface )

Returns the property smart pointer.
### Arguments

- *int* **surface** - Surface number.

### Return value

Property used for the surface.
## Property GetSurfacePropertyInherit ( int surface )

Inherits the property for the specific object. All changes of the inherited property will not affect the reference one.
### Arguments

- *int* **surface** - Surface number.

### Return value

Inherited property smart pointer.
## void ClearSurfaceProperty ( int surface )

Removes the assigned property from the specified surface.
### Arguments

- *int* **surface** - Surface number.

## void ClearSurfacePropertyInherit ( int surface )

Removes the inherited property and sets back the source(parent) property for the specified surface.
### Arguments

- *int* **surface** - Surface number.

## bool IsSurfacePropertyInherited ( int surface )

Returns a value indicating if a given property is inherited.
### Arguments

- *int* **surface** - Surface number.

### Return value

Positive number if the surface property is inherited; otherwise, **0**.
## string GetSurfacePropertyName ( int surface )

Returns the name of the property of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Property name.
## string GetSurfaceName ( int surface )

Returns the name of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface name.
## void SetViewportMask ( int mask , int surface )

Sets a [viewport mask](../../../principles/bit_masking/index.md#viewport) for a given surface. The object surface is rendered, if its mask matches the player (camera) and material masks.
```csharp
// hide the first surface from the camera by disabling all the bits of the mask
obj.SetViewportMask(0, 0);

// restore visibility of the surface (the camera must have the first bit of the Viewport mask enabled)
obj.SetViewportMask(1, 0);

// enable all the bits by using bitwise NOT
obj.SetViewportMask(~0, 0);

// enable ONLY the fifth bit of the mask
obj.SetViewportMask(1 << 4, 0);


```


### Arguments

- *int* **mask** - Surface viewport mask.
- *int* **surface** - Surface number.

## int GetViewportMask ( int surface )

Returns a viewport mask for a given surface. The object surface is rendered, if its mask matches the player (camera) and material masks.
```csharp
// get the viewport mask of the first surface
int mask = obj.GetViewportMask(0);

// check if the fifth bit is set
bool isBitSet = (mask >> 4 & 1) != 0;

// check if masks match
bool doMasksMatch = (mask & mask2) != 0;


```


### Arguments

- *int* **surface** - Surface number.

### Return value

Surface viewport mask.
## WorldBoundBox GetWorldBoundBox ( int surface )

Returns the world bounding box of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Bounding box (in world coordinates).
## WorldBoundSphere GetWorldBoundSphere ( int surface )

Returns the world bounding sphere of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Bounding sphere (in world coordinates).
## int FindSurface ( string name )

Searches for a surface with a given name.
### Arguments

- *string* **name** - Surface name.

### Return value

Surface number if it exists; otherwise, -1.
## void FlushBodyTransform ( )

Forces to set the transformations of the body for the node.
## void Render ( Render.PASS pass , int surface )


Renders raw object's surface to texture in specified pass.


> **Notice:** All [camera parameters](../../../code/uusl/parameters.md#camera_parameters) should be set manually.


**Usage Example**


```csharp
texture_render.BindColorTexture(0, texture);
texture_render.Enable();
Object.Render(Render.PASS.AMBIENT, 0);
texture_render.Disable();
texture_render.UnbindColorTexture(0);


```


### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - A [rendering pass](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME).
- *int* **surface** - Surface number.

## void SetSoundOcclusion ( float occlusion , int surface )

Sets a new sound occlusion value for the specified surface of the object, that determines how much it affects sounds in case of occlusion. For a sound source to be occluded by the specified surface, at least one bit of its [occlusion mask](#setSoundOcclusionMask_int_int_void) should match the [occlusion mask of the sound source](../../../api/library/sounds/class.soundsource_cs.md#setOcclusionMask_int_void).
> **Notice:** [Sound occlusion](../../../api/library/engine/class.sound_cs.md#setSourceOcclusion_int_void) must be enabled.


### Arguments

- *float* **occlusion** - Occlusion value in the range **[0.0f, 1.0f]** to be set for the specified surface. The default value is 0.0f.

  - 0.0f - no occlusion, sound volume will stay the same in case of occlusion by the surface.
  - 1.0f - maximum occlusion, sound will not be heard at all in case of occlusion by the surface.
- *int* **surface** - Surface number.

## float GetSoundOcclusion ( int surface )

Returns the current sound occlusion value for the specified surface of the object, that determines how much it affects sounds in case of occlusion. For a sound source to be occluded by the specified surface, at least one bit of its [occlusion mask](#setSoundOcclusionMask_int_int_void) should match the [occlusion mask of the sound source](../../../api/library/sounds/class.soundsource_cs.md#setOcclusionMask_int_void).
> **Notice:** [Sound occlusion](../../../api/library/engine/class.sound_cs.md#setSourceOcclusion_int_void) must be enabled.


### Arguments

- *int* **surface** - Surface number.

### Return value

Current occlusion value in the range **[0.0f, 1.0f]** set for the specified surface.
- 0.0f - no occlusion, sound volume will stay the same in case of occlusion by the surface.
- 1.0f - maximum occlusion, sound will not be heard at all in case of occlusion by the surface.

The default value is 0.0f.
## void SetSoundOcclusionMask ( int mask , int surface )

Sets a new sound occlusion mask for the specified surface of the object. For a sound source to be occluded by the specified surface, at least one bit of this mask should match the [occlusion mask of the sound source](../../../api/library/sounds/class.soundsource_cs.md#setOcclusionMask_int_void). Each surface has its own [occlusion value](#setSoundOcclusion_float_int_void), that determines how much it affects sounds in case of occlusion.
> **Notice:** [Sound occlusion](../../../api/library/engine/class.sound_cs.md#setSourceOcclusion_int_void) must be enabled.


### Arguments

- *int* **mask** - Integer, each bit of which is a mask for sound source occlusion.
- *int* **surface** - Surface number.

## int GetSoundOcclusionMask ( int surface )

Returns sound occlusion mask for the specified surface of the object. For a sound source to be occluded by the specified surface, at least one bit of this mask should match the [occlusion mask of the sound source](../../../api/library/sounds/class.soundsource_cs.md#setOcclusionMask_int_void). Each surface has its own [occlusion value](#setSoundOcclusion_float_int_void), that determines how much it affects sounds in case of occlusion.
> **Notice:** [Sound occlusion](../../../api/library/engine/class.sound_cs.md#setSourceOcclusion_int_void) must be enabled.


### Arguments

- *int* **surface** - Surface number.

### Return value

Integer, each bit of which is a mask for sound source occlusion.
## void SetPhysicsFriction ( float value , int surface )

Sets the coefficient of friction for the specified surface. This coefficient allows to model more rough rubbing of surfaces and is opposite to the body's movement direction. Friction parameter values of both surfaces being in contact are considered. The resulting calculated friction depends on the objects' masses and gravity, and the angle between contacting surfaces.
- The *higher* the value, the less tendency the body has to slide.

Friction is calculated by the contact between physical bodies.
### Arguments

- *float* **value** - Friction coefficient value in the range **[0.0f, 1.0f]** to be set for the specified surface.
- *int* **surface** - Surface number.

## float GetPhysicsFriction ( int surface )

Returns the current coefficient of friction for the specified surface. This coefficient allows to model more rough rubbing of surfaces and is opposite to the body's movement direction. Friction parameter values of both surfaces being in contact are considered. The resulting calculated friction depends on the objects' masses and gravity, and the angle between contacting surfaces.
- The *higher* the value, the less tendency the body has to slide.

Friction is calculated by the contact between physical bodies.
### Arguments

- *int* **surface** - Surface number.

### Return value

Current friction coefficient value in the range **[0.0f, 1.0f]** set for the specified surface.
## void SetPhysicsRestitution ( float value , int surface )

Sets the coefficient of restitution for the specified surface. This coefficient determines the degree of relative kinetic energy retained after a collision. It defines how bouncy the object is by contacting with another object. It depends on the elasticity of the materials of colliding bodies. The simulated restitution, like [friction](#setPhysicsFriction_float_int_void), considers the total value for both objects being in contact.
- The maximum value of 1.0f models elastic collision. Objects bounce off according to the impulse they get by contact.
- The minimum value of 0.0f models inelastic collision. Objects do not bounce at all.

Restitution is calculated by the contact between physical bodies.
### Arguments

- *float* **value** - Restitution coefficient value in the range **[0.0f, 1.0f]** to be set for the specified surface.
- *int* **surface** - Surface number.

## float GetPhysicsRestitution ( int surface )

Returns the current coefficient of restitution for the specified surface. This coefficient determines the degree of relative kinetic energy retained after a collision. It defines how bouncy the object is by contacting with another object. It depends on the elasticity of the materials of colliding bodies. The simulated restitution, like [friction](#setPhysicsFriction_float_int_void), considers the total value for both objects being in contact.
- The maximum value of 1.0f models elastic collision. Objects bounce off according to the impulse they get by contact.
- The minimum value of 0.0f models inelastic collision. Objects do not bounce at all.

Restitution is calculated by the contact between physical bodies.
### Arguments

- *int* **surface** - Surface number.

### Return value

Current restitution coefficient value in the range **[0.0f, 1.0f]** set for the specified surface.
## void SetShadowMode ( Object.SURFACE_SHADOW_MODE mode , int surface )

Sets the shadow mode for the specified surface. To cast a shadow from a light source (Omni, Proj, or World), the surface's shadow mode should be [adjusted](../../../content/optimization/lights/index.md#static_light) in accordance with the [shadow mode of the light source](../../../api/library/lights/class.light_cs.md#setShadowMode_int_void).
### Arguments

- *[Object.SURFACE_SHADOW_MODE](../../../api/library/objects/class.object_cs.md#SURFACE_SHADOW_MODE)* **mode** - Surface shadow mode to be set, one of the following:

  - [SURFACE_SHADOW_MODE_DYNAMIC](#SURFACE_SHADOW_MODE_DYNAMIC)
  - [SURFACE_SHADOW_MODE_MIXED](#SURFACE_SHADOW_MODE_MIXED)
- *int* **surface** - Target surface number.

## Object.SURFACE_SHADOW_MODE GetShadowMode ( int surface )

Returns the shadow mode set for the specified surface. To cast a shadow from a light source (Omni, Proj, or World), the surface's shadow mode should be [adjusted](../../../content/optimization/lights/index.md#static_light) in accordance with the [shadow mode of the light source](../../../api/library/lights/class.light_cs.md#setShadowMode_int_void).
### Arguments

- *int* **surface** - Target surface number.

### Return value

Surface shadow mode, one of the following:
- [SURFACE_SHADOW_MODE_DYNAMIC](#SURFACE_SHADOW_MODE_DYNAMIC)
- [SURFACE_SHADOW_MODE_MIXED](#SURFACE_SHADOW_MODE_MIXED)


## UGUID GetLostMaterialGUID ( int surface )

Returns the [GUID](../../../api/library/filesystem/class.uguid_cs.md) of a lost material. If for some reason a material assigned to the specified surface is missing, this method can be used to get it's GUID.
### Arguments

- *int* **surface** - Target surface number.

### Return value

Lost material [GUID](../../../api/library/filesystem/class.uguid_cs.md).
## UGUID GetLostSurfacePropertyGUID ( int surface )

Returns the [GUID](../../../api/library/filesystem/class.uguid_cs.md) of a lost surface property. If for some reason a property assigned to the specified surface is missing, this method can be used to get it's GUID.
### Arguments

- *int* **surface** - Target surface number.

### Return value

Lost property [GUID](../../../api/library/filesystem/class.uguid_cs.md).
## void SetLightingMode ( Object.SURFACE_LIGHTING_MODE mode , int surface )

Sets the lighting mode for the specified surface.
### Arguments

- *[Object.SURFACE_LIGHTING_MODE](../../../api/library/objects/class.object_cs.md#SURFACE_LIGHTING_MODE)* **mode** - Surface lighting mode to be set, one of the following:

  - [STATIC](#SURFACE_LIGHTING_MODE_STATIC)
  - [DYNAMIC](#SURFACE_LIGHTING_MODE_DYNAMIC)
  - [ADVANCED](#SURFACE_LIGHTING_MODE_ADVANCED)
- *int* **surface** - Target surface number.

## Object.SURFACE_LIGHTING_MODE GetLightingMode ( int surface )

Returns the lighting mode for the specified surface.
### Arguments

- *int* **surface** - Target surface number.

### Return value

Surface lighting mode, one of the following:
- [STATIC](#SURFACE_LIGHTING_MODE_STATIC)
- [DYNAMIC](#SURFACE_LIGHTING_MODE_DYNAMIC)
- [ADVANCED](#SURFACE_LIGHTING_MODE_ADVANCED)


## void SetMaterialFilePath ( string path , int surface )

Sets the material by file path to a given surface.
### Arguments

- *string* **path** - Material file path.
- *int* **surface** - Target surface number.

## void SetMaterialFilePath ( string path , string pattern )

Sets the material by file path to given surfaces.
### Arguments

- *string* **path** - Material file path.
- *string* **pattern** - Pattern (string with a [regular expression](../../../api/library/common/class.regexp_cs.md#intro)), against which surface names will be matched.

## string GetMaterialFilePath ( int surface )

Returns the file path for the material assigned to a given surface.
### Arguments

- *int* **surface** - Target surface number.

### Return value

Material file path.
## void SetMaterialGUID ( UGUID guid , int surface )

Sets a new material with a given [GUID](../../../api/library/filesystem/class.uguid_cs.md) to the specified surface.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Material [GUID](../../../api/library/filesystem/class.uguid_cs.md).
- *int* **surface** - Target surface number.

## void SetMaterialGUID ( UGUID guid , string pattern )

Sets a new material with a given [GUID](../../../api/library/filesystem/class.uguid_cs.md) to the specified surface.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Material [GUID](../../../api/library/filesystem/class.uguid_cs.md).
- *string* **pattern** - Pattern (string with a [regular expression](../../../api/library/common/class.regexp_cs.md#intro)), against which surface names will be matched.

## UGUID GetMaterialGUID ( int surface )

Returns a [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the material for the specified surface.
### Arguments

- *int* **surface** - Target surface number.

### Return value

Material [GUID](../../../api/library/filesystem/class.uguid_cs.md).
## void SetMaterial ( Material mat , int surface )

Sets a new material for the specified surface.
### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **mat** - Material instance.
- *int* **surface** - Surface number.

## void SetMaterial ( Material mat , string pattern )

Sets a new material for the specified surface.
### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **mat** - Material instance.
- *string* **pattern** - Pattern (string with a [regular expression](../../../api/library/common/class.regexp_cs.md#intro)), against which surface names will be matched.

## int GetSurfaceStatDrawCalls ( int surface )

Returns the number of draw calls (DIP) for the surface with the specified number during the last frame.
### Arguments

- *int* **surface** - Surface number.

### Return value

Number of draw calls (DIP) for the specified surface during the last frame.
## int GetSurfaceStatDrawCountViewport ( int surface )

Returns the number of times the surface with the specified number was drawn in the viewport last frame.
### Arguments

- *int* **surface** - Surface number.

### Return value

Number of times the specified surface was drawn in the viewport last frame.
## int GetSurfaceStatDrawCountReflection ( int surface )

Returns the number of times the surface with the specified index was drawn during reflections rendering in the last frame.
### Arguments

- *int* **surface** - Surface number.

### Return value

Number of times the specified surface was drawn during reflections rendering in the last frame.
## int GetSurfaceStatDrawCountShadow ( int surface )

Returns the number of times the surface with the specified index was drawn during shadows rendering in the last frame.
```csharp
ObjectMeshStatic mesh;
int total_draw_count_shadows = 0;

// event handler function calculating the total number of times the surfaces of a Static Mesh were drawn

void endscreen_event_handler()
{
	total_draw_count_shadows = 0;

	for (int surf = 0; surf < mesh.NumSurfaces; surf++)
	{
		if (mesh.GetSurfaceStatFrame(surf) == Engine.Frame)
		{
			// This surface was rendered during the current frame, so the info is up-to date
			total_draw_count_shadows += mesh.GetSurfaceStatDrawCountShadow(surf);
		}
	}
}

// create an instance of the EventConnections class
EventConnections endscreen_event_connections = new EventConnections();

void Init()
{

	// subscribe to the EndScreen event with a handler function keeping the connection
	Render.EventEndScreen.Connect(endscreen_event_connections, endscreen_event_handler);
}


```


### Arguments

- *int* **surface** - Surface number.

### Return value

Number of times the specified surface was drawn during shadows rendering in the last frame.
## long GetSurfaceStatFrame ( int surface )

Returns the number of [Engine frame](../../../api/library/engine/class.engine_cs.md#getFrame_int64_t), in which the surface with the specified number was drawn last time.
### Arguments

- *int* **surface** - Surface number.

### Return value

Number of frame, in which the specified surface was drawn last time.
## float GetSurfaceRenderCustomParameterFloat ( int surface , string name )

Returns the current value of the custom surface parameter with the given name for the given surface of the object. If the parameter is not overridden for the surface, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **surface** - Surface number.
- *string* **name** - Parameter name.

### Return value

Current parameter value, or 0 if no parameter with this name exists.
## float GetSurfaceRenderCustomParameterFloat ( int surface , int param )

Returns the current value of the custom surface parameter with the given number for the given surface of the object. If the parameter is not overridden for the surface, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.

### Return value

Current parameter value.
## int GetSurfaceRenderCustomParameterInt ( int surface , string name )

Returns the current value of the custom surface parameter with the given name for the given surface of the object. If the parameter is not overridden for the surface, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **surface** - Surface number.
- *string* **name** - Parameter name.

### Return value

Current parameter value, or 0 if no parameter with this name exists.
## int GetSurfaceRenderCustomParameterInt ( int surface , int param )

Returns the current value of the custom surface parameter with the given number for the given surface of the object. If the parameter is not overridden for the surface, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.

### Return value

Current parameter value.
## uint GetSurfaceRenderCustomParameterUInt ( int surface , string name )

Returns the current value of the custom surface parameter with the given name for the given surface of the object. If the parameter is not overridden for the surface, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **surface** - Surface number.
- *string* **name** - Parameter name.

### Return value

Current parameter value, or 0 if no parameter with this name exists.
## uint GetSurfaceRenderCustomParameterUInt ( int surface , int param )

Returns the current value of the custom surface parameter with the given number for the given surface of the object. If the parameter is not overridden for the surface, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.

### Return value

Current parameter value.
## bool IsSurfaceRenderCustomParameterOverridden ( int surface , int param )

Checks if the custom surface parameter with the given number is overridden for the given surface of the object.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.

### Return value

true if the parameter is overridden for the surface; otherwise, false.
## void ResetSurfaceRenderCustomParameter ( int surface , int param )

Resets the override of the custom surface parameter with the given number for the given surface: the surface uses the default value from the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)* again.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.

## void ResetSurfaceRenderCustomParameters ( int surface )

Resets the overrides of all custom surface parameters for the given surface of the object.
### Arguments

- *int* **surface** - Surface number.

## void SetSurfaceRenderCustomParameterFloat ( int surface , string name , float value )

Sets a new value of the custom surface parameter with the given name for the given surface of the object. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)*. If no parameter with this name exists in the layout, the method does nothing.
### Arguments

- *int* **surface** - Surface number.
- *string* **name** - Parameter name.
- *float* **value** - New parameter value.

## void SetSurfaceRenderCustomParameterFloat ( int surface , int param , float value )

Sets a new value of the custom surface parameter with the given number for the given surface of the object. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)*.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.
- *float* **value** - New parameter value.

## void SetSurfaceRenderCustomParameterInt ( int surface , string name , int value )

Sets a new value of the custom surface parameter with the given name for the given surface of the object. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)*. If no parameter with this name exists in the layout, the method does nothing.
### Arguments

- *int* **surface** - Surface number.
- *string* **name** - Parameter name.
- *int* **value** - New parameter value.

## void SetSurfaceRenderCustomParameterInt ( int surface , int param , int value )

Sets a new value of the custom surface parameter with the given number for the given surface of the object. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)*.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.
- *int* **value** - New parameter value.

## void SetSurfaceRenderCustomParameterUInt ( int surface , string name , uint value )

Sets a new value of the custom surface parameter with the given name for the given surface of the object. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)*. If no parameter with this name exists in the layout, the method does nothing.
### Arguments

- *int* **surface** - Surface number.
- *string* **name** - Parameter name.
- *uint* **value** - New parameter value.

## void SetSurfaceRenderCustomParameterUInt ( int surface , int param , uint value )

Sets a new value of the custom surface parameter with the given number for the given surface of the object. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cs.md#getSurfaceParameters_CustomParameterLayout)*.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.
- *uint* **value** - New parameter value.
