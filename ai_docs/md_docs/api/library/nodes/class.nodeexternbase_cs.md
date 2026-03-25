# Unigine::NodeExternBase Class (CS)

**Inherits from:** Base


The base class that is used to implement logic of [custom user-defined nodes](../../../api/library/nodes/class.nodeextern_cs.md). The custom node class should be inherited from NodeExternBase.


## NodeExternBase Class

### Members

---

## int GetClassID ( )

Returns a unique class ID.
### Return value

Unique class ID.
## Node GetNode ( )

Returns the Node instance.
### Return value

Node.
## NodeExtern GetNodeExtern ( )

Returns the [NodeExtern](../../../api/library/nodes/class.nodeextern_cs.md) instance that is created on loading the custom node.
### Return value

NodeExtern.
## int LoadWorld ( Xml xml )

Loads a node state from the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Xml smart pointer.

### Return value

Returns 1 if the node state was successfully loaded; otherwise, 0 is returned.
## void RenderHandler ( )

Renders the handler for the custom user-defined node.
## void RenderVisualizer ( )

Renders the visualizer for the custom user-defined node.
> **Notice:** You should enable the engine visualizer by the **show_visualizer 1** console command.


## bool SaveState ( Stream stream )

Saves a node state into the stream.
Saving into the stream requires creating a blob to save into. To restore the saved state the [RestoreState()](#restoreState_Stream_int) method is used:


```csharp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
node.SaveState(blob_state);

// change the node state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
node.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream smart pointer.

### Return value

true on success; otherwise, false.
## bool RestoreState ( Stream stream )

Restores a node state from the stream.
Restoring from the stream requires creating a blob to save into and saving the state using the [SaveState()](#saveState_Stream_int) method:


```csharp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
node.SaveState(blob_state);

// change the node state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
node.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream smart pointer.

### Return value

true on success; otherwise, false.
## int SaveWorld ( Xml xml )

Saves a node state into the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Xml smart pointer.

### Return value

1 if the node state was successfully saved; otherwise, 0 is returned.
## void UpdateEnabled ( )

Updates enabled.
## void UpdateTransform ( )

Updates transformation matrix of the custom node.
