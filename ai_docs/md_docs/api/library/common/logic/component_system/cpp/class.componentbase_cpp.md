# ComponentBase Class (CPP)

**Header:** #include <UnigineComponentSystem.h>


This is a base class implementing basic functionality of C++ logic [components](../../../../../../principles/component_system/index.md).


> **Notice:** All your components must be inherited from this class.


To declare a component use the ***COMPONENT_DEFINE*** macro, in this case, the name of the property associated with the component will be the same as the class name.


```cpp
#include <UnigineComponentSystem.h>

using namespace Unigine;

class MyComponent : public ComponentBase
{
public:
	// declare constructor and destructor for the MyComponent class
	COMPONENT_DEFINE(MyComponent, ComponentBase);

	//...
};

```


To specify a custom property name ***COMPONENT*** and ***PROP_NAME*** macros instead:


```cpp
// constructor and destructor for the component
COMPONENT(MyComponent, Unigine::ComponentBase);

// custom name of the property associated with the component
PROP_NAME("my_component");

```


### Component Parameters


A component parameter is created using any of the following macros. Each macro has the [format](../../../../../../code/formats/property_format.md) as indicated in the brackets with the **mandatory** arguments in bold:


- [PROP_PARAM](#param_basic)(**type, name**, mask_type [for Mask parameters only], default_value, items [for switch parameters only], title, tooltip, group, args)
- [PROP_STRUCT](#param_structures)(**type, name**, title, tooltip, group, args)
- [PROP_ARRAY](#param_arrays)(**type, name**, title, tooltip, group, args)
- [PROP_ARRAY_STRUCT](#param_arrays)(**struct_type, name**, title, tooltip, group, args)


The common optional arguments are:


- *title, tooltip, group* - for displaying the corresponding information on the property parameter in the UnigineEditor.
- *args* - for passing arguments (e.g., min/max values, conditions, file filters) to a parameter's XML element in the component property. In the following example *Setting 1* and *Setting 2* are displayed only if *Auto Adjustment* is disabled: ```cpp PROP_PARAM(Toggle, auto_adjustment, false); PROP_PARAM(Float, setting_1, 2.0f / 1.0f, "Setting 1", "", "", "auto_adjustment=0"); PROP_PARAM(Float, setting_2, 1.0f, "Setting 2", "", "", "auto_adjustment=0"); ```


See more on *args* [here](../../../../../../code/formats/property_format.md#element_parameter).


When you create a component you should declare all parameters to be used. The list of [available parameter types](../../../../../../code/formats/property_format.md#parameter_type) is the same as for [properties](../../../../../../principles/properties/index.md) as they are used as basis for components.


#### Basic Parameters


Parameters of basic types (*Int, Float, Node, Material*, etc.) are declared using the **PROP_PARAM** macro, which has the following format:


```cpp
				PROP_PARAM(type, name, mask_type, default_value, items, title, tooltip, group, args)

```


The arguments except *type, name* are optional:


- *mask_type* - for Mask parameters only; available mask types are listed [here](../../../../../../code/formats/property_format.md#mask_flags).
- *default_value* - available for all parameter types, but may be omitted for *Vec*, Color, Property, Material, Node* and *Curve2d*. For example: ```cpp // for int value it should be set in the following way PROP_PARAM(Int, name, 0, "title", "tooltip") // for Vec*, Color, Property, Material, Node and Curve2d it may be like this PROP_PARAM(Color, name, vec4_black, "title", ...) // or even like this PROP_PARAM(Color, name, "title", ...) ```
- *items* - for the [*switch*](../../../../../../code/formats/property_format.md#parameter_type) parameter only.


#### Structures


Each structure, that you want to use in your component, must be inherited from the **ComponentStruct** class. This is required to ensure correct generation of the corresponding [property file](../../../../../../code/formats/property_format.md).


To declare a structured parameter use the following macro (the last three arguments are optional, see [above](#parameters)):


```cpp
PROP_STRUCT(type, name, title, tooltip, group, args);
```


> **Notice:** If a component has a structured parameter (**struct**), the definition of the structure must appear before the declaration of the parameter. The same is true, when a structure inherits from another structure: the parent must be defined before its child.


Below is an example of a component named **SomeComponent**, that has multiple parameters of various types including structures (nested and inherited):


```cpp
class SomeComponent: public Unigine::ComponentBase
{
public:
	// constructor and destructor for our component
	COMPONENT(SomeComponent, Unigine::ComponentBase);

	// name of the property associated with the component
	PROP_NAME("my_component");

	// methods to be executed at certain stages of the execution sequence
	COMPONENT_INIT(init);

	// parameters
	PROP_PARAM(Float, speed, 30.0f);
	PROP_PARAM(Node, some_node);

	// declaration of a structure (a property inside a property) named "ParentStruct"
	struct ParentStruct : public Unigine::ComponentStruct
	{
		// parameters, that will be displayed in the UnigineEditor
		PROP_PARAM(Int, var1, 1);
		PROP_PARAM(Float, var2, 2.0f);
		PROP_PARAM(Double, var3, 3.0f);

		// auxiliary variables, that won't be visible in the UnigineEditor
		float my_var1 = 2.0f;
		int my_var2 = 10;
	};

	// declaration of the structured parameter named "my_struct" of the ParentStruct type declared above
	PROP_STRUCT(ParentStruct, my_struct);

	// declaration of a child structure named "ChildStruct" inherited from the ParentStruct
	struct ChildStruct : public ParentStruct
	{
		// parameters, that will be displayed in the UnigineEditor
		PROP_PARAM(Int, child_param1, 1);
		PROP_PARAM(Double, child_param2, 2.0f);

		// declaration of a nested structure
		struct NestedStruct : public Unigine::ComponentStruct
		{
			// parameters, that will be displayed in the UnigineEditor
			PROP_PARAM(String, string_param1, "This is my string!");
		};

		// declaration of the structured parameter named "my_nested_struct" of the NestedStruct type declared above
		PROP_STRUCT(NestedStruct, my_nested_struct);
	};

	// declaration of the structured parameter named "my_struct2" of the ChildStruct type declared above
	PROP_STRUCT(ChildStruct, my_struct2, "Child Struct", "Example of an inherited structure with a nested one");

	// ...
};

```


#### Arrays


Array-type parameters are declared using the following macros (the last three arguments are optional, see [above](#parameters)):


```cpp
PROP_ARRAY_STRUCT(struct_type, name, title, tooltip, group, args);	// for arrays of structures
PROP_ARRAY(type, name, title, tooltip, group, args);				// for arrays of all other types

```


E.g., to declare a simple array of integer elements and array of **ParentStruct** elements for the **SomeComponent** component described above we can use:


```cpp
// ...

// declaring a simple array of integer elements named int_array
PROP_ARRAY(Int, int_array, "Integer Array", "This is an array of integer elements");

// declaring an array of ParentStruct elements named struct_array (ParentStruct should be declared earlier)
PROP_ARRAY_STRUCT(ParentStruct, struct_array);

// ...

```


> **Notice:** You can [edit arrays](../../../../../../editor2/properties_settings/index.md#edit_arrays) in UnigineEditor using the context menu.


#### Accessing Parameters


Accessing parameters including array-type and structured ones inside the component is simple (much like what you would normally do with member variables). Below is an example of accessing the parameters of the **SomeComponent** component described above inside its *init()* method:


```cpp
// ...

SomeComponent::init()
{
	// ...

	// changing the value of the speed parameter
	speed = 120.0f;

	// changing array's size and setting values of a couple of its elements
	int_array.resize(5);
	int_array[0] = 1;
	int_array[4] = 10;

	// setting the value of the var3 parameter of the first ParentStruct element of the array named struct_array
	struct_array[0]->var3 = struct_array[0]->var3 + 20.0f;

	// changing the value of the var1 parameter of the my_struct structured parameter
	my_struct->var1 = 5;

	// printing the value of string_param1 parameter of the nested structured parameter (my_nested_struct) inside the my_struct2 of the ChildStruct type inherited from the ParentStruct
	Log::message("String parameter value: %s",my_struct2->my_nested_struct->string_param1.get());

	// ...
}

```


### Component Methods


Each component can have an arbitrary set of methods implementing its logic. These methods are executed during the corresponding stages of the [execution sequence](../../../../../../code/fundamentals/execution_sequence/index.md). You can set multiple methods for each stage, they will be executed according to their **[order](#methods_order)** value (optional) or in the order they appear in the declaration.


```cpp
COMPONENT_INIT(function_name, order, invoke_disabled);
COMPONENT_UPDATE_ASYNC_THREAD(function_name, order, invoke_disabled);
COMPONENT_UPDATE_SYNC_THREAD(function_name, order, invoke_disabled);
COMPONENT_UPDATE(function_name, order, invoke_disabled);
COMPONENT_POST_UPDATE(function_name, order, invoke_disabled);
COMPONENT_UPDATE_PHYSICS(function_name, order), invoke_disabled;
COMPONENT_SWAP(function_name, order, invoke_disabled);
COMPONENT_SHUTDOWN(function_name, order, invoke_disabled);

```


Components can also override several lifecycle callbacks. These are invoked by the Component System when the component is created and when its enabled state changes:


```cpp
void on_ready() override {}		// called once when component was created
void on_enable() override {} 	// called once when property/node was enabled
void on_disable() override {}	// ... was disabled

```


#### Methods Execution Order


If several components are attached to a node, the **order** value determines the order in which their methods will be called during the corresponding stage of the execution sequence. E.g., suppose we have two components (*Component1* and *Component2*) attached to a node and they both have *init()* functions declared as follows:


```cpp
	// Component1
	COMPONENT_INIT(init, 2);

	// ...

	// Component2
	COMPONENT_INIT(init, 3);

	// ...

```


These functions will be called in the following order:


1. Component1::init()
2. Component2::init()


The *invoke_disabled* value (optional) indicates whether the method should be executed even if the component or node is disabled. For example:


```cpp
//...
COMPONENT_INIT(init, 2, true);  // initialize data even when disabled

void init()
{
    // initialization logic
}

COMPONENT_UPDATE(update, 0);    // execute only when enabled

void update()
{
    // per-frame update logic
}

```


#### Classes Execution Order


You can use the macro-based inheritance to control the execution order of base and inherited classes.


To **override** the base class method:


```cpp
class A
{
	COMPONENT_UPDATE(update);
	void update();
};

class B: public class A
{
	COMPONENT_UPDATE(update);
	void update();
};

// In this case only B::update() will be executed. It doesn't matter that A::update() is not virtual.

```


To run the base class method before a derived one:


```cpp
class A
{
	COMPONENT_UPDATE(update, -1);
	void update();
};

class B: public class A
{
	COMPONENT_UPDATE(update);
	void update();
};

// In this case A::update() is run first, and then B::update().

```


To run a derived class method before the base one:


```cpp
class A
{
	COMPONENT_UPDATE(update);
	void update();
};

class B: public class A
{
	COMPONENT_UPDATE(update, -1);
	void update();
};

// In this case B::update() is run first, and then A::update().

```


### Usage Example


Below you'll find an example of declaration of a logic component (`MyComponent.h`) along with logic implementation (`MyComponent.cpp`).


The implementation file of the component (`*.cpp`) must contain the following macro to ensure its automatic registration by C++ Component System, when it is [initialized](../../../../../../api/library/common/logic/component_system/cpp/class.componentsystem_cpp.md#initialize_void):


```cpp
REGISTER_COMPONENT ( your_component_name );
```


> **Warning:** Do not put this macro to header (`*.h`) files, otherwise your project won't be built!


<details>
<summary>MyComponent.h | Close</summary>

**MyComponent.h**


```cpp
class MyComponent: public Unigine::ComponentBase
{
public:

	// constructor and destructor for our component
	COMPONENT(MyComponent, Unigine::ComponentBase);

	// name of the property associated with the component
	PROP_NAME("my_component");

	// methods to be executed at certain stages of the execution sequence (see the "protected" section)
	COMPONENT_INIT(init);
	COMPONENT_UPDATE(update1, 3);
	COMPONENT_UPDATE(update2, 5);

	// parameters
	PROP_PARAM(Float, speed, 30.0f);
	PROP_PARAM(Node, some_node);

	// declaration of a structure (a property inside a property) named "ParentStruct"
	struct ParentStruct : public Unigine::ComponentStruct
	{
		// parameters, that will be displayed in the UnigineEditor
		PROP_PARAM(Int, var1, 1);
		PROP_PARAM(Float, var2, 2.0f);
		PROP_PARAM(Double, var3, 3.0f);

		// auxiliary variables, that won't be visible in the UnigineEditor
		float my_var1 = 2.0f;
		int my_var2 = 10;
	};

	// declaration of the structured parameter named "my_struct" of the ParentStruct type declared above
	PROP_STRUCT(ParentStruct, my_struct);

	// declaration of a child structure named "ChildStruct" inherited from the ParentStruct
	struct ChildStruct : public ParentStruct
	{
		// parameters, that will be displayed in the UnigineEditor
		PROP_PARAM(Int, child_param1, 1);
		PROP_PARAM(Double, child_param2, 2.0f);

		// declaration of a nested structure
		struct NestedStruct : public Unigine::ComponentStruct
		{
			// parameters, that will be displayed in the UnigineEditor
			PROP_PARAM(String, string_param1, "This is my string!");
		};

		// declaration of the structured parameter named "my_nested_struct" of the NestedStruct type declared above
		PROP_STRUCT(NestedStruct, my_nested_struct);
	};

	// declaration of the structured parameter named "my_struct2" of the ChildStruct type declared above
	PROP_STRUCT(ChildStruct, my_struct2, "Child Struct", "Example of an inherited structure with a nested one");

	// declaration of a simple array of integer elements named int_array
	PROP_ARRAY(Int, int_array, "Integer Array", "This is an array of integer elements");

	// declaration of an array of ParentStruct elements named struct_array (ParentStruct should be declared earlier)
	PROP_ARRAY_STRUCT(ParentStruct, struct_array);

protected:
	// world main loop
	void init();
	void update1();
	void update2();

};

```

</details>


<details>
<summary>MyComponent.cpp | Close</summary>

**MyComponent.cpp**


```cpp
#include "MyComponent.h"

REGISTER_COMPONENT( MyComponent );		// macro for component registration by C++ Component System

using namespace Unigine;
using namespace Math;

// method to be called on component initialization
void MyComponent::init()
{
	// changing the value of the speed parameter
	speed = 120.0f;

	// changing array's size and setting values of a couple of its elements
	int_array.resize(5);
	int_array[0] = 1;
	int_array[4] = 10;

	// setting the value of the var3 parameter of the first ParentStruct element of the array named struct_array
	struct_array[0]->var3 = struct_array[0]->var3 + 20.0f;

	// changing the value of the var1 parameter of the my_struct structured parameter
	my_struct->var1 = 5;

	// printing the value of string_param1 parameter of the nested structured parameter (my_nested_struct) inside the my_struct2 of the ChildStruct type inherited from the ParentStruct
	Log::message("\nString parameter value: %s",my_struct2->my_nested_struct->string_param1.get());
}

// first method to be called on world update
void MyComponent::update1()
{
	Log::message("\nMyComponent::update1() method!");
}

// second method to be called on world update
void MyComponent::update2()
{
	Log::message("\nMyComponent::update2() method!");
}

```

</details>


### See Also


- [C++ Component System usage example](../../../../../../code/usage/using_component_system/index.md) for more details on using C++ Component System.
- *[Property File Format](../../../../../../code/formats/property_format.md)* article to learn more about the property file format (`*.prop`).
- C++ Sample


## ComponentBase Class

---

## virtual void on_ready ( )

This method is called **immediately** after the component was created and attached to a node.
You can override this method and use it instead of the constructor for initialization, as the component is in an "undefined" state at construction time.


> **Notice:** The *init()* method is called only on [initializing a world](../../../../../../code/fundamentals/execution_sequence/main_loop.md#world_init). Implementing component initialization in *on_ready()* enables you to do all necessary preparations beforehand, if your component is to be accessed by other components on world initialization.

## virtual void on_enable ( )

This method is called by the Component System, when the component becomes enabled and active (both, node and property are enabled). You can override this method to implement some specific actions to be performed each time, when the component becomes enabled and active.
## virtual void on_disable ( )

This method is called by the Component System, when the component becomes disabled (both, node and property are disabled). You can override this method to implement some specific actions to be performed each time, when the component becomes disabled and inactive.
## const char * getClassName ( )

Returns the name of the class associated with the component. The name is generated automatically in the *COMPONENT* macro.
### Return value

Component class name.
## const char * getComponentDescription ( )

Returns the component description. The description can be specified in the *COMPONENT_DESCRIPTION* macro.
### Return value

Component description.
## const char * getPropertyName ( )


Returns the name of the property associated with the component.


> **Notice:** The name is automatically generated if you use the *COMPONENT_DEFINE* macro: in this case, the property name will be same as the class name. To specify a custom name, use the *COMPONENT* and *PROP_NAME* macros instead.


### Return value

Property name.
## const char * getParentPropertyName ( )


Returns the name of the parent property from which the current property associated with the component is inherited.


> **Notice:** The name is automatically generated if you use the *COMPONENT_DEFINE* macro: in this case, the property name will be same as the class name. To specify a custom name, use the *COMPONENT* and *PROP_NAME* macros instead.

### Return value

Parent property name.
## void setEnabled ( int enable )

Enables or disables the component.
### Arguments

- *int* **enable** - Use **1** to enable the component, **0** - to disable it.

## int isEnabled ( )

Returns a value indicating whether the component is enabled.
### Return value

**1** if the component is enabled; otherwise **0**.
## int isInitialized ( )

Returns a value indicating whether the component is initialized (its *init()* method was already called).
### Return value

**1** if the component is initialized; otherwise **0**.
## int isAutoSaveProperty ( )


Returns a value indicating whether the property file associated with the component should be automatically generated each time C++ Component System is [initialized](../../../../../../api/library/common/logic/component_system/cpp/class.componentsystem_cpp.md#initialize_void) or *[createPropertyFiles()](../../../../../../api/library/common/logic/component_system/cpp/class.componentsystem_cpp.md#createPropertyFiles_void)* method is called.


> **Notice:** By default all components have their property files re-generated automatically, this behavior might not be suitable, when you modify properties manually after creation. In this case you can add the following macro to the header file containing your component's declaration:
>
>
> ```cpp
> PROP_AUTOSAVE(0);
> ```


### Return value

**1** if the property file associated with the component should be automatically generated each time C++ Component System is [initialized](../../../../../../api/library/common/logic/component_system/cpp/class.componentsystem_cpp.md#initialize_void) or *[createPropertyFiles()](../../../../../../api/library/common/logic/component_system/cpp/class.componentsystem_cpp.md#createPropertyFiles_void)* method is called; otherwise **0**.
## const Node Ptr & getNode ( )

Returns the node, to which the component is attached.
### Return value

Node, to which the component is attached.
## const Property Ptr & getProperty ( )

Returns the property associated with the component.
### Return value

Property associated with the component.
## int getPropertyNum ( )

Returns the number of the property associated with the component.
### Return value

Number of the property in the list of properties assigned to the node.
## template < C class >

## C * addComponent ( const Node Ptr & node )

Adds the component to the specified node. This method is equivalent to *[ComponentSystem::addComponent()](../../../../../../api/library/common/logic/component_system/cpp/class.componentsystem_cpp.md#addComponent_const_NodePtr_ref_C_ptr)* method.
### Arguments

- *const [Node](../../../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node, to which the component is to be added.

### Return value

Pointer to the new added component, if it was successfully added to the specified node; otherwise nullptr.
## template < C class >

## int removeComponent ( const Node Ptr & node )

Removes the component from the specified node. This method is equivalent to *[ComponentSystem::removeComponent()](../../../../../../api/library/common/logic/component_system/cpp/class.componentsystem_cpp.md#removeComponent_const_NodePtr_ref_int)* method.
### Arguments

- *const [Node](../../../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node, from which the component is to be removed.

### Return value

**1** if the component was successfully removed from the specified node; otherwise **0**.
## template < C class >

## C * getComponent ( const Node Ptr & node , bool enabled_only = false )

Returns the first component of the specified type associated with the specified node. This method is equivalent to *[ComponentSystem::getComponent()](../../../../../../api/library/common/logic/component_system/cpp/class.componentsystem_cpp.md#getComponent_const_NodePtr_ref_C_ptr)* method.
### Arguments

- *const [Node](../../../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node, for which the component of this type is to be found.
- *bool* **enabled_only** - Enabled flag: true to get enabled component only, false to get component in any case.

### Return value

Pointer to the component if it exists; otherwise, nullptr.
## template < C class >

## void getComponents ( const Node Ptr & node , Vector <C *> & components )

Returns all components of this type assigned to the specified node and puts them to the specified buffer vector. This method is equivalent to *[ComponentSystem::getComponents()](../../../../../../api/library/common/logic/component_system/cpp/class.componentsystem_cpp.md#getComponents_const_NodePtr_ref_Vectortmplargs_ref_int_void)* method.
### Arguments

- *const [Node](../../../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node, whose components are to be retrieved.
- *[Vector](../../../../../../api/library/containers/vector/class.vector_cpp.md)<C *> &* **components** - Buffer vector, to which all found components of this type will be put.

## template < C class >

## C * getComponentInChildren ( const Node Ptr & node , bool enabled_only = false )


Returns the first component of this type found among all the children of the specified node (including the node itself). This method searches for the component in the following order:


- node itself
- node reference
- node's children
- children of node's children


This method is equivalent to *[ComponentSystem::getComponentInChildren()](../../../../../../api/library/common/logic/component_system/cpp/class.componentsystem_cpp.md#getComponentInChildren_const_NodePtr_ref_C_ptr)* method.


### Arguments

- *const [Node](../../../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node, whose hierarchy is to be checked for the components of this type.
- *bool* **enabled_only** - Enabled flag: true to get enabled component only, false to get component in any case.

### Return value

Pointer to the component if it exists; otherwise, nullptr.
## template < C class >

## void getComponentsInChildren ( const Node Ptr & node , Vector <C *> & components )

Searches for all components of this type down the hierarchy of the specified node and puts them to the given buffer vector. This method is equivalent to *[ComponentSystem::getComponentsInChildren()](../../../../../../api/library/common/logic/component_system/cpp/class.componentsystem_cpp.md#getComponentsInChildren_const_NodePtr_ref_Vectortmplargs_ref_int_void)* method.
### Arguments

- *const [Node](../../../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node, whose hierarchy is to be checked for the components of this type.
- *[Vector](../../../../../../api/library/containers/vector/class.vector_cpp.md)<C *> &* **components** - Buffer vector, to which all found components of this type will be put.

## template < C class >

## C * getComponentInParent ( const Node Ptr & node , bool enabled_only = false )

Returns the first component of this type found among all predecessors and [posessors](../../../../../../api/library/nodes/class.node_cpp.md#getPossessor_Node) of the specified node. This method is equivalent to *[ComponentSystem::getComponentInParent()](../../../../../../api/library/common/logic/component_system/cpp/class.componentsystem_cpp.md#getComponentInParent_const_NodePtr_ref_C_ptr)* method.
### Arguments

- *const [Node](../../../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node, whose hierarchy is to be checked for the components of this type.
- *bool* **enabled_only** - Enabled flag: true to get enabled component only, false to get component in any case.

### Return value

Pointer to the component if it exists; otherwise, nullptr.
## template < C class >

## void getComponentsInParent ( const Node Ptr & node , Vector <C *> & components )

Searches for all components of this type up the hierarchy of the specified node and puts them to the given buffer vector. This method is equivalent to *[ComponentSystem::getComponentsInParent()](../../../../../../api/library/common/logic/component_system/cpp/class.componentsystem_cpp.md#getComponentsInParent_const_NodePtr_ref_Vectortmplargs_ref_int_void)* method.
### Arguments

- *const [Node](../../../../../../api/library/nodes/class.node_cpp.md)Ptr &* **node** - Node, whose hierarchy is to be checked for the components of this type.
- *[Vector](../../../../../../api/library/containers/vector/class.vector_cpp.md)<C *> &* **components** - Buffer vector, to which all found components of this type will be put.

## void setDestroyCallback ( Unigine:: CallbackBase * func )

Sets a callback function to be called before destroying the component. This function can be used to implement certain actions to be performed when a component is destroyed.
### Arguments

- *Unigine::[CallbackBase](../../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **func** - Callback function.

## void clearDestroyCallback ( )

Removes a destroy callback function previously set by the *[setDestroyCallback()](#setDestroyCallback_CallbackBase_ptr_void)* method. This callback function can be used to implement certain actions to be performed when a component is destroyed.
## void save_property ( const char * name )

Saves all parameters of the property associated with the component to the specified `prop`-file.
### Arguments

- *const char ** **name** - Name of the target `.prop`-file.

## void init ( )

Engine calls this function on world initialization. Put you code for resources initialization during the world start here.
## void update ( )

Engine calls this function before updating each render frame. You can specify here all logic-related functions you want to be called every frame while your application executes.
## void postUpdate ( )

Engine calls this function after updating each render frame. You can correct behavior after the state of the node has been updated.
## void updatePhysics ( )

Engine calls this function before updating each physics frame. Here you can control physics, perform continuous physics-related operations (pushing a car forward depending on current motor's RPM, simulating a wind blowing constantly, perform immediate collision response, etc.). The engine calls *updatePhysics()* with the fixed rate (60 times per second by default) regardless of the fps number. Similar to the world script's *updatePhysics()* function.
## void shutdown ( )

Engine calls this function on world shutdown. Here you can clean up resources that were created during world script execution to avoid memory leaks.
## int is_equals ( const Ptr < Xml > & xml1 , const Ptr < Xml > & xml2 )

Returns a value indicating whether the two xml nodes are actually equal (have the same set of parameters with the same values and the same hierarchy).
### Arguments

- *const [Ptr](../../../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../../../api/library/common/class.xml_cpp.md)> &* **xml1** - First xml node.
- *const [Ptr](../../../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../../../api/library/common/class.xml_cpp.md)> &* **xml2** - Second xml node.

### Return value

1 if the two specified xml nodes are equal; otherwise, 0.
