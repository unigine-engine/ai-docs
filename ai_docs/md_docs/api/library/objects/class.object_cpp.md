# Object Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Node


An [object](../../../objects/index.md) with a set of [surfaces](../../../principles/world_structure/index.md#surfaces) to represent geometry. Rendering materials are [assigned](#setMaterial_Material_int_void) per object surface. An object can be assigned a [physical body](#setBody_Body_int_int).


## Object Class

### Enums

## SURFACE_SHADOW_MODE

| Name | Description |
|---|---|
| **SURFACE_SHADOW_MODE_MIXED** = 0 | Mode to cast shadows from both static and dynamic light sources. |
| **SURFACE_SHADOW_MODE_DYNAMIC** = 1 | Mode to cast shadows only if the surface is lit by a dynamic light source. |

## SURFACE_LIGHTING_MODE

| Name | Description |
|---|---|
| **SURFACE_LIGHTING_MODE_STATIC** = 0 | Optimized for use in static GI, static reflections and cached shadows. |
| **SURFACE_LIGHTING_MODE_DYNAMIC** = 1 | Excludes the surface from use in static GI and static reflections and is suitable for dynamic shadows. |
| **SURFACE_LIGHTING_MODE_ADVANCED** = 2 | Enables manual adjustment of all lighting-related settings. |

### Members

## int getNumSurfaces () const

Returns the current number of surfaces of the object.
> **Notice:** For your convenience, *[ObjectMeshDynamic::create()](../../../api/library/objects/class.objectmeshdynamic_cpp.md#ObjectMeshDynamic_constPtrMesh_int)* initializes the object with one internal surface named "`dynamic`". The first call to *[addSurface()](../../../api/library/objects/class.objectmeshdynamic_cpp.md#addSurface_cstr_void)* simply assigns a user-defined name to this surface without changing the total surface count. To create additional surfaces, call *[addSurface()](../../../api/library/objects/class.objectmeshdynamic_cpp.md#addSurface_cstr_void)* again.


### Return value

Current number of surfaces of the object
## void setEnabled ( bool enabled )

Sets a new value indicating if the node and its parent nodes are enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable node; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if the node and its parent nodes are enabled.
### Return value

**true** if node is enabled ; otherwise **false**.
## Ptr < BodyRigid > getBodyRigid () const

Returns the current rigid body assigned to the object.
### Return value

Current rigid body assigned to the object
## void setBody ( const Ptr < Body >& body )

Sets a new physical body assigned to the object, or **NULL** (**0**) if no body is assigned.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)>&* **body** - The physical body assigned to the object

## Ptr < Body > getBody () const

Returns the current physical body assigned to the object, or **NULL** (**0**) if no body is assigned.
### Return value

Current physical body assigned to the object
## bool isVisibleShadow () const

Returns the current value indicating if the object's shadow is rendered.
### Return value

**true** if the object's shadow is rendered; otherwise **false**.
## bool isVisibleCamera () const

Returns the current value indicating if the object is rendered.
### Return value

**true** if the object is rendered; otherwise **false**.
---

## bool setBody ( const Ptr < Body > & body , bool update = 1 )

Assigns a physical body to the object.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body** - Physical body to be assigned to the object.
- *bool* **update** - Update flag. Set this flag to update the object after assigning the specified body to it.

### Return value

true if the specified body is set successfully; otherwise, false.
## Math:: BoundBox getBoundBox ( int surface ) const

Returns the bounding box of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Bounding box.
## Math:: BoundSphere getBoundSphere ( int surface ) const

Returns the bounding sphere of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Bounding sphere.
## void setBakeToEnvProbe ( bool enabled , int surface )

Sets a value indicating if the specified surface is to be baked to environment probes.
### Arguments

- *bool* **enabled** - **1** to enable baking of the specified surface to environment probes, **0** - to disable it.
- *int* **surface** - Surface number.

## bool getBakeToEnvProbe ( int surface ) const

Returns a value indicating if the specified surface is to be baked to environment probes.
### Arguments

- *int* **surface** - Surface number.

### Return value

true if the specified surface is to be baked to environment probes; otherwise, false.
## void setBakeToGI ( bool enabled , int surface )

Sets a value indicating if the specified surface is to be baked to GI (voxel probes and lightmaps).
### Arguments

- *bool* **enabled** - **1** to enable baking of the specified surface to GI, **0** - to disable it.
- *int* **surface** - Surface number.

## bool getBakeToGI ( int surface ) const

Returns a value indicating if the specified surface is to be baked to GI (voxel probes and lightmaps).
### Arguments

- *int* **surface** - Surface number.

### Return value

**1** if the specified surface is to be baked to GI; otherwise, **0**.
## void setCastEnvProbeShadow ( bool enabled , int surface )

Enables or disables casting shadows from environment probes by the specified surface.
### Arguments

- *bool* **enabled** - **1** to enable casting shadows from environment probes by the specified surface, **0** to disable it.
- *int* **surface** - Surface number.

## bool getCastEnvProbeShadow ( int surface ) const

Returns a value indicating if casting shadows from environment probes by the specified surface is enabled.
### Arguments

- *int* **surface** - Surface number.

### Return value

**1** if casting shadows from environment probes by the specified surface is enabled; otherwise, **0**.
## void setCastShadow ( bool enabled , int surface )

Enables or disables casting shadows from non-world lights for a given surface.
### Arguments

- *bool* **enabled** - **1** if shadows are to be cast by a given surface; otherwise, **0**.
- *int* **surface** - Surface number.

## bool getCastShadow ( int surface ) const

Returns the surface cast shadow flag, which indicates if a given surface should cast shadows from non-world lights.
### Arguments

- *int* **surface** - Surface number.

### Return value

Positive number if shadows are cast by a given surface; otherwise, **0**.
## void setCastWorldShadow ( bool enabled , int surface )

Enables or disables casting shadows from world lights for a given surface.
### Arguments

- *bool* **enabled** - true if world shadows are to be cast by a given surface; otherwise, false.
- *int* **surface** - Surface number.

## bool getCastWorldShadow ( int surface ) const

Returns the surface cast world shadow flag, which indicates if a given surface should cast shadows from world lights.
### Arguments

- *int* **surface** - Surface number.

### Return value

Positive number if world shadows are cast by a given surface; otherwise, **0**.
## void setCollision ( bool enabled , int surface )

Enables or disables [collision detection](../../../principles/physics/collision/index.md) for a given surface.
### Arguments

- *bool* **enabled** - **1** if collision detection is enabled for a given surface; otherwise, **0**.
- *int* **surface** - Surface number.

## bool getCollision ( int surface ) const

Returns the surface collision flag, which indicates if [collision detection](../../../principles/physics/collision/index.md) for a given surface is enabled.
### Arguments

- *int* **surface** - Surface number.

### Return value

Positive number if collision detection is enabled for a given surface; otherwise, **0**.
## void setCollisionMask ( int mask , int surface )

Sets a collision mask for a given surface. Two objects collide, if they both have matching masks.
### Arguments

- *int* **mask** - Surface collision mask.
- *int* **surface** - Surface number.

## int getCollisionMask ( int surface ) const

Returns the collision mask for a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface collision mask.
## void setEnabled ( bool enabled , int surface )

Enables or disables a surface with the specified number. The disabled surface is not rendered, does not take part in collision detection, and does not cast shadows.
```cpp
// temporarily disable the first surface of the object (index 0)
obj->setEnabled(false, 0);	// (enable/disable, surface index)

//...

// enable the first surface again if it is disabled
if(!obj->isEnabled(0))
	obj->setEnabled(true, 0);

```


### Arguments

- *bool* **enabled** - true to enable the surface, false to disable it.
- *int* **surface** - Surface number.

## bool isEnabled ( int surface ) const

Returns a value indicating if a given surface is enabled.
```cpp
// temporarily disable the first surface of the object (index 0)
obj->setEnabled(false, 0);	// (enable/disable, surface index)

//...

// enable the first surface again if it is disabled
if(!obj->isEnabled(0))
	obj->setEnabled(true, 0);

```


### Arguments

- *int* **surface** - Surface number.

### Return value

true if the surface is enabled; otherwise, false.
## void setIntersection ( bool enabled , int surface )

Enables or disables intersections with a given surface.
### Arguments

- *bool* **enabled** - true to enable intersections with a given surface, false to disable them.
- *int* **surface** - Surface number.

## bool getIntersection ( const Math::Vec3& p0 , const Math::Vec3& p1 , const Ptr < ObjectIntersectionTexCoord > & v , int surface ) const

Checks if there is an intersection between a line and a given surface. If the function returns true the data about the texture coordinates of the intersection point will be put to [ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_cpp.md) object.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cpp.md#intersections)*


### Arguments

- *const  Math::Vec3&* **p0** - Line start point coordinates (local).
- *const  Math::Vec3&* **p1** - Line end point coordinates (local).
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_cpp.md)> &* **v** - [ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_cpp.md) class instance to store corresponding intersection data.
- *int* **surface** - Surface number.

