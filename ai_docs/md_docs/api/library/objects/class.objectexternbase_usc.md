# ObjectExternBase Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Base


The base class, from which the [custom user-defined objects](../../../api/library/objects/class.objectextern_usc.md) are inherited.


## ObjectExternBase Class

---

## int getClassID ( )

Returns a unique class ID.
### Return value

Unique class ID.
## int getCollision ( Vec3 p0 , Vec3 p1 , Vector<int>& OUT_surfaces )

Spatial collision with the bounding box.
### Arguments

- *Vec3* **p0** - Coordinates of the start point of the line.
- *Vec3* **p1** - Coordinates of the end point of the line.
- *Vector<int>&* **OUT_surfaces** - Return array with surface numbers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Returns **1** if the array of surfaces is not empty.
## int getCollision ( BoundBox bb , Vector<int>& OUT_surfaces )

Spatial collision with the bounding box.
### Arguments

- *BoundBox* **bb** - Bounding box.
- *Vector<int>&* **OUT_surfaces** - Return array with surface numbers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Returns **1** if the array of surfaces is not empty.
## int getIntersection ( Vec3 p0 , Vec3 p1 , Vec3 * OUT_ret_point , vec3 * OUT_ret_normal , vec4 * OUT_ret_texcoord , int * OUT_ret_index , int * OUT_ret_instance , int surface )

Returns a value indicating that the line intersects the object surface.
### Arguments

- *Vec3* **p0** - Coordinates of the start point of the line.
- *Vec3* **p1** - Coordinates of the end point of the line.
- *Vec3 ** **OUT_ret_point** - Intersection point coordinates. Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *vec3 ** **OUT_ret_normal** - Intersection normal vector. Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *vec4 ** **OUT_ret_texcoord** - Intersection texture coordinates. Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int ** **OUT_ret_index** - Intersected triangle number. Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int ** **OUT_ret_instance** - Intersected instance number. Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **surface** - Surface number.

### Return value

Returns **1** if the intersection occurs.
## Node getNode ( )

Returns the Node smart pointer.
### Return value

Node smart pointer.
## int getNumSurfaces ( )

Returns the number of object surfaces.
### Return value

The number of object surfaces.
## int getNumTriangles ( int surface )

Returns the number of triangles.
### Arguments

- *int* **surface** - Surface number.

### Return value

Returns the number of triangles.
## Object getObject ( )

Returns the Object smart pointer.
### Return value

Object smart pointer.
## ObjectExtern getObjectExtern ( )

Returns the ObjectExtern smart pointer.
### Return value

ObjectExtern smart pointer.
## int getOrder ( Vec3 camera , int surface )

Returns the rendering order with respect to the camera position.
### Arguments

- *Vec3* **camera** - World camera position.
- *int* **surface** - Surface number.

### Return value

Surface rendering order.
## int getRandomPoint ( vec3 & ret_point , vec3 & ret_normal , vec3 & ret_velocity , int surface )

Returns a random point from a surface.
### Arguments

- *vec3 &* **ret_point** - Random point coordinates.
- *vec3 &* **ret_normal** - Random normal vector.
- *vec3 &* **ret_velocity** - Random velocity vector.
- *int* **surface** - Surface number.

### Return value

Returns **1** if the random point is valid.
## int getResource ( int surface )

Returns the unique render resource identifier.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface resource identifier.
## int getSequence ( Vec3 camera , int surface )

Returns the rendering sequence with respect to the camera position.
### Arguments

- *Vec3* **camera** - World camera position.
- *int* **surface** - Surface number.

### Return value

Surface rendering sequence.
## string getSurfaceName ( int surface )

Returns the object surface name.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface name.
## float getTransparentDistance ( Vec3 camera , int surface )

Returns the transparent rendering distance.
### Arguments

- *Vec3* **camera** - World camera position.
- *int* **surface** - Surface number.

### Return value

Surface rendering distance.
## void create ( int surface )

Renders a create function.
### Arguments

- *int* **surface** - Surface number.

