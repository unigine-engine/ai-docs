# Unigine.WorldExternBase Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Base


The base class, from which the [custom user-defined worlds](../../../api/library/worlds/class.worldextern_usc.md) are inherited.


## WorldExternBase Class

---

## int getClassID ( )

Returns a unique class ID.
### Return value

Returns a unique class ID.
## Node getNode ( )

Returns the Node smart pointer.
### Return value

Node smart pointer.
## WorldExtern getWorldExtern ( )

Returns the WorldExtern smart pointer.
### Return value

WorldExtern smart pointer.
## int loadWorld ( Xml xml )

Loads a world state from the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - Xml smart pointer.

### Return value

1 if the world state was successfully loaded; otherwise, 0.
## void preRender ( float ifps )

Pre-render function, i.e. after the *update()* and before the *render()* function.
### Arguments

- *float* **ifps** - Inverse FPS value.

## void renderHandler ( )

Renders the handler for the external world.
## void renderVisualizer ( )


Renders the visualizer.


> **Notice:** You should enable the engine visualizer by the **show_visualizer 1** console command.


## int saveState ( Stream stream )


Saves a world state into the stream. Saving into the stream requires creating a blob to save into. To restore the saved state the *[restoreState()](#restoreState_Stream_int)* method is used:


```cpp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
worldExtern1.saveState(blob_state);

// change state
//...//

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
worldExtern1.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream smart pointer.

### Return value

**1** on success; otherwise, **0**.
## int restoreState ( Stream stream )


Restores a world state from the stream. Restoring from the stream requires creating a blob to save into and saving the state using the *[saveState()](#saveState_Stream_int)* method:


```cpp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
worldExtern1.saveState(blob_state);

// change state
//...//

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
worldExtern1.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream smart pointer.

### Return value

**1** on success; otherwise, **0**.
## int saveWorld ( Xml xml )

Saves a world state into the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - Xml smart pointer.

### Return value

1 if the world state was successfully saved; otherwise, 0.
## void update ( float ifps )

Update function. It is called when the node is visible.
### Arguments

- *float* **ifps** - Inverse FPS value.

## void updateEnabled ( )

Updates enabled.
## void updateTransform ( )

Updates transformation matrix of the external world.
## void setUpdateDistanceLimit ( float distance )

Sets the distance from the camera within which the external world should be updated.
### Arguments

- *float* **distance** - Distance from the camera within which the external world should be updated (in units).

## float getUpdateDistanceLimit ( )

Returns the distance from the camera within which the external world should be updated.
### Return value

Distance from the camera within which the external world should be updated (in units).
## void setUpdate ( bool enabled )

Sets a value indicating if the external world should be constantly updated each frame, regardless of the [update distance](#setUpdateDistanceLimit_float_void).
### Arguments

- *bool* **enabled** - true to enable forced updating for the external world; false - to disable forced updating and take the [update distance](#setUpdateDistanceLimit_float_void) into account.

## bool isUpdate ( )

Returns a value indicating if the external world should be constantly updated each frame, regardless of the [update distance](#setUpdateDistanceLimit_float_void).
### Return value

true if the external world is constantly updated each frame; otherwise, false