### Return value

true if there is an intersection with a given surface; otherwise, false.
## bool getIntersection ( int surface ) const

Returns a surface intersection flag. This flag indicates if intersections with a given surface are enabled.
### Arguments

- *int* **surface** - Surface number.

### Return value

true if intersections with a given surface are enabled; otherwise, false.
## bool getIntersection ( const Math::Vec3& p0 , const Math::Vec3& p1 , const Ptr < ObjectIntersectionNormal > & v , int surface ) const

Checks if there is an intersection between a line and a given surface. If the function returns true the data about the normal at the intersection point will be put to [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_cpp.md) object.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cpp.md#intersections)*

### Arguments

- *const  Math::Vec3&* **p0** - Line start point coordinates (local).
- *const  Math::Vec3&* **p1** - Line end point coordinates (local).
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_cpp.md)> &* **v** - [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_cpp.md) class instance to store corresponding intersection data.
- *int* **surface** - Surface number.

### Return value

true if there is an intersection with a given surface; otherwise, false.
## bool getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int mask , const Ptr < ObjectIntersection > & v , int * ret_surface ) const

Checks if there is an intersection between a line and a surface with a given intersection mask. If the function returns true the data about the intersection point will be put to [ObjectIntersection](../../../api/library/objects/class.objectintersection_cpp.md) object and the number of the first intersected surface will be put to the return variable.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cpp.md#intersections)*

### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point coordinates (local).
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point coordinates (local).
- *int* **mask** - Intersection mask.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectIntersection](../../../api/library/objects/class.objectintersection_cpp.md)> &* **v** - [ObjectIntersection](../../../api/library/objects/class.objectintersection_cpp.md) class instance to store corresponding intersection data.
- *int ** **ret_surface** - Intersected surface index.

### Return value

true if there is an intersection; otherwise, false.
## bool getIntersection ( const Math::Vec3& p0 , const Math:: Vec3 & p1 , const Ptr < ObjectIntersection > & v , int surface ) const

Checks if there is an intersection between a line and a given surface. If the function returns true the data about the intersection point will be put to [ObjectIntersection](../../../api/library/objects/class.objectintersection_cpp.md) object.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cpp.md#intersections)*

### Arguments

- *const  Math::Vec3&* **p0** - Line start point coordinates (local).
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point coordinates (local).
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectIntersection](../../../api/library/objects/class.objectintersection_cpp.md)> &* **v** - [ObjectIntersection](../../../api/library/objects/class.objectintersection_cpp.md) class instance to store corresponding intersection data.
- *int* **surface** - Surface number.

### Return value

true if there is an intersection with a given surface; otherwise, false.
## bool getIntersection ( const Math::Vec3& p0 , const Math::Vec3& p1 , int mask , const Ptr < ObjectIntersectionNormal > & v , int * ret_surface ) const

Checks if there is an intersection between a line and a surface with a given intersection mask. If the function returns true the data about the normal at the intersection point will be put to [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_cpp.md) object and the number of the first intersected surface will be put to the return variable.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cpp.md#intersections)*

### Arguments

- *const  Math::Vec3&* **p0** - Line start point coordinates (local).
- *const  Math::Vec3&* **p1** - Line end point coordinates (local).
- *int* **mask** - Intersection mask.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_cpp.md)> &* **v** - [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_cpp.md) class instance to store corresponding intersection data.
- *int ** **ret_surface** - Intersected surface index.

### Return value

true if there is an intersection; otherwise, false.
## bool getIntersection ( const Math::Vec3& p0 , const Math::Vec3& p1 , int mask , const Ptr < ObjectIntersectionTexCoord > & v , int * ret_surface ) const

Checks if there is an intersection between a line and a surface with a given intersection mask. If the function returns true the data about the texture coordinates of the intersection point will be put to [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_cpp.md) object and the number of the first intersected surface will be put to the return variable.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cpp.md#intersections)*

### Arguments

- *const  Math::Vec3&* **p0** - Line start point coordinates (local).
- *const  Math::Vec3&* **p1** - Line end point coordinates (local).
- *int* **mask** - Intersection mask.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_cpp.md)> &* **v** - [ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_cpp.md) class instance to store corresponding intersection data.
- *int ** **ret_surface** - Intersected surface index.

