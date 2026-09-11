# Object Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


An [object](../../../objects/index.md) with a set of [surfaces](../../../principles/world_structure/index.md#surfaces) to represent geometry. Rendering materials are [assigned](#setMaterial_Material_int_void) per object surface. An object can be assigned a [physical body](#setBody_Body_int_int).


## Object Class

### Members

## int getNumSurfaces () const

Returns the current number of surfaces of the object.
> **Notice:** For your convenience, *[ObjectMeshDynamic()()](../../../api/library/objects/class.objectmeshdynamic_usc.md#ObjectMeshDynamic_constPtrMesh_int)* initializes the object with one internal surface named "`dynamic`". The first call to *[addSurface()()](../../../api/library/objects/class.objectmeshdynamic_usc.md#addSurface_cstr_void)* simply assigns a user-defined name to this surface without changing the total surface count. To create additional surfaces, call *[addSurface()()](../../../api/library/objects/class.objectmeshdynamic_usc.md#addSurface_cstr_void)* again.


### Return value

Current number of surfaces of the object
## void setEnabled ( int enabled )

Sets a new value indicating if the node and its parent nodes are enabled.
### Arguments

- *int* **enabled** - The node

## int isEnabled () const

Returns the current value indicating if the node and its parent nodes are enabled.
### Return value

Current node
## BodyRigid getBodyRigid () const

Returns the current rigid body assigned to the object.
### Return value

Current rigid body assigned to the object
## void setBody ( Body body )

Sets a new physical body assigned to the object, or **NULL** (**0**) if no body is assigned.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body** - The physical body assigned to the object

## Body getBody () const

Returns the current physical body assigned to the object, or **NULL** (**0**) if no body is assigned.
### Return value

Current physical body assigned to the object
## int isVisibleShadow () const

Returns the current value indicating if the object's shadow is rendered.
### Return value

Current the object's shadow is rendered
## int isVisibleCamera () const

Returns the current value indicating if the object is rendered.
### Return value

Current the object is rendered
---

## BoundBox getBoundBox ( int surface )

Returns the bounding box of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Bounding box.
## BoundSphere getBoundSphere ( int surface )

Returns the bounding sphere of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Bounding sphere.
## void setBakeToEnvProbe ( int enabled , int surface )

Sets a value indicating if the specified surface is to be baked to environment probes.
### Arguments

- *int* **enabled** - **1** to enable baking of the specified surface to environment probes, **0** - to disable it.
- *int* **surface** - Surface number.

## int getBakeToEnvProbe ( int surface )

Returns a value indicating if the specified surface is to be baked to environment probes.
### Arguments

- *int* **surface** - Surface number.

### Return value

**1** if the specified surface is to be baked to environment probes; otherwise, **0**.
## void setBakeToGI ( int enabled , int surface )

Sets a value indicating if the specified surface is to be baked to GI (voxel probes and lightmaps).
### Arguments

- *int* **enabled** - **1** to enable baking of the specified surface to GI, **0** - to disable it.
- *int* **surface** - Surface number.

## int getBakeToGI ( int surface )

Returns a value indicating if the specified surface is to be baked to GI (voxel probes and lightmaps).
### Arguments

- *int* **surface** - Surface number.

### Return value

**1** if the specified surface is to be baked to GI; otherwise, **0**.
## void setCastEnvProbeShadow ( int enabled , int surface )

Enables or disables casting shadows from environment probes by the specified surface.
### Arguments

- *int* **enabled** - **1** to enable casting shadows from environment probes by the specified surface, **0** to disable it.
- *int* **surface** - Surface number.

## int getCastEnvProbeShadow ( int surface )

Returns a value indicating if casting shadows from environment probes by the specified surface is enabled.
### Arguments

- *int* **surface** - Surface number.

### Return value

**1** if casting shadows from environment probes by the specified surface is enabled; otherwise, **0**.
## void setCastShadow ( int enabled , int surface )

Enables or disables casting shadows from non-world lights for a given surface.
### Arguments

- *int* **enabled** - **1** if shadows are to be cast by a given surface; otherwise, **0**.
- *int* **surface** - Surface number.

## int getCastShadow ( int surface )

Returns the surface cast shadow flag, which indicates if a given surface should cast shadows from non-world lights.
### Arguments

- *int* **surface** - Surface number.

### Return value

Positive number if shadows are cast by a given surface; otherwise, **0**.
## void setCastWorldShadow ( int enabled , int surface )

Enables or disables casting shadows from world lights for a given surface.
### Arguments

- *int* **enabled** - **1** if world shadows are to be cast by a given surface; otherwise, **0**.
- *int* **surface** - Surface number.

## int getCastWorldShadow ( int surface )

Returns the surface cast world shadow flag, which indicates if a given surface should cast shadows from world lights.
### Arguments

- *int* **surface** - Surface number.

### Return value

Positive number if world shadows are cast by a given surface; otherwise, **0**.
## void setCollision ( int enabled , int surface )

Enables or disables [collision detection](../../../principles/physics/collision/index.md) for a given surface.
### Arguments

- *int* **enabled** - **1** if collision detection is enabled for a given surface; otherwise, **0**.
- *int* **surface** - Surface number.

## int getCollision ( int surface )

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

## int getCollisionMask ( int surface )

Returns the collision mask for a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface collision mask.
## void setEnabled ( int enabled , int surface )

Enables or disables a surface with the specified number. The disabled surface is not rendered, does not take part in collision detection, and does not cast shadows.
### Arguments

- *int* **enabled** - **1** to enable the surface, **0** to disable it.
- *int* **surface** - Surface number.

## int isEnabled ( int surface )

Returns a value indicating if a given surface is enabled.
### Arguments

- *int* **surface** - Surface number.

### Return value

**1** if the surface is enabled; otherwise, **0**.
## void setIntersection ( int enabled , int surface )

Enables or disables intersections with a given surface.
### Arguments

- *int* **enabled** - **1** to enable intersections with a given surface, **0** to disable them.
- *int* **surface** - Surface number.

## bool getIntersection ( Vec3 p0 , Vec3 p1 , ObjectIntersectionTexCoord v , int surface )

Checks if there is an intersection between a line and a given surface. If the function returns true the data about the texture coordinates of the intersection point will be put to [ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_usc.md) object.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_usc.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_usc.md#intersections)*


### Arguments

- *Vec3* **p0** - Line start point coordinates (local).
- *Vec3* **p1** - Line end point coordinates (local).
- *[ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_usc.md)* **v** - [ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_usc.md) class instance to store corresponding intersection data.
- *int* **surface** - Surface number.

### Return value

**1** if there is an intersection with a given surface; otherwise, **0**.
## int getIntersection ( int surface )

Returns a surface intersection flag. This flag indicates if intersections with a given surface are enabled.
### Arguments

- *int* **surface** - Surface number.

### Return value

**1** if intersections with a given surface are enabled; otherwise, **0**.
## bool getIntersection ( Vec3 p0 , Vec3 p1 , ObjectIntersectionNormal v , int surface )

Checks if there is an intersection between a line and a given surface. If the function returns true the data about the normal at the intersection point will be put to [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_usc.md) object.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_usc.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_usc.md#intersections)*

### Arguments

- *Vec3* **p0** - Line start point coordinates (local).
- *Vec3* **p1** - Line end point coordinates (local).
- *[ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_usc.md)* **v** - [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_usc.md) class instance to store corresponding intersection data.
- *int* **surface** - Surface number.

### Return value

**1** if there is an intersection with a given surface; otherwise, **0**.
## bool getIntersection ( Vec3 p0 , int mask , ObjectIntersection v , int[] ret_surface )

Checks if there is an intersection between a line and a surface with a given intersection mask. If the function returns true the data about the intersection point will be put to [ObjectIntersection](../../../api/library/objects/class.objectintersection_usc.md) object and the number of the first intersected surface will be put to the return variable.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_usc.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_usc.md#intersections)*

### Arguments

- *Vec3* **p0** - Line start point coordinates (local).
- *int* **mask** - Intersection mask.
- *[ObjectIntersection](../../../api/library/objects/class.objectintersection_usc.md)* **v** - [ObjectIntersection](../../../api/library/objects/class.objectintersection_usc.md) class instance to store corresponding intersection data.
- *int[]* **ret_surface** - Intersected surface index.

### Return value

**1** if there is an intersection; otherwise, **0**.
## bool getIntersection ( Vec3 p0 , ObjectIntersection v , int surface )

Checks if there is an intersection between a line and a given surface. If the function returns true the data about the intersection point will be put to [ObjectIntersection](../../../api/library/objects/class.objectintersection_usc.md) object.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_usc.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_usc.md#intersections)*

### Arguments

- *Vec3* **p0** - Line start point coordinates (local).
- *[ObjectIntersection](../../../api/library/objects/class.objectintersection_usc.md)* **v** - [ObjectIntersection](../../../api/library/objects/class.objectintersection_usc.md) class instance to store corresponding intersection data.
- *int* **surface** - Surface number.

### Return value

**1** if there is an intersection with a given surface; otherwise, **0**.
## bool getIntersection ( Vec3 p0 , Vec3 p1 , int mask , ObjectIntersectionNormal v , int[] ret_surface )

Checks if there is an intersection between a line and a surface with a given intersection mask. If the function returns true the data about the normal at the intersection point will be put to [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_usc.md) object and the number of the first intersected surface will be put to the return variable.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_usc.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_usc.md#intersections)*

### Arguments

- *Vec3* **p0** - Line start point coordinates (local).
- *Vec3* **p1** - Line end point coordinates (local).
- *int* **mask** - Intersection mask.
- *[ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_usc.md)* **v** - [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_usc.md) class instance to store corresponding intersection data.
- *int[]* **ret_surface** - Intersected surface index.

### Return value

**1** if there is an intersection; otherwise, **0**.
## bool getIntersection ( Vec3 p0 , Vec3 p1 , int mask , ObjectIntersectionTexCoord v , int[] ret_surface )

Checks if there is an intersection between a line and a surface with a given intersection mask. If the function returns true the data about the texture coordinates of the intersection point will be put to [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_usc.md) object and the number of the first intersected surface will be put to the return variable.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_usc.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_usc.md#intersections)*

### Arguments

- *Vec3* **p0** - Line start point coordinates (local).
- *Vec3* **p1** - Line end point coordinates (local).
- *int* **mask** - Intersection mask.
- *[ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_usc.md)* **v** - [ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_usc.md) class instance to store corresponding intersection data.
- *int[]* **ret_surface** - Intersected surface index.

### Return value

**1** if there is an intersection; otherwise, **0**.
## bool getIntersection ( Vec3 p0 , Vec3 p1 , int mask , Vec3[] ret_point , int[] ret_index , int[] ret_surface )

Checks if there is an intersection between a line and a surface with a given intersection mask. If the function returns true the data about the intersection (point, normal and texture coordinates) and the number of the first intersected surface will be put to corresponding return variables.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_usc.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_usc.md#intersections)*

### Arguments

- *Vec3* **p0** - Line start point coordinates (local).
- *Vec3* **p1** - Line end point coordinates (local).
- *int* **mask** - Intersection mask.
- *Vec3[]* **ret_point** - Intersection point coordinates (object's local coordinate system). Pass NULL if this parameter is not required.
- *int[]* **ret_index** - Intersected triangle number. Pass NULL if this parameter is not required.
- *int[]* **ret_surface** - Intersected surface number. Pass NULL if this parameter is not required.

### Return value

**1** if there is at least one intersection found; otherwise, **0**.
## bool getIntersection ( Vec3 p1 , Vec3[] ret_point , int[] ret_index , int surface )

Checks if there is an intersection between a line and a given surface. If the function returns true the data about the intersection (point, normal and texture coordinates) will be put to corresponding return variables.
> **Notice:** The following objects have individual parameters, that control accuracy of intersection detection for them:
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_usc.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_usc.md#intersections)*

### Arguments

- *Vec3* **p1** - Line end point coordinates (local).
- *Vec3[]* **ret_point** - Intersection point coordinates (object's local coordinate system). Pass NULL if this parameter is not required.
- *int[]* **ret_index** - Intersected triangle number. Pass NULL if this parameter is not required.
- *int* **surface** - Surface number.

### Return value

**1** if there is an intersection with a given surface; otherwise, **0**.
## void setIntersectionMask ( int mask , int surface )

Sets an intersection mask for a given surface.
### Arguments

- *int* **mask** - Surface intersection mask.
- *int* **surface** - Surface number.

## int getIntersectionMask ( int surface )

Returns the intersection mask for a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface intersection mask.
## void setPhysicsIntersection ( int enabled , int surface )

Enables or disables physics intersections (between physical objects with bodies and collider shapes, or ray intersections with collider geometry) for a given surface.
### Arguments

- *int* **enabled** - **1** to enable physics intersections with a given surface, **0** to disable them.
- *int* **surface** - Surface number.

## int getPhysicsIntersection ( int surface )

Returns a surface physics intersection flag. This flag indicates if physics intersections (between physical objects with bodies and collider shapes, or ray intersections with collider geometry) with a given surface are enabled.
### Arguments

- *int* **surface** - Surface number.

### Return value

**1** if intersections with a given surface are enabled; otherwise, **0**.
## void setPhysicsIntersectionMask ( int mask , int surface )

Sets the [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for a surface with the specified number.
### Arguments

- *int* **mask** - Surface physics intersection mask.
- *int* **surface** - Surface number.

## int getPhysicsIntersectionMask ( int surface )

Returns the [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for a surface with the specified number.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface physics intersection mask set for the specified surface.
## void setShadowMask ( int mask , int surface )

Sets a shadow mask for a given surface.
For the shadow from an object's surface to be rendered for a light source, this mask must match the following ones (one bit, at least):

- [Shadow mask of the light source](../../../api/library/lights/class.light_usc.md#setShadowMask_int_void)
- [Shadow mask of the material](../../../api/library/rendering/class.material_usc.md#setShadowMask_int_void) assigned to this surface


### Arguments

- *int* **mask** - Surface shadow mask.
- *int* **surface** - Surface number.

## int getShadowMask ( int surface )

Returns the shadow mask for a given surface.
For the shadow from an object's surface to be rendered for a light source, this mask must match the following ones (one bit, at least):

- [Shadow mask of the light source](../../../api/library/lights/class.light_usc.md#setShadowMask_int_void)
- [Shadow mask of the material](../../../api/library/rendering/class.material_usc.md#setShadowMask_int_void) assigned to this surface


### Arguments

- *int* **surface** - Surface number.

### Return value

Surface shadow mask.
## Material getMaterial ( int surface )

Returns a material used for a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Material used for the surface.
## Material getMaterialInherit ( int surface )

Inherits the surface material (i.e. creates a material instance). Modifications made to a new material instance will not affect the source material.
> **Notice:** A child material will be created only once, all subsequent calls to this method will return the first created child material.


### Arguments

- *int* **surface** - Surface number.

### Return value

Inherited material.
## int isMaterialInherited ( int surface )

Returns the value indicating if a given surface material is inherited. Modifications made in a material instance do not affect the source material.
### Arguments

- *int* **surface** - Surface number.

### Return value

Positive number if the material is inherited; otherwise, **0**.
## void clearMaterialInherit ( int surface )

Removes the inherited material and sets back the source(parent) material for the specified surface.
### Arguments

- *int* **surface** - Surface number.

## void setMaterialParameterInt ( string name , int parameter , int surface )

Sets the value of a given integer parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Parameter name.
- *int* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## int getMaterialParameterInt ( string name , int surface )

Returns the value of a given integer parameter of the surface material.
### Arguments

- *string* **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void setMaterialParameterInt2 ( string name , ivec2 parameter , int surface )

Sets the value of a given [*ivec2*](../../../api/library/math/class.ivec2_usc.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Parameter name.
- *ivec2* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## ivec2 getMaterialParameterInt2 ( string name , int surface )

Returns the value of a given [*ivec2*](../../../api/library/math/class.ivec2_usc.md) parameter of the surface material.
### Arguments

- *string* **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void setMaterialParameterInt3 ( string name , ivec3 parameter , int surface )

Sets the value of a given [*ivec3*](../../../api/library/math/class.ivec3_usc.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Parameter name.
- *ivec3* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## ivec3 getMaterialParameterInt3 ( string name , int surface )

Returns the value of a given [*ivec3*](../../../api/library/math/class.ivec3_usc.md) parameter of the surface material.
### Arguments

- *string* **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void setMaterialParameterInt4 ( string name , ivec4 parameter , int surface )

Sets the value of a given [*ivec4*](../../../api/library/math/class.ivec4_usc.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Parameter name.
- *ivec4* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## ivec4 getMaterialParameterInt4 ( string name , int surface )

Returns the value of a given [*ivec4*](../../../api/library/math/class.ivec4_usc.md) parameter of the surface material.
### Arguments

- *string* **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void setMaterialParameterFloat ( string name , float parameter , int surface )

Sets the value of a given float parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Parameter name.
- *float* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## float getMaterialParameterFloat ( string name , int surface )

Returns the value of a given float parameter of the surface material.
### Arguments

- *string* **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void setMaterialParameterFloat2 ( string name , vec2 parameter , int surface )

Sets the value of a given [*vec2*](../../../api/library/math/class.vec2_usc.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Parameter name.
- *vec2* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## vec2 getMaterialParameterFloat2 ( string name , int surface )

Returns the value of a given [*vec2*](../../../api/library/math/class.vec2_usc.md) parameter of the surface material.
### Arguments

- *string* **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void setMaterialParameterFloat3 ( string name , vec3 parameter , int surface )

Sets the value of a given [*vec3*](../../../api/library/math/class.vec3_usc.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Parameter name.
- *vec3* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## vec3 getMaterialParameterFloat3 ( string name , int surface )

Returns the value of a given [*vec3*](../../../api/library/math/class.vec3_usc.md) parameter of the surface material.
### Arguments

- *string* **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void setMaterialParameterFloat4 ( string name , vec4 parameter , int surface )

Sets the value of a given [*vec4*](../../../api/library/math/class.vec4_usc.md) parameter of the surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Parameter name.
- *vec4* **parameter** - Parameter value.
- *int* **surface** - Surface number.

## vec4 getMaterialParameterFloat4 ( string name , int surface )

Returns the value of a given [*vec4*](../../../api/library/math/class.vec4_usc.md) parameter of the surface material.
### Arguments

- *string* **name** - Parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value.
## void setMaterialState ( string name , int state , int surface )

Sets the state value for a given surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Material state name.
- *int* **state** - State value.
- *int* **surface** - Surface number.

## int getMaterialState ( string name , int surface )

Returns the state value of a given surface material.
### Arguments

- *string* **name** - Material state name.
- *int* **surface** - Surface number.

### Return value

State value.
## void setMaterialTexture ( string name , string texture , int surface )

Sets the path to a given texture of a given surface material.
> **Notice:** When called for the first time, this method creates a copy of the source material (which is equal to the [getMaterialInherit](#getMaterialInherit_int_Material) method).


### Arguments

- *string* **name** - Material texture name.
- *string* **texture** - Path to the texture file.
- *int* **surface** - Surface number.

## string getMaterialTexture ( string name , int surface )

Returns the path to a given texture of a given surface material.
### Arguments

- *string* **name** - Material texture name.
- *int* **surface** - Surface number.

### Return value

Path to the texture file.
## void setMinVisibleDistance ( float distance , int surface )

Updates the minimum visibility distance of a given surface. It is the distance, starting from which the surface begins to [fade in](#setMinFadeDistance_float_int_void) until it becomes completely visible.
### Arguments

- *float* **distance** - Minimum visibility distance, in units. If a negative value is provided, **0** will be used instead. The default value is -inf.
- *int* **surface** - Surface number.

## float getMinVisibleDistance ( int surface )

Returns minimum visibility distance of a given surface. It is the distance, starting from which the surface begins to [fade in](#setMinFadeDistance_float_int_void) until it becomes completely visible.
### Arguments

- *int* **surface** - Surface number.

### Return value

Minimum visibility distance, in units.
## void setExperimentalNavigation ( int enabled , int surface )

Sets a value indicating if a given surface contributes to the walkable surface when an [ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_usc.md) is baked. Marking geometry is opt-in: a surface takes part in baking only when this flag is set, which keeps decoration and clutter out of the navigation mesh.
### Arguments

- *int* **enabled** - Navigation flag. The default value is false.
- *int* **surface** - Surface number.

## int getExperimentalNavigation ( int surface )

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

## int getExperimentalNavigationBakeMask ( int surface )

Returns the bake mask of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Bake mask of the surface.
## void setExperimentalNavigationArea ( int area , int surface )

Sets the area stamped onto the navigation mesh polygons baked from a given surface. It is how a road, a patch of mud, or a metal walkway gets its own traversal cost without a volume being placed over it.
### Arguments

- *int* **area** - Area index from the registry of the [ExperimentalNavigation](../../../api/library/pathfinding/class.experimentalnavigation_usc.md) singleton. The default value is 63.
- *int* **surface** - Surface number.

## int getExperimentalNavigationArea ( int surface )

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

## float getMaxVisibleDistance ( int surface )

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

## float getMinFadeDistance ( int surface )

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

## float getMaxFadeDistance ( int surface )

Returns the maximum fade-out distance. Over this distance the surface smoothly becomes invisible due to [alpha fading](../../../code/console/index.md#render_alpha_fade). It is counted starting from the [maximum visibility distance](#getMaxVisibleDistance_int_float).
### Arguments

- *int* **surface** - Surface number.

### Return value

Maximum fade-out distance, in units.
## void setMinParent ( int parent , int surface )

Updates the number of hierarchy levels up to the reference object, which is used to measure the [minimum visible distance from.](#setMinVisibleDistance_float_int_void):
- **0** is the current surface
- **1** is the object to which the surface belongs
- higher values are to move higher up the hierarchy to node parents


### Arguments

- *int* **parent** - Number of hierarchy levels. If a negative value is provided, **0** will be used instead.
- *int* **surface** - Surface number.

## int getMinParent ( int surface )

Returns the number of hierarchy levels up to the reference object, which is used to measure the [minimum visible distance from.](#setMinVisibleDistance_float_int_void):
- **0** is the current surface
- **1** is the object to which the surface belongs
- higher values are to move higher up the hierarchy to node parents

 Returns the surface minimum LOD parent surface number.
### Arguments

- *int* **surface** - Surface number.

### Return value

Number of hierarchy levels.
## void setMaxParent ( int parent , int surface )

Updates the number of hierarchy levels up to the reference object, which is used to measure the [maximum visibility distance from.](#setMaxVisibleDistance_float_int_void):
- **0** is the current surface
- **1** is the object to which the surface belongs
- higher values are to move higher up the hierarchy to node parents


### Arguments

- *int* **parent** - Number of hierarchy levels. If a negative value is provided, **0** will be used instead.
- *int* **surface** - Surface number.

## int getMaxParent ( int surface )

Returns the number of hierarchy levels up to the reference object, which is used to measure the [maximum visibility distance from.](#setMaxVisibleDistance_float_int_void):
- **0** is the current surface
- **1** is the object to which the surface belongs
- higher values are to move higher up the hierarchy to node parents


### Arguments

- *int* **surface** - Surface number.

### Return value

Number of hierarchy levels.
## int getNumTriangles ( int surface )

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

## int getParent ( int surface )

Returns the number of the parent surface for a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Parent surface number. If -1 is returned, the parent surface is not specified for a given surface.
## int setSurfaceProperty ( variable surface )

Sets a new property for a given surface.
### Arguments

- *variable* **surface** - Number of the surface (*int*) or pattern (string with [a regular expression](../../../api/library/common/class.regexp_usc.md#intro)), against which surface names will be matched.

### Return value

1 if the property is set successfully; otherwise, 0.
## int setSurfaceProperty ( int surface )

Sets a new property for the specified surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

1 if the property is set successfully; otherwise, 0.
## int setSurfaceProperty ( )

Sets a new property for the specified surface(s).
### Arguments

### Return value

1 if the property is set successfully; otherwise, 0.
## int setSurfaceProperty ( int surface )

Sets a new property for the specified surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

1 if the property is set successfully; otherwise, 0.
## int setSurfaceProperty ( )

Sets a new property for the specified surface(s).
### Arguments

### Return value

1 if the property is set successfully; otherwise, 0.
## Property getSurfaceProperty ( int surface )

Returns the property defined for a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Property used for the surface.
## Property getSurfacePropertyInherit ( int surface )

Inherits the property for the specific object. All changes of the inherited property will not affect the reference one.
### Arguments

- *int* **surface** - Surface number.

### Return value

The inherited property.
## void clearSurfaceProperty ( int surface )

Removes the assigned property from the specified surface.
### Arguments

- *int* **surface** - Surface number.

## void clearSurfacePropertyInherit ( int surface )

Removes the inherited property and sets back the source(parent) property for the specified surface.
### Arguments

- *int* **surface** - Surface number.

## int isSurfacePropertyInherited ( int surface )

Returns a value indicating if a given property is inherited.
### Arguments

- *int* **surface** - Surface number.

### Return value

Positive number if the surface property is inherited; otherwise, **0**.
## string getSurfacePropertyName ( int surface )

Returns the name of the property of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Property name.
## void setSurfacePropertyParameter ( string name , Variable value , int surface )

Sets the value of a given surface property parameter.
### Arguments

- *string* **name** - Property parameter name.
- *Variable* **value** - Parameter value as a [Variable](../../../api/library/common/class.variable_usc.md).
- *int* **surface** - Surface number.

## Variable getSurfacePropertyParameter ( string name , int surface )

Returns the current value of a given surface property parameter.
### Arguments

- *string* **name** - Property parameter name.
- *int* **surface** - Surface number.

### Return value

Parameter value as a [Variable](../../../api/library/common/class.variable_usc.md).
## string getSurfaceName ( int surface )

Returns the name of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface name.
## void setViewportMask ( int mask , int surface )

Sets a [viewport mask](../../../principles/bit_masking/index.md#viewport) for a given surface. The object surface is rendered, if its mask matches the player (camera) and material masks.
```cpp
// hide the first surface from the camera by disabling all the bits of the mask
obj.setViewportMask(0, 0);

// restore visibility of the surface (the camera must have the first bit of the Viewport mask enabled)
obj.setViewportMask(1, 0);

// enable all the bits by using bitwise NOT
obj.setViewportMask(~0, 0);

// enable ONLY the fifth bit of the mask
obj.setViewportMask(1 << 4, 0);

```


### Arguments

- *int* **mask** - Surface viewport mask.
- *int* **surface** - Surface number.

## int getViewportMask ( int surface )

Returns a viewport mask for a given surface. The object surface is rendered, if its mask matches the player (camera) and material masks.
```cpp
// get the viewport mask of the first surface
int mask = obj.getViewportMask(0);

// check if the fifth bit set
int isBitSet = mask >> 4 & 1;

// check if masks match
int doMasksMatch = mask & mask2 > 0 ? 1 : 0;

```


### Arguments

- *int* **surface** - Surface number.

### Return value

Surface viewport mask.
## WorldBoundBox getWorldBoundBox ( int surface )

Returns the world bounding box of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Bounding box (in world coordinates).
## WorldBoundSphere getWorldBoundSphere ( int surface )

Returns the world bounding sphere of a given surface.
### Arguments

- *int* **surface** - Surface number.

### Return value

Bounding sphere (in world coordinates).
## int findSurface ( string name )

Searches for a surface with a given name.
### Arguments

- *string* **name** - Surface name.

### Return value

Surface number if it exists; otherwise, -1.
## void flushBodyTransform ( )

Forces to set the transformations of the body for the node.
## void setSoundOcclusion ( float occlusion , int surface )

Sets a new sound occlusion value for the specified surface of the object, that determines how much it affects sounds in case of occlusion. For a sound source to be occluded by the specified surface, at least one bit of its [occlusion mask](#setSoundOcclusionMask_int_int_void) should match the [occlusion mask of the sound source](../../../api/library/sounds/class.soundsource_usc.md#setOcclusionMask_int_void).
> **Notice:** [Sound occlusion](../../../api/library/engine/class.sound_usc.md#setSourceOcclusion_int_void) must be enabled.


### Arguments

- *float* **occlusion** - Occlusion value in the range **[0.0f, 1.0f]** to be set for the specified surface. The default value is 0.0f.

  - 0.0f - no occlusion, sound volume will stay the same in case of occlusion by the surface.
  - 1.0f - maximum occlusion, sound will not be heard at all in case of occlusion by the surface.
- *int* **surface** - Surface number.

## float getSoundOcclusion ( int surface )

Returns the current sound occlusion value for the specified surface of the object, that determines how much it affects sounds in case of occlusion. For a sound source to be occluded by the specified surface, at least one bit of its [occlusion mask](#setSoundOcclusionMask_int_int_void) should match the [occlusion mask of the sound source](../../../api/library/sounds/class.soundsource_usc.md#setOcclusionMask_int_void).
> **Notice:** [Sound occlusion](../../../api/library/engine/class.sound_usc.md#setSourceOcclusion_int_void) must be enabled.


### Arguments

- *int* **surface** - Surface number.

### Return value

Current occlusion value in the range **[0.0f, 1.0f]** set for the specified surface.
- 0.0f - no occlusion, sound volume will stay the same in case of occlusion by the surface.
- 1.0f - maximum occlusion, sound will not be heard at all in case of occlusion by the surface.

The default value is 0.0f.
## void setSoundOcclusionMask ( int mask , int surface )

Sets a new sound occlusion mask for the specified surface of the object. For a sound source to be occluded by the specified surface, at least one bit of this mask should match the [occlusion mask of the sound source](../../../api/library/sounds/class.soundsource_usc.md#setOcclusionMask_int_void). Each surface has its own [occlusion value](#setSoundOcclusion_float_int_void), that determines how much it affects sounds in case of occlusion.
> **Notice:** [Sound occlusion](../../../api/library/engine/class.sound_usc.md#setSourceOcclusion_int_void) must be enabled.


### Arguments

- *int* **mask** - Integer, each bit of which is a mask for sound source occlusion.
- *int* **surface** - Surface number.

## int getSoundOcclusionMask ( int surface )

Returns sound occlusion mask for the specified surface of the object. For a sound source to be occluded by the specified surface, at least one bit of this mask should match the [occlusion mask of the sound source](../../../api/library/sounds/class.soundsource_usc.md#setOcclusionMask_int_void). Each surface has its own [occlusion value](#setSoundOcclusion_float_int_void), that determines how much it affects sounds in case of occlusion.
> **Notice:** [Sound occlusion](../../../api/library/engine/class.sound_usc.md#setSourceOcclusion_int_void) must be enabled.


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

## float getPhysicsFriction ( int surface )

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

## float getPhysicsRestitution ( int surface )

Returns the current coefficient of restitution for the specified surface. This coefficient determines the degree of relative kinetic energy retained after a collision. It defines how bouncy the object is by contacting with another object. It depends on the elasticity of the materials of colliding bodies. The simulated restitution, like [friction](#setPhysicsFriction_float_int_void), considers the total value for both objects being in contact.
- The maximum value of 1.0f models elastic collision. Objects bounce off according to the impulse they get by contact.
- The minimum value of 0.0f models inelastic collision. Objects do not bounce at all.

Restitution is calculated by the contact between physical bodies.
### Arguments

- *int* **surface** - Surface number.

### Return value

Current restitution coefficient value in the range **[0.0f, 1.0f]** set for the specified surface.
## void setShadowMode ( int mode , int surface )

Sets the shadow mode for the specified surface. To cast a shadow from a light source (Omni, Proj, or World), the surface's shadow mode should be [adjusted](../../../content/optimization/lights/index.md#static_light) in accordance with the [shadow mode of the light source](../../../api/library/lights/class.light_usc.md#setShadowMode_int_void).
### Arguments

- *int* **mode** - Surface shadow mode, one of the following:

  - [OBJECT_SURFACE_SHADOW_MODE_DYNAMIC](#SURFACE_SHADOW_MODE_DYNAMIC)
  - [OBJECT_SURFACE_SHADOW_MODE_MIXED](#SURFACE_SHADOW_MODE_MIXED)
- *int* **surface** - Target surface number.

## int getShadowMode ( int surface )

Returns the shadow mode set for the specified surface. To cast a shadow from a light source (Omni, Proj, or World), the surface's shadow mode should be [adjusted](../../../content/optimization/lights/index.md#static_light) in accordance with the [shadow mode of the light source](../../../api/library/lights/class.light_usc.md#setShadowMode_int_void).
### Arguments

- *int* **surface** - Target surface number.

### Return value

Surface shadow mode, one of the following:
- [OBJECT_SURFACE_SHADOW_MODE_DYNAMIC](#SURFACE_SHADOW_MODE_DYNAMIC)
- [OBJECT_SURFACE_SHADOW_MODE_MIXED](#SURFACE_SHADOW_MODE_MIXED)


## UGUID getLostMaterialGUID ( int surface )

Returns the [GUID](../../../api/library/filesystem/class.uguid_usc.md) of a lost material. If for some reason a material assigned to the specified surface is missing, this method can be used to get it's GUID.
### Arguments

- *int* **surface** - Target surface number.

### Return value

Lost material [GUID](../../../api/library/filesystem/class.uguid_usc.md).
## UGUID getLostSurfacePropertyGUID ( int surface )

Returns the [GUID](../../../api/library/filesystem/class.uguid_usc.md) of a lost surface property. If for some reason a property assigned to the specified surface is missing, this method can be used to get it's GUID.
### Arguments

- *int* **surface** - Target surface number.

### Return value

Lost property [GUID](../../../api/library/filesystem/class.uguid_usc.md).
## void setLightingMode ( int mode , int surface )

Sets the lighting mode for the specified surface.
### Arguments

- *int* **mode** - Surface lighting mode, one of the following:

  - **0** - STATIC
  - **1** - DYNAMIC
  - **2** - ADVANCED
- *int* **surface** - Target surface number.

## int getLightingMode ( int surface )

Returns the lighting mode for the specified surface.
### Arguments

- *int* **surface** - Target surface number.

### Return value

Surface lighting mode, one of the following:
- **0** - STATIC
- **1** - DYNAMIC
- **2** - ADVANCED


## string getMaterialFilePath ( int surface )

Returns the file path for the material assigned to a given surface.
### Arguments

- *int* **surface** - Target surface number.

### Return value

Material file path.
## UGUID getMaterialGUID ( int surface )

Returns a [GUID](../../../api/library/filesystem/class.uguid_usc.md) of the material for the specified surface.
### Arguments

- *int* **surface** - Target surface number.

### Return value

Material [GUID](../../../api/library/filesystem/class.uguid_usc.md).
## int getSurfaceStatDrawCalls ( int surface )

Returns the number of draw calls (DIP) for the surface with the specified number during the last frame.
### Arguments

- *int* **surface** - Surface number.

### Return value

Number of draw calls (DIP) for the specified surface during the last frame.
## int getSurfaceStatDrawCountViewport ( int surface )

Returns the number of times the surface with the specified number was drawn in the viewport last frame.
### Arguments

- *int* **surface** - Surface number.

### Return value

Number of times the specified surface was drawn in the viewport last frame.
## int getSurfaceStatDrawCountReflection ( int surface )

Returns the number of times the surface with the specified index was drawn during reflections rendering in the last frame.
### Arguments

- *int* **surface** - Surface number.

### Return value

Number of times the specified surface was drawn during reflections rendering in the last frame.
## int getSurfaceStatDrawCountShadow ( int surface )

Returns the number of times the surface with the specified index was drawn during shadows rendering in the last frame.
### Arguments

- *int* **surface** - Surface number.

### Return value

Number of times the specified surface was drawn during shadows rendering in the last frame.
## long getSurfaceStatFrame ( int surface )

Returns the number of [Engine frame](../../../api/library/engine/class.engine_usc.md#getFrame_int64_t), in which the surface with the specified number was drawn last time.
### Arguments

- *int* **surface** - Surface number.

### Return value

Number of frame, in which the specified surface was drawn last time.
## bool isSurfaceRenderCustomParameterOverridden ( int surface , int param )

Checks if the custom surface parameter with the given number is overridden for the given surface of the object.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.

### Return value

**1** if the parameter is overridden for the surface; otherwise, **0**.
## void resetSurfaceRenderCustomParameter ( int surface , int param )

Resets the override of the custom surface parameter with the given number for the given surface: the surface uses the default value from the *[surface parameters layout](../../../api/library/rendering/class.render_usc.md#getSurfaceParameters_CustomParameterLayout)* again.
### Arguments

- *int* **surface** - Surface number.
- *int* **param** - Parameter number.

## void resetSurfaceRenderCustomParameters ( int surface )

Resets the overrides of all custom surface parameters for the given surface of the object.
### Arguments

- *int* **surface** - Surface number.
