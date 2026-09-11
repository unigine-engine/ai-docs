# ComponentSystem Class (CPP)

**Header:** #include <UnigineComponentSystem.h>

**Inherits from:** Unigine::WorldLogic

> **Notice:** This class is a singleton.


This class implements functionality of [C++ Component System](../../../../../../principles/component_system/index.md) and is used to create, destroy, and manage components.


### See Also


- [C++ Component System usage example](../../../../../../code/usage/using_component_system/index.md) for more details on using C++ Component System.
- C++ Sample


## ComponentSystem Class

---

## ComponentSystem * get ( )


Returns a pointer to C++ Component System. This pointer must be obtained to access functions of C++ Component System:


```cpp
ComponentSystem *cs = ComponentSystem::get();
// access functions of C++ Component System
...

```


## void initialize ( )


Performs initialization of C++ Component System, registration of all components and creation of all necessary [property files](../../../../../../code/formats/property_format.md).


> **Notice:** - This method should me called in the *[AppSystemLogic::init()](../../../../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic_init)* method.
> - If a property file for any component does not exist, it will be created automatically.


```cpp
virtual int AppSystemLogic::init()
{
	// initialize ComponentSystem and register all components
	ComponentSystem::get()->initialize();

	/*...*/

	return 1;
}

```


## void addInitCallback ( Unigine:: CallbackBase * callback )

Adds a callback which is called during ComponentSystem initialization.
### Arguments