### Return value

true if there is an intersection; otherwise, false.
## bool getIntersection ( const Math::Vec3& p0 , const Math::Vec3& p1 , int mask , Math:: Vec3 * ret_point , Math:: vec3 * OUT_ret_normal , Math:: vec4 * OUT_ret_texcoord , int * ret_index , int * OUT_ret_instance , int * ret_surface ) const

Checks if there is an intersection between a line and a surface with a given intersection mask. If the function returns true the data about the intersection (point, normal and texture coordinates) and the number of the first intersected surface will be put to corresponding return variables.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cpp.md#intersections)*

### Arguments

- *const  Math::Vec3&* **p0** - Line start point coordinates (local).
- *const  Math::Vec3&* **p1** - Line end point coordinates (local).
- *int* **mask** - Intersection mask.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) ** **ret_point** - Intersection point coordinates (object's local coordinate system). Pass NULL if this parameter is not required.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) ** **OUT_ret_normal** - Coordinates of the normal vector to the intersection point. Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md) ** **OUT_ret_texcoord** - Texture coordinates of the intersection point (vec4, where vec4.xy is for the first (0) UV channel, vec4.zw is for the second (1) UV channel). Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int ** **ret_index** - Intersected triangle number. Pass NULL if this parameter is not required.
- *int ** **OUT_ret_instance** - Intersected instance number. Pass NULL if this parameter is not required. > **Notice:** Intersected instance number can be obtained for the following classes: > - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)* > - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)* > - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cpp.md)* > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int ** **ret_surface** - Intersected surface number. Pass NULL if this parameter is not required.

### Return value

true if there is at least one intersection found; otherwise, false.
## bool getIntersection ( const Math:: Vec3 & p0 , const Math::Vec3& p1 , Math:: Vec3 * ret_point , Math:: vec3 * OUT_ret_normal , Math:: vec4 * OUT_ret_texcoord , int * ret_index , int * OUT_ret_instance , int surface ) const

Checks if there is an intersection between a line and a given surface. If the function returns true the data about the intersection (point, normal and texture coordinates) will be put to corresponding return variables.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cpp.md#intersections)*

### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point coordinates (local).
- *const  Math::Vec3&* **p1** - Line end point coordinates (local).
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) ** **ret_point** - Intersection point coordinates (object's local coordinate system). Pass NULL if this parameter is not required.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) ** **OUT_ret_normal** - Coordinates of the normal vector to the intersection point. Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md) ** **OUT_ret_texcoord** - Texture coordinates of the intersection point (vec4, where vec4.xy is for the first (0) UV channel, vec4.zw is for the second (1) UV channel). Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int ** **ret_index** - Intersected triangle number. Pass NULL if this parameter is not required.
- *int ** **OUT_ret_instance** - Intersected instance number. Pass NULL if this parameter is not required. > **Notice:** Intersected instance number can be obtained for the following classes: > - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)* > - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)* > - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cpp.md)* > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **surface** - Surface number.

### Return value

true if there is an intersection with a given surface; otherwise, false.
## void setIntersectionMask ( int mask , int surface )

Sets an intersection mask for a given surface.
### Arguments

- *int* **mask** - Surface intersection mask.
- *int* **surface** - Surface number.

## int getIntersectionMask ( int surface ) const

Returns the intersection mask for a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface intersection mask.
## void setPhysicsIntersection ( bool enabled , int surface )

Enables or disables physics intersections (between physical objects with bodies and collider shapes, or ray intersections with collider geometry) for a given surface.
### Arguments

- *bool* **enabled** - true to enable physics intersections with a given surface, false to disable them.
- *int* **surface** - Surface number.

## bool getPhysicsIntersection ( int surface ) const

Returns a surface physics intersection flag. This flag indicates if physics intersections (between physical objects with bodies and collider shapes, or ray intersections with collider geometry) with a given surface are enabled.
### Arguments

- *int* **surface** - Surface number.

### Return value

true if intersections with a given surface are enabled; otherwise, false.
## void setPhysicsIntersectionMask ( int mask , int surface )

