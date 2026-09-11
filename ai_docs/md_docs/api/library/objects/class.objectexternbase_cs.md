# ObjectExternBase Class (CS)

**Inherits from:** Base


The base class, from which the [custom user-defined objects](../../../api/library/objects/class.objectextern_cs.md) are inherited.


## ObjectExternBase Class

### Members

---

## int GetClassID ( )

Returns a unique class ID.
### Return value

Unique class ID.
## int GetCollision ( vec3 p0 , vec3 p1 , int[] OUT_surfaces )

Spatial collision with the bounding box.
### Arguments

- *vec3* **p0** - Coordinates of the start point of the line.
- *vec3* **p1** - Coordinates of the end point of the line.
- *int[]* **OUT_surfaces** - Return array with surface numbers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Returns **1** if the array of surfaces is not empty.
## int GetCollision ( BoundBox bb , int[] OUT_surfaces )

Spatial collision with the bounding box.
### Arguments

- *[BoundBox](../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.
- *int[]* **OUT_surfaces** - Return array with surface numbers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Returns **1** if the array of surfaces is not empty.
## int GetIntersection ( vec3 p0 , vec3 p1 , vec3[] OUT_ret_point , vec3[] OUT_ret_normal , vec4[] OUT_ret_texcoord , int[] OUT_ret_index , int[] OUT_ret_instance , int surface )

Returns a value indicating that the line intersects the object surface.
### Arguments

- *vec3* **p0** - Coordinates of the start point of the line.
- *vec3* **p1** - Coordinates of the end point of the line.
- *vec3[]* **OUT_ret_point** - Intersection point coordinates. Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *vec3[]* **OUT_ret_normal** - Intersection normal vector. Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *vec4[]* **OUT_ret_texcoord** - Intersection texture coordinates. Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int[]* **OUT_ret_index** - Intersected triangle number. Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int[]* **OUT_ret_instance** - Intersected instance number. Pass NULL if this parameter is not required. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **surface** - Surface number.

### Return value

Returns **1** if the intersection occurs.
## Node GetNode ( )

Returns the Node smart pointer.
### Return value

Node smart pointer.
## int GetNumSurfaces ( )

Returns the number of object surfaces.
### Return value

The number of object surfaces.
## int GetNumTriangles ( int surface )

Returns the number of triangles.
### Arguments

- *int* **surface** - Surface number.

### Return value

Returns the number of triangles.
## Object GetObject ( )

Returns the Object smart pointer.
### Return value

Object smart pointer.
## ObjectExtern GetObjectExtern ( )

Returns the ObjectExtern smart pointer.
### Return value

ObjectExtern smart pointer.
## int GetOrder ( vec3 camera , int surface )

Returns the rendering order with respect to the camera position.
### Arguments

- *vec3* **camera** - World camera position.
- *int* **surface** - Surface number.

### Return value

Surface rendering order.
## int GetRandomPoint ( out vec3 ret_point , out vec3 ret_normal , out vec3 ret_velocity , int surface )

Returns a random point from a surface.
### Arguments

- *out vec3* **ret_point** - Random point coordinates.
- *out vec3* **ret_normal** - Random normal vector.
- *out vec3* **ret_velocity** - Random velocity vector.
- *int* **surface** - Surface number.

### Return value

Returns **1** if the random point is valid.
## int GetResource ( int surface )

Returns the unique render resource identifier.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface resource identifier.
## int GetSequence ( vec3 camera , int surface )

Returns the rendering sequence with respect to the camera position.
### Arguments

- *vec3* **camera** - World camera position.
- *int* **surface** - Surface number.

### Return value

Surface rendering sequence.
## string GetSurfaceName ( int surface )

Returns the object surface name.
### Arguments

- *int* **surface** - Surface number.

### Return value

Surface name.
## float GetTransparentDistance ( vec3 camera , int surface )

Returns the transparent rendering distance.
### Arguments

- *vec3* **camera** - World camera position.
- *int* **surface** - Surface number.

### Return value

Surface rendering distance.
## void Create ( int surface )

Renders a create function.
### Arguments

- *int* **surface** - Surface number.

## int FindSurface ( string name )

Returns the number of the object surface by its name.
### Arguments

- *string* **name** - Surface name.

### Return value

Surface number.
## bool HasCreate ( )

Returns a value indicating that the object has a create function.
### Return value

true if the object has a create function; otherwise, false.
## bool HasLods ( )

Returns a value indicating if the object has LODs.
### Return value

true if the object has surface LODs; otherwise, false.
## bool HasRender ( )

Returns a value indicating that the object has a render function.
### Return value

true if the object has a render function; otherwise, false.
## bool HasShadow ( )

Returns a value indicating that the object has a shadow function.
### Return value

true if the object has a shadow function; otherwise, false.
## int LoadWorld ( Xml xml )

Loads an object state from the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Xml smart pointer.

### Return value

Returns **1** if the object state was successfully loaded; otherwise, **0** is returned.
## void PreRender ( float ifps )

Pre-render function, i.e. after the *update()* and before the *render()* function. This method can be used to make necessary preparations for rendering (e.g. prepare a texture) after the *update()*.
### Arguments

- *float* **ifps** - Inverse FPS value.

## void Render ( Render.PASS pass , int surface )

Renders the render function.
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass.
- *int* **surface** - Surface number.

## void RenderHandler ( )

Renders the handler.
## void RenderShadow ( Render.PASS pass , int surface )

Renders render function.
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass.
- *int* **surface** - Surface number.

## void RenderVisualizer ( )

Renders the visualizer.
> **Notice:** You should enable the engine visualizer by the **show_visualizer 1** console command.


## void ResizeSurfaces ( )

Resizes all of the object surfaces.
## int SaveState ( Stream stream )

Saves an object state into the stream.
Saving into the stream requires creating a blob to save into. To restore the saved state the [restoreState()](#restoreState_Stream_int) method is used:


```csharp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
object.SaveState(blob_state);

// change the node state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
object.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream smart pointer.

### Return value

Returns **1** if the object state was successfully saved into the stream; otherwise, **0** is returned.
## int RestoreState ( Stream stream )

Restores an object state from the stream.
Restoring from the stream requires creating a blob to save into and saving the state using the [saveState()](#saveState_Stream_int) method:


```csharp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
object.SaveState(blob_state);

// change the node state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
object.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream smart pointer.

### Return value

Returns **1** if the object state was successfully restored from the stream; otherwise, **0** is returned.
## int SaveWorld ( Xml xml )

Saves an object state into the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Xml smart pointer.

### Return value

Returns **1** if the object state was successfully saved; otherwise, **0** is returned.
## void Update ( float ifps )

Update function.
### Arguments

- *float* **ifps** - Inverse FPS value.

## void UpdateEnabled ( )

Updates enabled.
## void UpdateEnabled ( int surface )

Updates enabled.
### Arguments

- *int* **surface** - Surface number.

## void UpdateSurfaces ( )

Updates all of the object surfaces.
## void UpdateTransform ( )

Updates transformation.
## void SetUpdateDistanceLimit ( float distance )

Sets the distance from the camera within which the object should be updated.
### Arguments

- *float* **distance** - Distance from the camera within which the object should be updated (in units).

## float GetUpdateDistanceLimit ( )

Returns the distance from the camera within which the object should be updated.
### Return value

Distance from the camera within which the object should be updated (in units).
## void SetForceUpdate ( bool enabled )

Sets a value indicating if the object should be constantly updated each frame, regardless of the [update distance](#setUpdateDistanceLimit_float_void).
### Arguments

- *bool* **enabled** - true to enable forced updating for the object; false - to disable forced updating and take the [update distance](#setUpdateDistanceLimit_float_void) into account.

## bool IsForceUpdate ( )

Returns a value indicating if the object should be constantly updated each frame, regardless of the [update distance](#setUpdateDistanceLimit_float_void).
### Return value

true if the object is constantly updated each frame; otherwise, false
