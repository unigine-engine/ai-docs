# Unigine.WorldExternBase Class (CS)

**Inherits from:** Base


UNIGINE Base WorldExtern class.


## WorldExternBase Class

### Members

---

## int GetClassID ( )

Returns a unique class ID.
### Return value

Unique class ID.
## Node GetNode ( )

Returns the Node smart pointer.
### Return value

Node smart pointer.
## WorldExtern GetWorldExtern ( )

Returns the WorldExtern smart pointer.
### Return value

WorldExtern smart pointer.
## int LoadWorld ( Xml xml )

Loads a world state from the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Xml smart pointer.

### Return value

1 if the world state was successfully loaded; otherwise, 0.
## void PreRender ( float ifps )

Pre-render function, i.e. after the *update()* and before the *render()* function.
### Arguments

- *float* **ifps** - Inverse FPS value.

## void RenderHandler ( )

Renders the handler for the external world.
## void RenderVisualizer ( )


Renders the visualizer.


> **Notice:** You should enable the engine visualizer by the **show_visualizer 1** console command.


## bool SaveState ( Stream stream )


Saves a world state into the stream. Saving into the stream requires creating a blob to save into. To restore the saved state the *[RestoreState()](#restoreState_Stream_int)* method is used:


```csharp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
worldExtern1.SaveState(blob_state);

// change the node state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
worldExtern1.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream smart pointer.

### Return value

true on success; otherwise, false.
## bool RestoreState ( Stream stream )


Restores a world state from the stream. Restoring from the stream requires creating a blob to save into and saving the state using the *[SaveState()](#saveState_Stream_int)* method:


```csharp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
worldExtern1.SaveState(blob_state);

// change the node state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
worldExtern1.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream smart pointer.

### Return value

true on success; otherwise, false.
## int SaveWorld ( Xml xml )

Saves a world state into the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Xml smart pointer.

### Return value

1 if the world state was successfully saved; otherwise, 0.
## void Update ( float ifps )

Update function. It is called when the node is visible.
### Arguments

- *float* **ifps** - Inverse FPS value.

## void UpdateEnabled ( )

Updates enabled.
## void UpdateTransform ( )

Updates transformation matrix of the external world.
## void SetUpdateDistanceLimit ( float distance )

Sets the distance from the camera within which the external world should be updated.
### Arguments

- *float* **distance** - Distance from the camera within which the external world should be updated (in units).

## float GetUpdateDistanceLimit ( )

Returns the distance from the camera within which the external world should be updated.
### Return value

Distance from the camera within which the external world should be updated (in units).
## void SetUpdate ( bool enabled )

Sets a value indicating if the external world should be constantly updated each frame, regardless of the [update distance](#setUpdateDistanceLimit_float_void).
### Arguments

- *bool* **enabled** - true to enable forced updating for the external world; false - to disable forced updating and take the [update distance](#setUpdateDistanceLimit_float_void) into account.

## bool IsUpdate ( )

Returns a value indicating if the external world should be constantly updated each frame, regardless of the [update distance](#setUpdateDistanceLimit_float_void).
### Return value

true if the external world is constantly updated each frame; otherwise, false