Sets the [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for a surface with the specified number.
### Arguments

- *int* **mask** - Surface physics intersection mask.
- *int* **surface** - Surface number.

## int getPhysicsIntersectionMask ( int surface ) const

Returns the [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for a surface with the specified number.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface physics intersection mask set for the specified surface.
## void setShadowMask ( int mask , int surface )

Sets a shadow mask for a given surface.
For the shadow from an object's surface to be rendered for a light source, this mask must match the following ones (one bit, at least):

- [Shadow mask of the light source](../../../api/library/lights/class.light_cpp.md#setShadowMask_int_void)
- [Shadow mask of the material](../../../api/library/rendering/class.material_cpp.md#setShadowMask_int_void) assigned to this surface


### Arguments

- *int* **mask** - Surface shadow mask.
- *int* **surface** - Surface number.

## int getShadowMask ( int surface ) const

Returns the shadow mask for a given surface.
For the shadow from an object's surface to be rendered for a light source, this mask must match the following ones (one bit, at least):

- [Shadow mask of the light source](../../../api/library/lights/class.light_cpp.md#setShadowMask_int_void)
- [Shadow mask of the material](../../../api/library/rendering/class.material_cpp.md#setShadowMask_int_void) assigned to this surface


### Arguments

- *int* **surface** - Surface number.

### Return value

Surface shadow mask.
## Ptr < Material > getMaterial ( int surface ) const

Returns a material used for a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Material smart pointer.
## Ptr < Material > getMaterialInherit ( int surface )

Inherits the surface material (i.e. creates a material instance). Modifications made to a new material instance will not affect the source material.
> **Notice:** A child material will be created only once, all subsequent calls to this method will return the first created child material.


### Arguments

- *int* **surface** - Surface number.

### Return value

Inherited material smart pointer.
## bool isMaterialInherited ( int surface ) const

Returns the value indicating if a given surface material is inherited. Modifications made in a material instance do not affect the source material.
### Arguments

- *int* **surface** - Surface number.

### Return value

Positive number if the material is inherited; otherwise, **0**.
## void clearMaterialInherit ( int surface )

Removes the inherited material and sets back the source(parent) material for the specified surface.
### Arguments

- *int* **surface** - Surface number.

## void setMaterialParameterInt ( const char * name , int parameter , int surface )

Sets the value of a given integer parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *const char ** **name** - Parameter name.
- *int* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## int getMaterialParameterInt ( const char * name , int surface ) const

Returns the value of a given integer parameter of the surface material.
### Arguments

- *const char ** **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void setMaterialParameterInt2 ( const char * name , const Math:: ivec2 & parameter , int surface )

Sets the value of a given [*ivec2*](../../../api/library/math/class.ivec2_cpp.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## Math:: ivec2 getMaterialParameterInt2 ( const char * name , int surface ) const

Returns the value of a given [*ivec2*](../../../api/library/math/class.ivec2_cpp.md) parameter of the surface material.
### Arguments

- *const char ** **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void setMaterialParameterInt3 ( const char * name , const Math:: ivec3 & parameter , int surface )

Sets the value of a given [*ivec3*](../../../api/library/math/class.ivec3_cpp.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## Math:: ivec3 getMaterialParameterInt3 ( const char * name , int surface ) const

Returns the value of a given [*ivec3*](../../../api/library/math/class.ivec3_cpp.md) parameter of the surface material.
### Arguments

- *const char ** **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void setMaterialParameterInt4 ( const char * name , const Math:: ivec4 & parameter , int surface )

Sets the value of a given [*ivec4*](../../../api/library/math/class.ivec4_cpp.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## Math:: ivec4 getMaterialParameterInt4 ( const char * name , int surface ) const

Returns the value of a given [*ivec4*](../../../api/library/math/class.ivec4_cpp.md) parameter of the surface material.
### Arguments

- *const char ** **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void setMaterialParameterFloat ( const char * name , float parameter , int surface )

Sets the value of a given float parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *const char ** **name** - Parameter name.
- *float* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## float getMaterialParameterFloat ( const char * name , int surface ) const

Returns the value of a given float parameter of the surface material.
### Arguments

- *const char ** **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void setMaterialParameterFloat2 ( const char * name , const Math:: vec2 & parameter , int surface )

Sets the value of a given [*vec2*](../../../api/library/math/class.vec2_cpp.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## Math:: vec2 getMaterialParameterFloat2 ( const char * name , int surface ) const

Returns the value of a given [*vec2*](../../../api/library/math/class.vec2_cpp.md) parameter of the surface material.
### Arguments

- *const char ** **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void setMaterialParameterFloat3 ( const char * name , const Math:: vec3 & parameter , int surface )

Sets the value of a given [*vec3*](../../../api/library/math/class.vec3_cpp.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## Math:: vec3 getMaterialParameterFloat3 ( const char * name , int surface ) const

Returns the value of a given [*vec3*](../../../api/library/math/class.vec3_cpp.md) parameter of the surface material.
### Arguments

- *const char ** **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void setMaterialParameterFloat4 ( const char * name , const Math:: vec4 & parameter , int surface )

Sets the value of a given [*vec4*](../../../api/library/math/class.vec4_cpp.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *const char ** **name** - Parameter name.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## Math:: vec4 getMaterialParameterFloat4 ( const char * name , int surface ) const

Returns the value of a given [*vec4*](../../../api/library/math/class.vec4_cpp.md) parameter of the surface material.
### Arguments

- *const char ** **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void setMaterialState ( const char * name , int state , int surface )

Sets the state value for a given surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *const char ** **name** - Material state name.
- *int* **state** - State value.
- *int* **surface** - Surface number.

## int getMaterialState ( const char * name , int surface ) const

Returns the state value of a given surface material.
### Arguments

- *const char ** **name** - Material state name.
- *int* **surface** - Surface number.

### Return value

State value.
## void setMaterialTexture ( const char * name , const char * texture , int surface )

Sets the path to a given texture of a given surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *const char ** **name** - Material texture name.
- *const char ** **texture** - Path to the texture file.
- *int* **surface** - Surface number.

## const char * getMaterialTexture ( const char * name , int surface ) const

Returns the path to a given texture of a given surface material.
### Arguments

- *const char ** **name** - Material texture name.
- *int* **surface** - Surface number.

### Return value

Path to the texture file.
## void setMinVisibleDistance ( float distance , int surface )

Updates the minimum visibility distance of a given surface. It is the distance, starting from which the surface begins to [fade in](#setMinFadeDistance_float_int_void) until it becomes completely visible.
### Arguments

- *float* **distance** - Minimum visibility distance, in units. If a negative value is provided, **0** will be used instead. The default value is -inf.
- *int* **surface** - Surface number.

## float getMinVisibleDistance ( int surface ) const

Returns minimum visibility distance of a given surface. It is the distance, starting from which the surface begins to [fade in](#setMinFadeDistance_float_int_void) until it becomes completely visible.
### Arguments

- *int* **surface** - Surface number.

### Return value

Minimum visibility distance, in units.
## void setExperimentalNavigation ( bool enabled , int surface )

Sets a value indicating if a given surface contributes to the walkable surface when an [ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md) is baked. Marking geometry is opt-in: a surface takes part in baking only when this flag is set, which keeps decoration and clutter out of the navigation mesh.
### Arguments

- *bool* **enabled** - Navigation flag. The default value is false.
- *int* **surface** - Surface number.

## bool getExperimentalNavigation ( int surface ) const

Returns a value indicating if a given surface contributes to the walkable surface when a navigation mesh is baked.
### Arguments

- *int* **surface** - Surface number.

### Return value

true if the surface takes part in navigation mesh baking; otherwise, false.
## void setExperimentalNavigationBakeMask ( int mask , int surface )

Sets the bake mask of a given surface. The surface is taken in only by the navigation meshes whose own bake mask shares at least one bit with this one, which is how one scene feeds several navigation meshes with different geometry.
### Arguments

- *int* **mask** - [Bake mask](../../../principles/bit_masking/index.md#bake_mask). The default value is 1.
- *int* **surface** - Surface number.

## int getExperimentalNavigationBakeMask ( int surface ) const

Returns the bake mask of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Bake mask of the surface.
## void setExperimentalNavigationArea ( int area , int surface )

Sets the area stamped onto the navigation mesh polygons baked from a given surface. It is how a road, a patch of mud, or a metal walkway gets its own traversal cost without a volume being placed over it.
### Arguments

- *int* **area** - Area index from the registry of the [ExperimentalNavigation](../../../api/library/pathfinding/class.experimentalnavigation_cpp.md) singleton. The default value is 63.
- *int* **surface** - Surface number.

## int getExperimentalNavigationArea ( int surface ) const

Returns the area stamped onto the navigation mesh polygons baked from a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Area index of the surface.
## void setMaxVisibleDistance ( float distance , int surface )

Updates the maximum visibility distance of a given surface. It is the distance, starting from which the surface begins to [fade out](#setMaxFadeDistance_float_int_void) until it becomes completely invisible.
### Arguments

- *float* **distance** - Maximum visibility distance, in units. If a negative value is provided, **0** will be used instead. The default value is inf.
- *int* **surface** - Surface number.

## float getMaxVisibleDistance ( int surface ) const

Returns the maximum visibility distance of a given surface. It is the distance, starting from which the surface begins to [fade out](#getMaxFadeDistance_int_float) until it becomes completely invisible.
### Arguments

- *int* **surface** - Surface number.

### Return value

Maximum visibility distance, in units.
## void setMinFadeDistance ( float distance , int surface )

Updates the minimum fade-in distance of a given surface. Over this distance the surface smoothly becomes visible due to [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [minimum visibility distance](#getMinVisibleDistance_int_float).
### Arguments

- *float* **distance** - Minimum fade-in distance, in units. If a negative value is provided, **0** will be used instead. The default value is 0.
- *int* **surface** - Surface number.

## float getMinFadeDistance ( int surface ) const

Returns the minimum fade-in distance of a given surface. Over this distance the surface smoothly becomes visible due to [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [minimum visibility distance](#getMinVisibleDistance_int_float).
### Arguments

- *int* **surface** - Surface number.

### Return value

Minimum fade-in distance, in units.
## void setMaxFadeDistance ( float distance , int surface )

Updates the maximum fade-out distance of a given surface. Over this distance the surface smoothly becomes invisible due to [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted off starting from the [maximum visibility distance](#getMaxVisibleDistance_int_float).
### Arguments

- *float* **distance** - Maximum fade-out distance, in units. If a negative value is provided, **0** will be used instead. The default value is 0.
- *int* **surface** - Surface number.

## float getMaxFadeDistance ( int surface ) const

Returns the maximum fade-out distance. Over this distance the surface smoothly becomes invisible due to [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [maximum visibility distance](#getMaxVisibleDistance_int_float).
### Arguments

- *int* **surface** - Surface number.

### Return value

Maximum fade-out distance, in units.
## void setMinParent ( int parent , int surface )

Sets surface minimum LOD parent surface number.
### Arguments

- *int* **parent** - Surface minimum LOD parent surface number.
- *int* **surface** - Surface number.

## int getMinParent ( int surface ) const

Returns the surface minimum LOD parent surface number.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface minimum LOD parent surface number.
## void setMaxParent ( int parent , int surface )

Sets a surface maximum LOD parent surface number.
### Arguments

- *int* **parent** - Surface maximum LOD parent surface number.
- *int* **surface** - Surface number.

## int getMaxParent ( int surface ) const

Returns the surface maximum LOD parent surface number.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface maximum LOD parent surface number.
## int getNumTriangles ( int surface ) const

Returns the number of triangles comprising a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Number of triangles.
## void setParent ( int parent , int surface )

Sets or clears the parent surface for a given surface.
### Arguments

- *int* **parent** - Number of the parent surface or **-1** to clear the parent.
- *int* **surface** - Surface number.

## int getParent ( int surface ) const

Returns the number of the parent surface for a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Parent surface number. If -1 is returned, the parent surface is not specified for a given surface.
## int setSurfaceProperty ( const char * name , const char * pattern )

Sets a new property for a given surface.
### Arguments

- *const char ** **name** - Name of the new property.
- *const char ** **pattern** - Pattern (string with a [regular expression](../../../api/library/common/class.regexp_cpp.md#intro)), against which surface names will be matched.

### Return value

1 if the property is set successfully; otherwise, 0.
## int setSurfaceProperty ( const char * name , int surface )

Sets a new property for the specified surface.
### Arguments

- *const char ** **name** - Name of the new property.
- *int* **surface** - Surface number.

### Return value

1 if the property is set successfully; otherwise, 0.
## int setSurfaceProperty ( const UGUID & guid , int surface )

Sets a new property for the specified surface.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Property [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
- *int* **surface** - Surface number.

### Return value

1 if the property is set successfully; otherwise, 0.
## int setSurfaceProperty ( const UGUID & guid , const char * pattern )

Sets a new property for the specified surface(s).
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Property [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
- *const char ** **pattern** - Pattern (string with a [regular expression](../../../api/library/common/class.regexp_cpp.md#intro)), against which surface names will be matched.

### Return value

1 if the property is set successfully; otherwise, 0.
## int setSurfaceProperty ( const Ptr < Property > & property , int surface )

Sets a new property for the specified surface.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)> &* **property** - Property smart pointer.
- *int* **surface** - Surface number.

### Return value

1 if the property is set successfully; otherwise, 0.
## int setSurfaceProperty ( const Ptr < Property > & property , const char * pattern )

Sets a new property for the specified surface(s).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)> &* **property** - Property smart pointer.
- *const char ** **pattern** - Pattern (string with a [regular expression](../../../api/library/common/class.regexp_cpp.md#intro)), against which surface names will be matched.

### Return value

1 if the property is set successfully; otherwise, 0.
## Ptr < Property > getSurfaceProperty ( int surface ) const

Returns the property smart pointer.
### Arguments

- *int* **surface** - Surface number.

### Return value

Property smart pointer.
## Ptr < Property > getSurfacePropertyInherit ( int surface )

Inherits the property for the specific object. All changes of the inherited property will not affect the reference one.
### Arguments

- *int* **surface** - Surface number.

### Return value

Inherited property smart pointer.
## void clearSurfaceProperty ( int surface )

Removes the assigned property from the specified surface.
### Arguments

- *int* **surface** - Surface number.

## void clearSurfacePropertyInherit ( int surface )

Removes the inherited property and sets back the source(parent) property for the specified surface.
### Arguments

- *int* **surface** - Surface number.

## bool isSurfacePropertyInherited ( int surface ) const

Returns a value indicating if a given property is inherited.
### Arguments

- *int* **surface** - Surface number.

### Return value

Positive number if the surface property is inherited; otherwise, **0**.
## const char * getSurfacePropertyName ( int surface ) const

Returns the name of the property of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Property name.
## const char * getSurfaceName ( int surface ) const

Returns the name of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface name.
## void setViewportMask ( int mask , int surface )

Sets a [viewport mask](../../../principles/bit_masking/index.md#viewport) for a given surface. The object surface is rendered, if its mask matches the player (camera) and material masks.
```cpp
// hide the first surface from the camera by disabling all the bits of the mask
obj->setViewportMask(0, 0);

// restore visibility of the surface (the camera must have the first bit of the Viewport mask enabled)
obj->setViewportMask(1, 0);

// enable all the bits by using bitwise NOT
obj->setViewportMask(~0, 0);

// enable ONLY the fifth bit of the mask
obj->setViewportMask(1 << 4, 0);


```


### Arguments

- *int* **mask** - Surface viewport mask.
- *int* **surface** - Surface number.

## int getViewportMask ( int surface ) const

Returns a viewport mask for a given surface. The object surface is rendered, if its mask matches the player (camera) and material masks.
```cpp
// get the viewport mask of the first surface
int mask = obj->getViewportMask(0);

// check if the fifth bit is set
bool isBitSet = (mask >> 4 & 1) != 0;

// check if masks match
bool doMasksMatch = (mask & mask2) != 0;


```


### Arguments

- *int* **surface** - Surface number.

### Return value

Surface viewport mask.
## Math:: WorldBoundBox getWorldBoundBox ( int surface ) const

Returns the world bounding box of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Bounding box (in world coordinates).
## Math:: WorldBoundSphere getWorldBoundSphere ( int surface ) const

Returns the world bounding sphere of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Bounding sphere (in world coordinates).
## int findSurface ( const char * name ) const

Searches for a surface with a given name.
### Arguments

- *const char ** **name** - Surface name.

### Return value

Surface number if it exists; otherwise, -1.
## void flushBodyTransform ( )

Forces to set the transformations of the body for the node.
## void render ( Render::PASS pass , int surface )


Renders raw object's surface to texture in specified pass.


> **Notice:** All [camera parameters](../../../code/uusl/parameters.md#camera_parameters) should be set manually.


**Usage Example**


```cpp
texture_render->bindColorTexture(0, texture);
texture_render->enable();
object->render(Render::PASS_AMBIENT, 0);
texture_render->disable();
texture_render->unbindColorTexture(0);


```


### Arguments

- *[Render::PASS](../../../api/library/rendering/class.render_cpp.md#PASS)* **pass** - A [rendering pass](../../../api/library/rendering/class.render_cpp.md#PASS_WIREFRAME).
- *int* **surface** - Surface number.

## void setSoundOcclusion ( float occlusion , int surface )

Sets a new sound occlusion value for the specified surface of the object, that determines how much it affects sounds in case of occlusion. For a sound source to be occluded by the specified surface, at least one bit of its [occlusion mask](#setSoundOcclusionMask_int_int_void) should match the [occlusion mask of the sound source](../../../api/library/sounds/class.soundsource_cpp.md#setOcclusionMask_int_void).
> **Notice:** [Sound occlusion](../../../api/library/engine/class.sound_cpp.md#setSourceOcclusion_int_void) must be enabled.


### Arguments

- *float* **occlusion** - Occlusion value in the range **[0.0f, 1.0f]** to be set for the specified surface. The default value is 0.0f.

  - 0.0f - no occlusion, sound volume will stay the same in case of occlusion by the surface.
  - 1.0f - maximum occlusion, sound will not be heard at all in case of occlusion by the surface.
- *int* **surface** - Surface number.

## float getSoundOcclusion ( int surface ) const

Returns the current sound occlusion value for the specified surface of the object, that determines how much it affects sounds in case of occlusion. For a sound source to be occluded by the specified surface, at least one bit of its [occlusion mask](#setSoundOcclusionMask_int_int_void) should match the [occlusion mask of the sound source](../../../api/library/sounds/class.soundsource_cpp.md#setOcclusionMask_int_void).
> **Notice:** [Sound occlusion](../../../api/library/engine/class.sound_cpp.md#setSourceOcclusion_int_void) must be enabled.


### Arguments

- *int* **surface** - Surface number.

### Return value

Current occlusion value in the range **[0.0f, 1.0f]** set for the specified surface.
- 0.0f - no occlusion, sound volume will stay the same in case of occlusion by the surface.
- 1.0f - maximum occlusion, sound will not be heard at all in case of occlusion by the surface.

The default value is 0.0f.
## void setSoundOcclusionMask ( int mask , int surface )

Sets a new sound occlusion mask for the specified surface of the object. For a sound source to be occluded by the specified surface, at least one bit of this mask should match the [occlusion mask of the sound source](../../../api/library/sounds/class.soundsource_cpp.md#setOcclusionMask_int_void). Each surface has its own [occlusion value](#setSoundOcclusion_float_int_void), that determines how much it affects sounds in case of occlusion.
> **Notice:** [Sound occlusion](../../../api/library/engine/class.sound_cpp.md#setSourceOcclusion_int_void) must be enabled.


### Arguments

- *int* **mask** - Integer, each bit of which is a mask for sound source occlusion.
- *int* **surface** - Surface number.

## int getSoundOcclusionMask ( int surface ) const

Returns sound occlusion mask for the specified surface of the object. For a sound source to be occluded by the specified surface, at least one bit of this mask should match the [occlusion mask of the sound source](../../../api/library/sounds/class.soundsource_cpp.md#setOcclusionMask_int_void). Each surface has its own [occlusion value](#setSoundOcclusion_float_int_void), that determines how much it affects sounds in case of occlusion.
> **Notice:** [Sound occlusion](../../../api/library/engine/class.sound_cpp.md#setSourceOcclusion_int_void) must be enabled.


### Arguments

- *int* **surface** - Surface number.

### Return value

Integer, each bit of which is a mask for sound source occlusion.
## void setPhysicsFriction ( float value , int surface )

Sets the coefficient of friction for the specified surface. This coefficient allows to model more rough rubbing of surfaces and is opposite to the body's movement direction. Friction parameter values of both surfaces being in contact are considered. The resulting calculated friction depends on the objects' masses and gravity, and the angle between contacting surfaces.
- The *higher* the value, the less tendency the body has to slide.

Friction is calculated by the contact between physical bodies.
### Arguments

- *float* **value** - Friction coefficient value in the range **[0.0f, 1.0f]** to be set for the specified surface.
- *int* **surface** - Surface number.

## float getPhysicsFriction ( int surface ) const

Returns the current coefficient of friction for the specified surface. This coefficient allows to model more rough rubbing of surfaces and is opposite to the body's movement direction. Friction parameter values of both surfaces being in contact are considered. The resulting calculated friction depends on the objects' masses and gravity, and the angle between contacting surfaces.
- The *higher* the value, the less tendency the body has to slide.

Friction is calculated by the contact between physical bodies.
### Arguments

- *int* **surface** - Surface number.

### Return value

Current friction coefficient value in the range **[0.0f, 1.0f]** set for the specified surface.
## void setPhysicsRestitution ( float value , int surface )

Sets the coefficient of restitution for the specified surface. This coefficient determines the degree of relative kinetic energy retained after a collision. It defines how bouncy the object is by contacting with another object. It depends on the elasticity of the materials of colliding bodies. The simulated restitution, like [friction](#setPhysicsFriction_float_int_void), considers the total value for both objects being in contact.
- The maximum value of 1.0f models elastic collision. Objects bounce off according to the impulse they get by contact.
- The minimum value of 0.0f models inelastic collision. Objects do not bounce at all.

Restitution is calculated by the contact between physical bodies.
### Arguments

- *float* **value** - Restitution coefficient value in the range **[0.0f, 1.0f]** to be set for the specified surface.
- *int* **surface** - Surface number.

## float getPhysicsRestitution ( int surface ) const

Returns the current coefficient of restitution for the specified surface. This coefficient determines the degree of relative kinetic energy retained after a collision. It defines how bouncy the object is by contacting with another object. It depends on the elasticity of the materials of colliding bodies. The simulated restitution, like [friction](#setPhysicsFriction_float_int_void), considers the total value for both objects being in contact.
- The maximum value of 1.0f models elastic collision. Objects bounce off according to the impulse they get by contact.
- The minimum value of 0.0f models inelastic collision. Objects do not bounce at all.

Restitution is calculated by the contact between physical bodies.
### Arguments

- *int* **surface** - Surface number.

### Return value

Current restitution coefficient value in the range **[0.0f, 1.0f]** set for the specified surface.
## void setShadowMode ( Object::SURFACE_SHADOW_MODE mode , int surface )

Sets the shadow mode for the specified surface. To cast a shadow from a light source (Omni, Proj, or World), the surface's shadow mode should be [adjusted](../../../content/optimization/lights/index.md#static_light) in accordance with the [shadow mode of the light source](../../../api/library/lights/class.light_cpp.md#setShadowMode_int_void).
### Arguments

- *[Object::SURFACE_SHADOW_MODE](../../../api/library/objects/class.object_cpp.md#SURFACE_SHADOW_MODE)* **mode** - Surface shadow mode to be set, one of the following:

  - [SURFACE_SHADOW_MODE_DYNAMIC](#SURFACE_SHADOW_MODE_DYNAMIC)
  - [SURFACE_SHADOW_MODE_MIXED](#SURFACE_SHADOW_MODE_MIXED)
- *int* **surface** - Target surface number.

## Object::SURFACE_SHADOW_MODE getShadowMode ( int surface ) const

Returns the shadow mode set for the specified surface. To cast a shadow from a light source (Omni, Proj, or World), the surface's shadow mode should be [adjusted](../../../content/optimization/lights/index.md#static_light) in accordance with the [shadow mode of the light source](../../../api/library/lights/class.light_cpp.md#setShadowMode_int_void).
### Arguments

- *int* **surface** - Target surface number.

### Return value

Surface shadow mode, one of the following:
- [SURFACE_SHADOW_MODE_DYNAMIC](#SURFACE_SHADOW_MODE_DYNAMIC)
- [SURFACE_SHADOW_MODE_MIXED](#SURFACE_SHADOW_MODE_MIXED)


## UGUID getLostMaterialGUID ( int surface ) const

Returns the [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of a lost material. If for some reason a material assigned to the specified surface is missing, this method can be used to get it's GUID.
### Arguments

- *int* **surface** - Target surface number.

### Return value

Lost material [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
## UGUID getLostSurfacePropertyGUID ( int surface ) const

Returns the [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of a lost surface property. If for some reason a property assigned to the specified surface is missing, this method can be used to get it's GUID.
### Arguments

- *int* **surface** - Target surface number.

### Return value

Lost property [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
## void setLightingMode ( Object::SURFACE_LIGHTING_MODE mode , int surface )

Sets the lighting mode for the specified surface.
### Arguments

- *[Object::SURFACE_LIGHTING_MODE](../../../api/library/objects/class.object_cpp.md#SURFACE_LIGHTING_MODE)* **mode** - Surface lighting mode to be set, one of the following:

  - [SURFACE_LIGHTING_MODE_STATIC](#SURFACE_LIGHTING_MODE_STATIC)
  - [SURFACE_LIGHTING_MODE_DYNAMIC](#SURFACE_LIGHTING_MODE_DYNAMIC)
  - [SURFACE_LIGHTING_MODE_ADVANCED](#SURFACE_LIGHTING_MODE_ADVANCED)
- *int* **surface** - Target surface number.

## Object::SURFACE_LIGHTING_MODE getLightingMode ( int surface ) const

Returns the lighting mode for the specified surface.
### Arguments

- *int* **surface** - Target surface number.

### Return value

Surface lighting mode, one of the following:
- [SURFACE_LIGHTING_MODE_STATIC](#SURFACE_LIGHTING_MODE_STATIC)
- [SURFACE_LIGHTING_MODE_DYNAMIC](#SURFACE_LIGHTING_MODE_DYNAMIC)
- [SURFACE_LIGHTING_MODE_ADVANCED](#SURFACE_LIGHTING_MODE_ADVANCED)


## void setMaterialFilePath ( const char * path , int surface )

Sets the material by file path to a given surface.
### Arguments

- *const char ** **path** - Material file path.
- *int* **surface** - Target surface number.

## void setMaterialFilePath ( const char * path , const char * pattern )

Sets the material by file path to given surfaces.
### Arguments

- *const char ** **path** - Material file path.
- *const char ** **pattern** - Pattern (string with a [regular expression](../../../api/library/common/class.regexp_cpp.md#intro)), against which surface names will be matched.

## String getMaterialFilePath ( int surface ) const

Returns the file path for the material assigned to a given surface.
### Arguments

- *int* **surface** - Target surface number.

### Return value

Material file path.
## void setMaterialGUID ( const UGUID & guid , int surface )

Sets a new material with a given [GUID](../../../api/library/filesystem/class.uguid_cpp.md) to the specified surface.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Material [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
- *int* **surface** - Target surface number.

## void setMaterialGUID ( const UGUID & guid , const char * pattern )

Sets a new material with a given [GUID](../../../api/library/filesystem/class.uguid_cpp.md) to the specified surface.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Material [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
- *const char ** **pattern** - Pattern (string with a [regular expression](../../../api/library/common/class.regexp_cpp.md#intro)), against which surface names will be matched.

## UGUID getMaterialGUID ( int surface ) const

Returns a [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the material for the specified surface.
### Arguments

- *int* **surface** - Target surface number.

### Return value

Material [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
## void setMaterial ( const Ptr < Material > & mat , int surface )

Sets a new material for the specified surface.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **mat** - Material smart pointer.
- *int* **surface** - Surface number.

## void setMaterial ( const Ptr < Material > & mat , const char * pattern )

Sets a new material for the specified surface.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **mat** - Material smart pointer.
- *const char ** **pattern** - Pattern (string with a [regular expression](../../../api/library/common/class.regexp_cpp.md#intro)), against which surface names will be matched.

## int getSurfaceStatDrawCalls ( int surface ) const

Returns the number of draw calls (DIP) for the surface with the specified number during the last frame.
### Arguments

- *int* **surface** - Surface number.

### Return value

Number of draw calls (DIP) for the specified surface during the last frame.
## int getSurfaceStatDrawCountViewport ( int surface ) const

Returns the number of times the surface with the specified number was drawn in the viewport last frame.
### Arguments

- *int* **surface** - Surface number.

### Return value

Number of times the specified surface was drawn in the viewport last frame.
## int getSurfaceStatDrawCountReflection ( int surface ) const

Returns the number of times the surface with the specified index was drawn during reflections rendering in the last frame.
### Arguments

- *int* **surface** - Surface number.

### Return value

Number of times the specified surface was drawn during reflections rendering in the last frame.
## int getSurfaceStatDrawCountShadow ( int surface ) const

Returns the number of times the surface with the specified index was drawn during shadows rendering in the last frame.
```cpp
ObjectMeshStaticPtr mesh;
int total_draw_count_shadows = 0;

// event handler function calculating the total number of times the surfaces of a Static Mesh were drawn

void endscreen_event_handler()
{
	total_draw_count_shadows = 0;

	for (int surf = 0; surf < mesh->getNumSurfaces(); surf++)
	{
		if (mesh->getSurfaceStatFrame(surf) == Engine::get()->getFrame())
		{
			// This surface was rendered during the current frame, so the info is up-to date
			total_draw_count_shadows += mesh->getSurfaceStatDrawCountShadow(surf);
		}
	}
}

// create an instance of the EventConnection class
EventConnection endscreen_event_connection;

int AppWorldLogic::init()
{

	// subscribe to the EndScreen event with a handler function keeping the connection
	Render::getEventEndScreen().connect(endscreen_event_connection, endscreen_event_handler);

	return 1;
}


```


### Arguments

- *int* **surface** - Surface number.

### Return value

Number of times the specified surface was drawn during shadows rendering in the last frame.
## long long getSurfaceStatFrame ( int surface ) const

Returns the number of [Engine frame](../../../api/library/engine/class.engine_cpp.md#getFrame_int64_t), in which the surface with the specified number was drawn last time.
### Arguments

- *int* **surface** - Surface number.

### Return value

Number of frame, in which the specified surface was drawn last time.
## float getSurfaceRenderCustomParameterFloat ( int surface , const char * name ) const

Returns the current value of the custom surface parameter with the given name for the given surface of the object. If the parameter is not overridden for the surface, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **surface** - Surface number.
- *const char ** **name** - Parameter name.

### Return value

Current parameter value, or 0 if no parameter with this name exists.
## float getSurfaceRenderCustomParameterFloat ( int surface , int param ) const

Returns the current value of the custom surface parameter with the given number for the given surface of the object. If the parameter is not overridden for the surface, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.

### Return value

Current parameter value.
## int getSurfaceRenderCustomParameterInt ( int surface , const char * name ) const

Returns the current value of the custom surface parameter with the given name for the given surface of the object. If the parameter is not overridden for the surface, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **surface** - Surface number.
- *const char ** **name** - Parameter name.

### Return value

Current parameter value, or 0 if no parameter with this name exists.
## int getSurfaceRenderCustomParameterInt ( int surface , int param ) const

Returns the current value of the custom surface parameter with the given number for the given surface of the object. If the parameter is not overridden for the surface, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.

### Return value

Current parameter value.
## unsigned int getSurfaceRenderCustomParameterUInt ( int surface , const char * name ) const

Returns the current value of the custom surface parameter with the given name for the given surface of the object. If the parameter is not overridden for the surface, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **surface** - Surface number.
- *const char ** **name** - Parameter name.

### Return value

Current parameter value, or 0 if no parameter with this name exists.
## unsigned int getSurfaceRenderCustomParameterUInt ( int surface , int param ) const

Returns the current value of the custom surface parameter with the given number for the given surface of the object. If the parameter is not overridden for the surface, the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)* is returned.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.

### Return value

Current parameter value.
## bool isSurfaceRenderCustomParameterOverridden ( int surface , int param ) const

Checks if the custom surface parameter with the given number is overridden for the given surface of the object.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.

### Return value

true if the parameter is overridden for the surface; otherwise, false.
## void resetSurfaceRenderCustomParameter ( int surface , int param )

Resets the override of the custom surface parameter with the given number for the given surface: the surface uses the default value from the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)* again.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.

## void resetSurfaceRenderCustomParameters ( int surface )

Resets the overrides of all custom surface parameters for the given surface of the object.
### Arguments

- *int* **surface** - Surface number.

## void setSurfaceRenderCustomParameterFloat ( int surface , const char * name , float value )

Sets a new value of the custom surface parameter with the given name for the given surface of the object. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)*. If no parameter with this name exists in the layout, the method does nothing.
### Arguments

- *int* **surface** - Surface number.
- *const char ** **name** - Parameter name.
- *float* **value** - New parameter value.

## void setSurfaceRenderCustomParameterFloat ( int surface , int param , float value )

Sets a new value of the custom surface parameter with the given number for the given surface of the object. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)*.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.
- *float* **value** - New parameter value.

## void setSurfaceRenderCustomParameterInt ( int surface , const char * name , int value )

Sets a new value of the custom surface parameter with the given name for the given surface of the object. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)*. If no parameter with this name exists in the layout, the method does nothing.
### Arguments

- *int* **surface** - Surface number.
- *const char ** **name** - Parameter name.
- *int* **value** - New parameter value.

## void setSurfaceRenderCustomParameterInt ( int surface , int param , int value )

Sets a new value of the custom surface parameter with the given number for the given surface of the object. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)*.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.
- *int* **value** - New parameter value.

## void setSurfaceRenderCustomParameterUInt ( int surface , const char * name , unsigned int value )

Sets a new value of the custom surface parameter with the given name for the given surface of the object. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)*. If no parameter with this name exists in the layout, the method does nothing.
### Arguments

- *int* **surface** - Surface number.
- *const char ** **name** - Parameter name.
- *unsigned int* **value** - New parameter value.

## void setSurfaceRenderCustomParameterUInt ( int surface , int param , unsigned int value )

Sets a new value of the custom surface parameter with the given number for the given surface of the object. The value overrides the default value defined in the *[surface parameters layout](../../../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)*.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.
- *unsigned int* **value** - New parameter value.