- *Unigine::[CallbackBase](../../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback** - Callback pointer.

## void setEnabled ( bool enabled )

Enables or disables the C++ Component System. You can use it for performance debugging: enable or disable *update()*, *postUpdate()*, *updatePhysics()*, *swap()*, *updateSync()*, *updateAsync()* for all components.
### Arguments

- *bool* **enabled** - true to enable the C++ Component System, false to disable it.

## bool isEnabled ( )

Returns a value indicating whether the C++ Component System is enabled. You can use it for performance debugging: check if *update()*, *postUpdate()*, *updatePhysics()*, *swap()*, *updateSync()*, *updateAsync()* are enabled/disabled for all components.
### Return value

true if the C++ Component System is enabled, false if it is disabled.
## bool isInitialized ( )

Returns a value indicating whether the Component System is initialized - that is, whether **[initialize()](../../../../../...md#initialize_void)** has already run and the init callbacks have been called.
### Return value

true if the Component System is initialized, false if it is not.
## int getNumComponents ( )


Returns the total number of components registered in C++ Component System.


> **Notice:** This method is very slow and should not be used often.


### Return value

Total number of registered components.
## int getNumNodesWithComponents ( )

Returns the total number of nodes with components assigned.
### Return value

Total number of nodes with components assigned.
## template < C class >

## void createPropertyFile ( )

Creates a property file for a registered component associated with the property with a given name. Parameters of each component are stored in a separate `*.prop` file. If this property file does not exist, it will be created in the `data/ComponentSystem` folder with a name obtained by the component's *[getPropertyName()](../../../../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md#getPropertyName_const_char_ptr)* method.
## void initializeComponents ( constNodePtr & node )

Forces initialization of components associated with the given node in the currrent frame (it doesn't wait for the *WorldLogic::update()* callback execution).
### Arguments

- *constNodePtr &* **node** - Node for which the components need to be initialized.

## void createPropertyFile ( const char * name )

Creates a property file for a registered component associated with the property with a given name. Parameters of each component are stored in a separate `*.prop` file. If this property file does not exist, it will be created in the `data/ComponentSystem` folder.
### Arguments

- *const char ** **name** - Name of the property associated with the component.

## void createPropertyFiles ( )

Creates property files for all registered components. Parameters of each component are stored in a separate `*.prop` file. If these property files do not exist, they will be created in the `data/ComponentSystem` folder.
## void refreshProperty ( const char * name )

Rewrites the `*.prop` file for the specified property and reloads it in the [Property Manager](../../../../../../api/library/engine/class.properties_cpp.md).
### Arguments

- *const char ** **name** - Property name.

## template < C class >

## void refreshProperty ( )

Rewrites the property file for the specified component and reloads it in the [Property Manager](../../../../../../api/library/engine/class.properties_cpp.md).
## template < C class >

## void registerComponent ( )


Registers a user component derived from the [ComponentBase](../../../../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md) class.


> **Notice:** - Components must be registered in the *[AppSystemLogic::init()](../../../../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic_init)* method.
> - If a property file for the component does not exist, it will be created automatically.
> - It is recommended to use the *[REGISTER_COMPONENT](../../../../../../code/usage/using_component_system/index.md#REGISTER_COMPONENT)* macro instead.


```cpp
virtual int AppSystemLogic::init()
{
	// registering a new user component
	ComponentSystem::get()->registerComponent<MyComponent>();

	/*...*/

	return 1;
}

```


## template < C class >

## void unregisterComponent ( )

Deletes a user component derived from the [ComponentBase](../../../../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md) class.
## template < C class >

## C * addComponent ( const Node Ptr & node )


Adds the component to the specified node.


```cpp
NodeDummyPtr node = NodeDummy::create();
node->setName("node_dummy");

ComponentSystem::get()->addComponent<MyComponent>(node->getNode());
// now the node named node_dummy appears in the Editor

```


### Arguments

- *const [Node](../../../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node, to which the component is to be added.

### Return value

Pointer to the new added component, if it was successfully added to the specified node; otherwise **nullptr**.
## template < C class >

## C * getComponent ( const Node Ptr & node , bool enabled_only = false )

Returns the first component of the specified type associated with the given node.
### Arguments

- *const [Node](../../../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node, for which the component of the specified type is to be found.
- *bool* **enabled_only** - Enabled flag: true to get enabled component only, false to get component in any case.

### Return value

Pointer to the component if any; otherwise, nullptr.
## template < C class >

## void getComponents ( const Node Ptr & node , Vector <C *> & out_components , int clear_vector )

Searches for all components of the specified type assigned to the specified node and puts them to the given buffer vector.
### Arguments

- *const [Node](../../../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node, for which the components of the specified type are to be found.
- *[Vector](../../../../../../api/library/containers/vector/class.vector_cpp.md)<C *> &* **out_components** - Buffer vector, to which all found components of the specified type will be added.
- *int* **clear_vector** - Flag indicating whether the buffer vector is to be cleared before adding the found components to it or not. Use **1** to clear the vector, **0** - to append new found components to the end of the vector. The default value is 1.

## template < C class >

## C * getComponentInChildren ( const Node Ptr & node , bool enabled_only = false )


Returns the first component of the specified type found among all the children of the specified node (including the node itself). This method searches for the component in the following order:


- node itself
- node reference
- node's children
- children of node's children


### Arguments

- *const [Node](../../../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node, whose hierarchy is to be checked for the specified type of component.
- *bool* **enabled_only** - Enabled flag: true to get enabled component only, false to get component in any case.

### Return value

Pointer to the component if any; otherwise, nullptr.
## template < C class >

## void getComponentsInChildren ( const Node Ptr & node , Vector <C *> & out_components , int clear_vector )

Searches for all components of the specified type down the hierarchy of the specified node and puts them to the given buffer vector.
### Arguments

- *const [Node](../../../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node, whose hierarchy is to be checked.
- *[Vector](../../../../../../api/library/containers/vector/class.vector_cpp.md)<C *> &* **out_components** - Buffer vector, to which all found components of the specified type will be added.
- *int* **clear_vector** - Flag indicating whether the buffer vector is to be cleared before adding the found components to it or not. Use 1 to clear the vector, 0 - to append new found components to the end of the vector. The default value is 1.

## template < C class >

## C * getComponentInParent ( const Node Ptr & node , bool enabled_only = false )

Returns the first component of the specified type found among all predecessors and [posessors](../../../../../../api/library/nodes/class.node_cpp.md#getPossessor_Node) of the specified node.
### Arguments

- *const [Node](../../../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node, whose hierarchy is to be checked.
- *bool* **enabled_only** - Enabled flag: true to get enabled component only, false to get component in any case.

### Return value

Pointer to the component if any; otherwise, nullptr.
## template < C class >

## void getComponentsInParent ( const Node Ptr & node , Vector <C *> & out_components , int clear_vector )

Searches for all components of the specified type up the hierarchy of the specified node and puts them to the given buffer vector.
### Arguments

- *const [Node](../../../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node, whose hierarchy is to be checked.
- *[Vector](../../../../../../api/library/containers/vector/class.vector_cpp.md)<C *> &* **out_components** - Buffer vector, to which all found components of the specified type will be added.
- *int* **clear_vector** - Flag indicating whether the buffer vector is to be cleared before adding the found components to it or not. Use 1 to clear the vector, 0 - to append new found components to the end of the vector. The default value is 1.

## template < C class >

## C * getComponentInWorld ( bool enabled_only = false )

Returns the first component of this type found in the current world.
### Arguments

- *bool* **enabled_only** - Enabled flag: true to get enabled component only, false to get component in any case.

### Return value

Pointer to the component if any; otherwise, nullptr.
## template < C class >

## void getComponentsInWorld ( Vector <C *> & out_components , bool enabled_only = false )

Searches for all components of the specified type in the current world and puts them to the given buffer vector.
### Arguments

- *[Vector](../../../../../../api/library/containers/vector/class.vector_cpp.md)<C *> &* **out_components** - Buffer vector, to which all found components of the specified type will be added.
- *bool* **enabled_only** - Enabled flag: true to get only enabled components, false to get all components.

## bool hasComponentByClassGUID ( int node_id , const UGUID & class_guid )

Returns a value indicating whether the node with the given ID has a component of the class with the given GUID. Unlike **[getComponent()](../../../../../...md#getComponent_const_NodePtr_ref_C_ptr)** the class is addressed by its GUID rather than by a C++ type, so the check does not require the class to be known at compile time.
### Arguments

- *int* **node_id** - ID of the node to be checked.
- *const [UGUID](../../../../../../api/library/filesystem/class.uguid_cpp.md) &* **class_guid** - GUID of the component class to be looked for.

### Return value

true if the node has a component of the specified class, false if it does not.
## template < C class >

## int removeComponent ( const Node Ptr & node )


Removes the component from the specified node.


```cpp
// removes a user component MyComponent from the node
ComponentSystem::get()->removeComponent<MyComponent>(some_node);

```


### Arguments

- *const [Node](../../../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node, from which the component is to be removed.

### Return value

**1** if the component was successfully removed from the specified node; otherwise **0**.
## void setWarningLevel ( int level )

Sets the warning level for C++ Component System. Warnings can be very useful when debugging your application, e.g. to investigate Null Reference Exception cases.
### Arguments

- *int* **level** - New warning level to be set. One of the following values:

  - WARNING_LEVEL::NONE - warning messages are disabled.
  - WARNING_LEVEL::LOW - warning messages are generated only for serious cases.
  - WARNING_LEVEL::HIGH - warning messages are generated for all cases including potential ones. At this level, for example, all Node/Property/Material parameters, that are empty at startup, will be reported.

## int getWarningLevel ( )

Returns the current warning level for C++ Component System. Warnings can be very useful when debugging your application, e.g. to investigate Null Reference Exception cases.
### Return value


Current warning level. One of the following values:


- WARNING_LEVEL::NONE - warning messages are disabled.
- WARNING_LEVEL::LOW - warning messages are generated only for serious cases.
- WARNING_LEVEL::HIGH - warning messages are generated for all cases including potential ones. At this level, for example, all Node/Property/Material parameters, that are empty at startup, will be reported.
