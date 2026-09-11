# Unigine::EditorLogic Class (CPP)

**Header:** #include <UnigineLogic.h>


The *EditorLogic* class is used to control the logic of the editor. Methods of this class are called after corresponding methods of the editor script.


EditorLogic class methods are called only if the [UnigineEditor](../../../../editor2/index.md) is loaded.


## EditorLogic Class

---

## virtual int init ( )

Engine calls this function on editor initialization. Similar to the editor script's init() function.
### Return value

true if the editor is initialized successfully; otherwise, false.
## virtual int shutdown ( )

Engine calls this function on editor shutdown. Similar to the editor script's *shutdown()* function.
### Return value

true if the editor shutdown is performed successfully; otherwise, false.
## virtual int update ( )

Engine calls this function before updating each render frame when editor is loaded. Similar to the editor script's *update()* function.
### Return value

true if there were no errors during the editor update; otherwise, false.
## virtual int postUpdate ( )

Engine calls this function after updating each render frame when editor is loaded. Similar to the editor script's *postUpdate()* function.
### Return value

true if there were no errors during the editor post update; otherwise, false.
## virtual int render ( const EngineWindowViewportPtr& window )

Engine calls this function before rendering each render frame for the specified Engine window, when editor is loaded. Similar to the editor script's *render()* function.
### Arguments

- *const EngineWindowViewportPtr&* **window** - Target Engine window viewport.

### Return value

true if there were no errors during the editor rendering; otherwise, false.
## virtual int worldInit ( )

Engine calls this function on world initialization when editor is loaded. This function is similar to the editor script's *worldInit()* function.
### Return value

true if there were no errors during the world initialization; otherwise, false.
## virtual int worldShutdown ( )

Engine calls this function on world shutdown when editor is loaded. Similar to the editor script's *worldShutdown()* function.
### Return value

true if there were no errors during the world shutdown; otherwise, false.
## virtual int worldSave ( )

Engine calls this function on world save when editor is loaded. Similar to the editor script's *worldSave()* function.
### Return value

true if there were no errors during the world saving; otherwise, false.
## virtual void clear ( )

A callback on world reloading and clearing nodes list.
## virtual void nodeReparented ( const Node Ptr & node )


Callback called on node reparenting.


```cpp
void nodeReparented(conat NodePtr &node) override {
	if(node->getName() == "my_node") {
		Log::message("The parent of the node my_node has been changed\n");
	}
}

```


### Arguments

- *const [Node](../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - A smart pointer to the node.

## virtual void nodeReordered ( const Node Ptr & node )


Callback called on node reordering.


```cpp
void nodeReordered(const NodePtr &node) override {
	if(node->getName() == "my_node") {
		Log::message("The node my_node is reordered\n");
	}
}

```


### Arguments

- *const [Node](../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - A smart pointer to the node.

## virtual void nodeRenamed ( const Node Ptr & node , const char * old_name )


Callback called on node renaming.


```cpp
void nodeRenamed(const NodePtr &node, const char *old_name) override {
	if (old_name == "my_node") {
		Log::message("The node my_node has been renamed\n");
		Log::message("The new name of the node is %s\n",node->getName());
	}
}

```


### Arguments

- *const [Node](../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - A smart pointer to the node.
- *const char ** **old_name** - Old name of the renamed node.

## virtual void nodeShowInEditorChanged ( const Node Ptr & node )


Callback called on changing displaying in world hierarchy option for a node.


```cpp
void nodeShowInEditorChanged(const NodePtr &node) override {
	if(node->getName() == "my_node") {
		Log::message("Displaying in world hierarchy has changed for the my_node node\n");
	}
}

```


### Arguments

- *const [Node](../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node smart pointer.

## virtual void materialAdded ( const UGUID & guid )

Callback called on adding a material.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Material [GUID](../../../../api/library/filesystem/class.uguid_cpp.md).

## virtual void materialRemoved ( const UGUID & guid )

Callback called on removing a material.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Material [GUID](../../../../api/library/filesystem/class.uguid_cpp.md).

## virtual void materialChanged ( const UGUID & guid )

Callback called on changing a material.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Material [GUID](../../../../api/library/filesystem/class.uguid_cpp.md).

## virtual void materialReparented ( const UGUID & guid , const UGUID & old_parent , const UGUID & new_parent )

Callback called on changing material's parent.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Material [GUID](../../../../api/library/filesystem/class.uguid_cpp.md).
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **old_parent** - Old parent material [GUID](../../../../api/library/filesystem/class.uguid_cpp.md).
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **new_parent** - New parent material [GUID](../../../../api/library/filesystem/class.uguid_cpp.md).

## virtual void propertyAdded ( const UGUID & guid )


Callback called on adding a property.


> **Notice:** Callbacks are triggered for all properties, including [hidden](../../../../code/formats/property_format.md#property_hidden) ones.

### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the property added.

## virtual void propertyRemoved ( const UGUID & guid )


Callback called on removing a property.


> **Notice:** Callbacks are triggered for all properties, including [hidden](../../../../code/formats/property_format.md#property_hidden) ones.

### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the property removed.

## virtual void propertyMoved ( const UGUID & guid )

Callback called on moving a property.
> **Notice:** Callbacks are triggered for all properties, including [hidden](../../../../code/formats/property_format.md#property_hidden) ones.

### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the property moved.

## virtual void propertyChanged ( const UGUID & guid )


Callback called on changing a property.


> **Notice:** Callbacks are triggered for all properties, including [hidden](../../../../code/formats/property_format.md#property_hidden) ones.

### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the property changed.

## virtual void propertyReparented ( const UGUID & guid , const UGUID & old_parent , const UGUID & new_parent )


Callback called on changing property's parent.


> **Notice:** Callbacks are triggered for all properties, including [hidden](../../../../code/formats/property_format.md#property_hidden) ones.

### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the property reparented.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **old_parent** - Old parent property [GUID](../../../../api/library/filesystem/class.uguid_cpp.md).
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **new_parent** - New parent property [GUID](../../../../api/library/filesystem/class.uguid_cpp.md).

## virtual void propertyReplaced ( const UGUID & guid , const UGUID & new_guid )


Callback called on replacing a property with another one.


> **Notice:** Callbacks are triggered for all properties, including [hidden](../../../../code/formats/property_format.md#property_hidden) ones.

### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the property being replaced.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **new_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the replacing property.

## virtual void materialCompileShadersBegin ( )

Callback called on launching shader compilation process.
## virtual void materialCompileShadersEnd ( )

Callback called on completion of shader compilation process.
## virtual void materialCompileShaders ( const Material Ptr & material , int num )

Callback called on completion of shader compilation process.
### Arguments

- *const [Material](../../../../api/library/rendering/class.material_cpp.md)Ptr &* **material** - Current material for which shaders are compiled.
- *int* **num** - Number of remaining remaining materials for which shaders are to be compiled.