## int findSurface ( string name )

Returns the number of the object surface by its name.
### Arguments

- *string* **name** - Surface name.

### Return value

Surface number.
## int hasCreate ( )

Returns a value indicating that the object has a create function.
### Return value

**1** if the object has a create function; otherwise, **0**.
## int hasLods ( )

Returns a value indicating if the object has LODs.
### Return value

**1** if the object has surface LODs; otherwise, **0**.
## int hasRender ( )

Returns a value indicating that the object has a render function.
### Return value

**1** if the object has a render function; otherwise, **0**.
## int hasShadow ( )

Returns a value indicating that the object has a shadow function.
### Return value

**1** if the object has a shadow function; otherwise, **0**.
## int loadWorld ( Xml xml )

Loads an object state from the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - Xml smart pointer.

### Return value

Returns **1** if the object state was successfully loaded; otherwise, **0** is returned.
## void preRender ( float ifps )

Pre-render function, i.e. after the *update()* and before the *render()* function. This method can be used to make necessary preparations for rendering (e.g. prepare a texture) after the *update()*.
### Arguments

- *float* **ifps** - Inverse FPS value.

## void render ( int pass , int surface )

Renders the render function.
### Arguments

- *int* **pass** - Rendering pass.
- *int* **surface** - Surface number.

## void renderHandler ( )

Renders the handler.
## void renderShadow ( int pass , int surface )

Renders render function.
### Arguments

- *int* **pass** - Rendering pass.
- *int* **surface** - Surface number.

## void renderVisualizer ( )

Renders the visualizer.
> **Notice:** You should enable the engine visualizer by the **show_visualizer 1** console command.


## void resizeSurfaces ( )

Resizes all of the object surfaces.
## int saveState ( Stream stream )

Saves an object state into the stream.
Saving into the stream requires creating a blob to save into. To restore the saved state the [restoreState()](#restoreState_Stream_int) method is used:


```cpp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
object.saveState(blob_state);

// change state
//...//

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
object.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream smart pointer.

### Return value

Returns **1** if the object state was successfully saved into the stream; otherwise, **0** is returned.
## int restoreState ( Stream stream )

Restores an object state from the stream.
Restoring from the stream requires creating a blob to save into and saving the state using the [saveState()](#saveState_Stream_int) method:


```cpp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
object.saveState(blob_state);

// change state
//...//

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
object.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream smart pointer.

### Return value

Returns **1** if the object state was successfully restored from the stream; otherwise, **0** is returned.
## int saveWorld ( Xml xml )

Saves an object state into the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - Xml smart pointer.

### Return value

Returns **1** if the object state was successfully saved; otherwise, **0** is returned.
## void update ( float ifps )

Update function.
### Arguments

- *float* **ifps** - Inverse FPS value.

## void updateEnabled ( )

Updates enabled.
## void updateEnabled ( int surface )

Updates enabled.
### Arguments

- *int* **surface** - Surface number.

## void updateSurfaces ( )

Updates all of the object surfaces.
## void updateTransform ( )

Updates transformation.
## void setUpdateDistanceLimit ( float distance )

Sets the distance from the camera within which the object should be updated.
### Arguments

- *float* **distance** - Distance from the camera within which the object should be updated (in units).

## float getUpdateDistanceLimit ( )

Returns the distance from the camera within which the object should be updated.
### Return value

Distance from the camera within which the object should be updated (in units).
## void setForceUpdate ( bool enabled )

Sets a value indicating if the object should be constantly updated each frame, regardless of the [update distance](#setUpdateDistanceLimit_float_void).
### Arguments

- *bool* **enabled** - true to enable forced updating for the object; false - to disable forced updating and take the [update distance](#setUpdateDistanceLimit_float_void) into account.

## bool isForceUpdate ( )

Returns a value indicating if the object should be constantly updated each frame, regardless of the [update distance](#setUpdateDistanceLimit_float_void).
### Return value

true if the object is constantly updated each frame; otherwise, false
