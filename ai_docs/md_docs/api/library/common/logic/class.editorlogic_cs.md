# Unigine::EditorLogic Class (CS)


The *EditorLogic* class is used to control the logic of the editor. Methods of this class are called after corresponding methods of the editor script.


EditorLogic class methods are called only if the [UnigineEditor](../../../../editor2/index.md) is loaded.


## EditorLogic Class

### Members

---

## virtual bool Init ( )

Engine calls this function on editor initialization. Similar to the editor script's init() function.
### Return value

true if the editor is initialized successfully; otherwise, false.
## virtual bool Shutdown ( )

Engine calls this function on editor shutdown. Similar to the editor script's *shutdown()* function.
### Return value

true if the editor shutdown is performed successfully; otherwise, false.
## virtual bool Update ( )

Engine calls this function before updating each render frame when editor is loaded. Similar to the editor script's *update()* function.
### Return value

true if there were no errors during the editor update; otherwise, false.
## virtual bool PostUpdate ( )

Engine calls this function after updating each render frame when editor is loaded. Similar to the editor script's *postUpdate()* function.
### Return value

true if there were no errors during the editor post update; otherwise, false.
## virtual bool Render ( EngineWindowViewport window )

Engine calls this function before rendering each render frame for the specified Engine window, when editor is loaded. Similar to the editor script's *render()* function.
### Arguments

- *[EngineWindowViewport](../../../../api/library/gui/class.enginewindowviewport_cs.md)* **window** - Target Engine window viewport.

### Return value

true if there were no errors during the editor rendering; otherwise, false.
## virtual bool WorldInit ( )

Engine calls this function on world initialization when editor is loaded. This function is similar to the editor script's *worldInit()* function.
### Return value

true if there were no errors during the world initialization; otherwise, false.
## virtual bool WorldShutdown ( )

Engine calls this function on world shutdown when editor is loaded. Similar to the editor script's *worldShutdown()* function.
### Return value

true if there were no errors during the world shutdown; otherwise, false.
## virtual bool WorldSave ( )

Engine calls this function on world save when editor is loaded. Similar to the editor script's *worldSave()* function.
### Return value

true if there were no errors during the world saving; otherwise, false.
## virtual void Clear ( )

A callback on world reloading and clearing nodes list.
## virtual void nodeReparented ( const Node Ptr & node )


Callback called on node reparenting.


```csharp
override void NodeReparented(Node node) {
	if(node.Name == "my_node") {
		Log.Message("The parent of the node my_node has been changed\n");
	}
}

```


### Arguments

- *const [Node](../../../../api/library/nodes/class.node_cs.md)Ptr &* **node** - Node.

## virtual void nodeReordered ( const Node Ptr & node )


Callback called on node reordering.


```csharp
override void NodeReordered(Node node) {
	if(node.Name == "my_node") {
		Log.Message("The node my_node is reordered\n");
	}
}

```


### Arguments

- *const [Node](../../../../api/library/nodes/class.node_cs.md)Ptr &* **node** - Node.

## virtual void nodeRenamed ( const Node Ptr & node , const char * old_name )


Callback called on node renaming.


```csharp
override void NodeRenamed(Node node, string old_name) {
	if (old_name == "my_node") {
		Log.Message("The node my_node has been renamed\n");
		Log.Message("The new name of the node is {0}\n",node.getName());
	}
}

```


### Arguments

- *const [Node](../../../../api/library/nodes/class.node_cs.md)Ptr &* **node** - Node.
- *const char ** **old_name** - Old name of the renamed node.

## virtual void nodeShowInEditorChanged ( const Node Ptr & node )


Callback called on changing displaying in world hierarchy option for a node.


```csharp
override void nodeShowInEditorChanged(Node node) {
	if (node.GetName() == "my_node") {
		Log.Message("Displaying in world hierarchy has changed for the my_node node\n");
	}
}

```


### Arguments

- *const [Node](../../../../api/library/nodes/class.node_cs.md)Ptr &* **node** - Node.

## virtual void materialAdded ( const UGUID & guid )

Callback called on adding a material.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cs.md) &* **guid** - Material [GUID](../../../../api/library/filesystem/class.uguid_cs.md).

## virtual void materialRemoved ( const UGUID & guid )

Callback called on removing a material.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cs.md) &* **guid** - Material [GUID](../../../../api/library/filesystem/class.uguid_cs.md).

## virtual void materialChanged ( const UGUID & guid )

Callback called on changing a material.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cs.md) &* **guid** - Material [GUID](../../../../api/library/filesystem/class.uguid_cs.md).

## virtual void materialReparented ( const UGUID & guid , const UGUID & old_parent , const UGUID & new_parent )

Callback called on changing material's parent.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cs.md) &* **guid** - Material [GUID](../../../../api/library/filesystem/class.uguid_cs.md).
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cs.md) &* **old_parent** - Old parent material [GUID](../../../../api/library/filesystem/class.uguid_cs.md).
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cs.md) &* **new_parent** - New parent material [GUID](../../../../api/library/filesystem/class.uguid_cs.md).

## virtual void propertyAdded ( const UGUID & guid )


Callback called on adding a property.


> **Notice:** Callbacks are triggered for all properties, including [hidden](../../../../code/formats/property_format.md#property_hidden) ones.

### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cs.md) &* **guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the property added.

## virtual void propertyRemoved ( const UGUID & guid )


Callback called on removing a property.


> **Notice:** Callbacks are triggered for all properties, including [hidden](../../../../code/formats/property_format.md#property_hidden) ones.

### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cs.md) &* **guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the property removed.

## virtual void propertyMoved ( const UGUID & guid )

Callback called on moving a property.
> **Notice:** Callbacks are triggered for all properties, including [hidden](../../../../code/formats/property_format.md#property_hidden) ones.

### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cs.md) &* **guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the property moved.

## virtual void propertyChanged ( const UGUID & guid )


Callback called on changing a property.


> **Notice:** Callbacks are triggered for all properties, including [hidden](../../../../code/formats/property_format.md#property_hidden) ones.

### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cs.md) &* **guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the property changed.

## virtual void propertyReparented ( const UGUID & guid , const UGUID & old_parent , const UGUID & new_parent )


Callback called on changing property's parent.


> **Notice:** Callbacks are triggered for all properties, including [hidden](../../../../code/formats/property_format.md#property_hidden) ones.

### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cs.md) &* **guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the property reparented.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cs.md) &* **old_parent** - Old parent property [GUID](../../../../api/library/filesystem/class.uguid_cs.md).
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cs.md) &* **new_parent** - New parent property [GUID](../../../../api/library/filesystem/class.uguid_cs.md).

## virtual void propertyReplaced ( const UGUID & guid , const UGUID & new_guid )


Callback called on replacing a property with another one.


> **Notice:** Callbacks are triggered for all properties, including [hidden](../../../../code/formats/property_format.md#property_hidden) ones.

### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cs.md) &* **guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the property being replaced.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cs.md) &* **new_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the replacing property.

## virtual void materialCompileShadersBegin ( )

Callback called on launching shader compilation process.
## virtual void materialCompileShadersEnd ( )

Callback called on completion of shader compilation process.
## virtual void materialCompileShaders ( const Material Ptr & material , int num )

Callback called on completion of shader compilation process.
### Arguments

- *const [Material](../../../../api/library/rendering/class.material_cs.md)Ptr &* **material** - Current material for which shaders are compiled.
- *int* **num** - Number of remaining remaining materials for which shaders are to be compiled.
