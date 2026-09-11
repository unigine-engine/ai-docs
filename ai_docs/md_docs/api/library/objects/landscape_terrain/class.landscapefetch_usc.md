# Unigine.LandscapeFetch Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to [fetch](#fetchForce_int) data of the [Landscape Terrain Object](../../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_usc.md) at a certain point (e.g. a height request) or check for an [intersection](#intersectionForce_int) with a traced line. The following performance optimizations are available:


- For each request you can engage or disengage certain data types (albedo, heights, masks, etc.). When the data type is engaged, you can obtain information via the corresponding  . Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
- Both fetch and intersection requests can be performed [asynchronously](#example_async) when an instant result is not required.


The workflow is as follows:


1. Create a new *LandscapeFetch* object instance.
2. Set necessary parameters (e.g. which data layers are to be used, whether to enable holes or not, etc.).
3. To get terrain data for a certain point call the **[fetchForce()()](../../../...md#fetchForce_int)** method providing coordinates for the desired point. > **Notice:** You can also fetch terrain data asynchronously via the **[fetchAsync()()](../../../...md#fetchAsync_int_void)** method.
4. To find an intersection of a traced line with the terrain call either the **[intersectionForce()()](../../../...md#intersectionForce_int)** method or the **[intersectionAsync()()](../../../...md#intersectionAsync_int_void)** method, if you want to perform an asynchronous request.


### Sample Component


### See also


- C++ sample
- C++ sample


## LandscapeFetch Class

### Members

## Vec3 getPosition () const

Returns the current coordinates of the fetch/intersection point.
### Return value

Current fetch/intersection point coordinates as a three-component vector.
## float getHeight () const

Returns the current height value at the point.
### Return value

Current height value at the point.
## vec3 getNormal () const

Returns the current normal vector coordinates at the point.
> **Notice:** To get valid normal information via this method, [engage normal data](#setUsesNormal_int_void) for the fetch/intersection request.


### Return value

Current normal vector coordinates at the point.
## vec4 getAlbedo () const

Returns the current albedo color information at the point.
> **Notice:** To get valid albedo color information via this method, [engage albedo data](#setUsesAlbedo_int_void) for the fetch/intersection request.


### Return value

Current albedo color at the point as a 4 component vector (R, G, B, A).
## int isIntersection () const

Returns the current value indicating if an intersection was detected.
### Return value

Current an intersection was detected
## void setUses ( int uses )

Sets a new flags engaging/disengaging certain data types for the fetch/intersection request.
### Arguments

- *int* **uses** - The combination of data engagement flags.

## int getUses () const

Returns the current flags engaging/disengaging certain data types for the fetch/intersection request.
### Return value

Current combination of data engagement flags.
## void setUsesHeight ( int height )

Sets a new value indicating if heights data is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point). This option is enabled by default.
### Arguments

- *int* **height** - The engagement of height data in the fetch/intersection request

## int isUsesHeight () const

Returns the current value indicating if heights data is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point). This option is enabled by default.
### Return value

Current engagement of height data in the fetch/intersection request
## void setUsesNormal ( int normal )

Sets a new value indicating if normals data is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
> **Notice:** Enable this option to get [normal](#getNormal_vec3) information for the point.


### Arguments

- *int* **normal** - The engagement of normals data in the fetch/intersection request

## int isUsesNormal () const

Returns the current value indicating if normals data is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
> **Notice:** Enable this option to get [normal](#getNormal_vec3) information for the point.


### Return value

Current engagement of normals data in the fetch/intersection request
## void setUsesAlbedo ( int albedo )

Sets a new value indicating if albedo data is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
> **Notice:** Enable this option to get [albedo](#getAlbedo_vec4) information for the point.


### Arguments

- *int* **albedo** - The engagement of albedo data in the fetch/intersection request

## int isUsesAlbedo () const

Returns the current value indicating if albedo data is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
> **Notice:** Enable this option to get [albedo](#getAlbedo_vec4) information for the point.


### Return value

Current engagement of albedo data in the fetch/intersection request
## void setIntersectionPrecision ( float precision )

Sets a new precision value used for intersection detection requested by [*intersectionForce()*](#intersectionForce_int) and [*intersectionAsync()*](#intersectionAsync_int_void) methods.
### Arguments

- *float* **precision** - The precision for intersection detection as a fraction of maximum precision in the [0; 1] range. The default value is 0.5f. Maximum precision is determined by the Engine on the basis of the data of your Landscape Terrain.

## float getIntersectionPrecision () const

Returns the current precision value used for intersection detection requested by [*intersectionForce()*](#intersectionForce_int) and [*intersectionAsync()*](#intersectionAsync_int_void) methods.
### Return value

Current precision for intersection detection as a fraction of maximum precision in the [0; 1] range. The default value is 0.5f. Maximum precision is determined by the Engine on the basis of the data of your Landscape Terrain.
## void setIntersectionPositionBegin ( Vec3 begin )

Sets a new coordinates of the starting point for intersection detection.
### Arguments

- *Vec3* **begin** - The three-component vector specifying starting point coordinates along X, Y, and Z axes.

## Vec3 getIntersectionPositionBegin () const

Returns the current coordinates of the starting point for intersection detection.
### Return value

Current three-component vector specifying starting point coordinates along X, Y, and Z axes.
## void setIntersectionPositionEnd ( Vec3 end )

Sets a new coordinates of the end point for intersection detection.
### Arguments

- *Vec3* **end** - The three-component vector specifying end point coordinates along X, Y, and Z axes.

## Vec3 getIntersectionPositionEnd () const

Returns the current coordinates of the end point for intersection detection.
### Return value

Current three-component vector specifying end point coordinates along X, Y, and Z axes.
## void setFetchPosition ( Vec2 position )

Sets a new point for which terrain data is to be fetched.
### Arguments

- *Vec2* **position** - The two-component vector specifying point coordinates along X and Y axes.

## Vec2 getFetchPosition () const

Returns the current point for which terrain data is to be fetched.
### Return value

Current two-component vector specifying point coordinates along X and Y axes.
## int isAsyncCompleted () const

Returns the current value indicating if async operation is completed. As the operation is completed you can obtain necessary data via *get*()* methods.
### Return value

Current async operation is completed
## void setHolesEnabled ( int enabled )

Sets a new value indicating if checking for terrain holes in the fetch/intersection request is enabled. This option is enabled by default. When disabled terrain holes created using decals are ignored.
### Arguments

- *int* **enabled** - The checking for terrain holes in the fetch/intersection request

## int isHolesEnabled () const

Returns the current value indicating if checking for terrain holes in the fetch/intersection request is enabled. This option is enabled by default. When disabled terrain holes created using decals are ignored.
### Return value

Current checking for terrain holes in the fetch/intersection request
## getEventEnd () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventStart () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## static LandscapeFetch ( )

The LandscapeFetch constructor.
## float getMask ( int num )

Returns information stored for the point in the detail mask with the specified number.
> **Notice:** To get valid detail mask information via this method, [engage mask data](#setUsesMask_int_int_void) for the fetch/intersection request.


### Arguments

- *int* **num** - Number of the detail mask in the **[0; 19]** range.

### Return value

Value for the point stored in the detail mask with the specified number.
## void setUsesMask ( int num , int value )

Sets a value indicating if data of the specified detail mask is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
> **Notice:** Enable this option to get [detail mask](#getMask_int_float) data for the point.


### Arguments

- *int* **num** - Detail mask number in the **[0; 19]** range.
- *int* **value** - **1** to engage data of the specified detail mask in the fetch/intersection request, **0** - to disengage.

## int isUsesMask ( int num )

Returns a value indicating if data of the specified detail mask is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
> **Notice:** Enable this option to get [detail mask](#getMask_int_float) data for the point.


### Arguments

- *int* **num** - Detail mask number in the **[0; 19]** range.

### Return value

**1** if data of the specified detail mask is engaged in the fetch/intersection request; otherwise, **0**.
## int fetchForce ( )

Fetches terrain data in forced mode for the point specified by the [*setFetchPosition()*](#setFetchPosition_Vec2_void). You can use the [*fetchAsync()*](#fetchAsync_int_void) method to reduce load, when an instant result is not required.
### Return value

**1** if terrain data was successfully obtained for the specified point; otherwise, **0**.
## int fetchForce ( Vec2 position )

Fetches terrain data in forced mode for the specified point. You can use the [*fetchAsync()*](#fetchAsync_int_void) method to reduce load, when an instant result is not required.
### Arguments

- *Vec2* **position** - Coordinates of the point.

### Return value

**1** if terrain data was successfully obtained for the specified point; otherwise, **0**.
## int intersectionForce ( )

Performs tracing along the line from the **p0** point specified by the [*setIntersectionPositionBegin()*](#setIntersectionPositionBegin_Vec3_void) to the **p1** point specified by the [*setIntersectionPositionEnd()*](#setIntersectionPositionEnd_Vec3_void) to find an intersection with the terrain in forced mode. You can use the [*intersectionAsync()*](#intersectionAsync_int_void) method to reduce load, when an instant result is not required.
### Return value

**1** if an intersection with the terrain was found; otherwise, **0**.
## int intersectionForce ( Vec3 p0 , Vec3 p1 )

Performs tracing along the line from the **p0** point to the **p1** point to find an intersection with the terrain in forced mode. You can use the [*intersectionAsync()*](#intersectionAsync_int_void) method to reduce load, when an instant result is not required.
### Arguments

- *Vec3* **p0** - Coordinates of the **p0** point.
- *Vec3* **p1** - Coordinates of the **p1** point.

### Return value

**1** if an intersection with the terrain was found; otherwise, **0**.
## void fetchAsync ( int critical = false )

Fetches terrain data for the point specified by the [*setFetchPosition()*](#setFetchPosition_Vec2_void) in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_void) method). For an instant result use the [*fetchForce()*](#fetchForce_int) method.
### Arguments

- *int* **critical** - **1** to set high priority for the fetch task, **0** - to set normal priority.

## void fetchAsync ( Vec2 position , int critical = false )

Fetches terrain data for the specified point in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_void) method). For an instant result use the [*fetchForce()*](#fetchForce_int) method.
### Arguments

- *Vec2* **position** - Coordinates of the point.
- *int* **critical** - **1** to set high priority for the fetch task, **0** - to set normal priority.

## void intersectionAsync ( int critical = false )

Performs tracing along the line from the **p0** point specified by the [*setIntersectionPositionBegin()*](#setIntersectionPositionBegin_Vec3_void) to the **p1** point specified by the [*setIntersectionPositionEnd()*](#setIntersectionPositionEnd_Vec3_void) to find an intersection with the terrain in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_void) method). For an instant result use the [*intersectionForce()*](#intersectionForce_int) method.
### Arguments

- *int* **critical** - **1** to set high priority for the intersection task, **0** - to set normal priority.

## void intersectionAsync ( Vec3 p0 , Vec3 p1 , int critical = false )

Performs tracing along the line from the **p0** point to the **p1** point to find an intersection with the terrain in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_void) method). For an instant result use the [*intersectionForce()*](#intersectionForce_int) method.
### Arguments

- *Vec3* **p0** - Coordinates of the **p0** point.
- *Vec3* **p1** - Coordinates of the **p1** point.
- *int* **critical** - **1** to set high priority for the intersection task, **0** - to set normal priority.

## void fetchForce ( Vector< LandscapeFetch > fetches )

Fetches (batch) terrain data in forced mode for the point specified by the [*setFetchPosition()*](#setFetchPosition_Vec2_void). You can use the [*fetchAsync()*](#fetchAsync_VECLandscapeFetch_int_void) method to reduce load, when an instant result is not required.
### Arguments

- *Vector<[LandscapeFetch](../../../../api/library/objects/landscape_terrain/class.landscapefetch_usc.md)>* **fetches** - List of fetch requests to be completed.

## void intersectionForce ( Vector< LandscapeFetch > fetches )

Performs tracing (batch) along the line from the **p0** point specified by the [*setIntersectionPositionBegin()*](#setIntersectionPositionBegin_Vec3_void) to the **p1** point specified by the [*setIntersectionPositionEnd()*](#setIntersectionPositionEnd_Vec3_void) to find an intersection with the terrain in forced mode. You can use the [*intersectionAsync()*](#intersectionAsync_VECLandscapeFetch_int_void) method to reduce load, when an instant result is not required.
### Arguments

- *Vector<[LandscapeFetch](../../../../api/library/objects/landscape_terrain/class.landscapefetch_usc.md)>* **fetches** - List of fetch requests to be completed.

## void fetchAsync ( Vector< LandscapeFetch > fetches , int critical = false )

Fetches (batch) terrain data for the point specified by the [*setFetchPosition()*](#setFetchPosition_Vec2_void) in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_VECLandscapeFetch_void) method). For an instant result use the [*fetchForce()*](#fetchForce_VECLandscapeFetch_void) method.
### Arguments

- *Vector<[LandscapeFetch](../../../../api/library/objects/landscape_terrain/class.landscapefetch_usc.md)>* **fetches** - List of fetch requests to be completed.
- *int* **critical** - **1** to set high priority for the fetch task, **0** - to set normal priority.

## void intersectionAsync ( Vector< LandscapeFetch > fetches , int critical = false )

Performs tracing (batch) along the line from the **p0** point specified by the [*setIntersectionPositionBegin()*](#setIntersectionPositionBegin_Vec3_void) to the **p1** point specified by the [*setIntersectionPositionEnd()*](#setIntersectionPositionEnd_Vec3_void) to find an intersection with the terrain in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_VECLandscapeFetch_void) method). For an instant result use the [*intersectionForce()*](#intersectionForce_VECLandscapeFetch_void) method.
### Arguments

- *Vector<[LandscapeFetch](../../../../api/library/objects/landscape_terrain/class.landscapefetch_usc.md)>* **fetches** - List of fetch requests to be completed.
- *int* **critical** - **1** to set high priority for the intersection task, **0** - to set normal priority.

## void wait ( )

Waits for completion of the fetch operation. As the operation is completed you can obtain necessary data via *get*()* methods.
## void wait ( Vector< LandscapeFetch > fetches )

Waits for completion of the specified fetch operations. As the operations are completed you can obtain necessary data via *get*()* methods.
### Arguments

- *Vector<[LandscapeFetch](../../../../api/library/objects/landscape_terrain/class.landscapefetch_usc.md)>* **fetches** - List of fetch requests to be completed.
