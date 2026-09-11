# Component Class (CS)


This is a base class implementing basic functionality of logic [components](../../../../../../principles/component_system/index.md).


> **Notice:** All your components must be inherited from this class.


### Component Parameters


When you create a component you should declare all parameters to be used. You can choose which of them should be displayed in the *Parameters* window of UnigineEditor, and which should not.


![](params_ui.png)

*Auto-generated UI for component parameters*


C# Component System supports the following field types:


- bool
- int, float, double
- string
- [vec2](../../../../../../api/library/math/class.vec2_cs.md), [dvec2](../../../../../../api/library/math/class.dvec2_cs.md), [ivec2](../../../../../../api/library/math/class.ivec2_cs.md)
- [vec3](../../../../../../api/library/math/class.vec3_cs.md), [dvec3](../../../../../../api/library/math/class.dvec3_cs.md), [ivec3](../../../../../../api/library/math/class.ivec3_cs.md)
- [vec4](../../../../../../api/library/math/class.vec4_cs.md), [dvec4](../../../../../../api/library/math/class.dvec4_cs.md), [ivec4](../../../../../../api/library/math/class.ivec4_cs.md)
- [quat](../../../../../../api/library/math/class.quat_cs.md)
- [mat3](../../../../../../api/library/math/class.mat3_cs.md), [mat4](../../../../../../api/library/math/class.mat4_cs.md), [dmat4](../../../../../../api/library/math/class.dmat4_cs.md)
- Property
- Material
- [Node](../../../../../../objects/nodes/index.md) (and nodes inherited from it: *NodeDummy, ObjectMeshStatic, LightOmni*, etc.)
- Link to asset (such as *[AssetLink](../../../../../../api/library/common/logic/component_system/cs/class.assetlink_cs.md) link_to_asset* for any type of asset and *[AssetLinkNode](../../../../../../api/library/common/logic/component_system/cs/class.assetlinknode_cs.md) link_to_node* exclusively for node assets)
- Enumerations (inherited from *System.Enum*)
- All classes inherited from *Unigine.Component*
- One-dimensional arrays (such as *int[] my_array*)
- Lists (such as *List<int> my_list*)
- Any nested structures and classes including [external ones](#external_structs) (declared ouside the component)


Any *public* field of the supported type is displayed in the UI of UnigineEditor automatically. You can adjust UI representation of each field of your component by specifying additional attributes and indicating parameter type in brackets right above the class field declaration as follows:


```csharp
[ParameterType(Attribute_1 = Value_1, ..., Attribute_n = Value_n)]
```


Example:


```csharp
[ParameterSlider(Title="Float Slider", Tootip="This is my float parameter", Min=0.0f, Max=10.0f)]
public float p_float;

```


![](attributes.png)


The type of field in UI can be configured using the following attributes:


- **Parameter** � a common attribute for all supported types of fields. It has the following parameters: > **Notice:** These three attributes are available for all parameter types.

  - ***Title*** � a parameter title to be displayed in UnigineEditor
  - ***Tooltip*** � a tooltip to be displayed when the user hovers the mouse pointer over the parameter in UnigineEditor
  - ***Group*** � a group to which the parameter belongs when displayed in UnigineEditor
- ***ParameterColor*** � a *vec4* parameter to be displayed using a Color widget in UnigineEditor
- ***ParameterFile*** � a *string* parameter to be displayed using the File Asset widget in UnigineEditor. It has the following *attribute*:

  - ***Filter*** � a list of acceptable asset extensions, separated by vertical bar (e.g. "*.node|.txt|.mat*")
- ***ParameterAsset*** � an *[AssetLink](../../../../../../api/library/common/logic/component_system/cs/class.assetlink_cs.md)* parameter to be displayed using the File Asset widget in UnigineEditor. It has the following *attribute*:

  - ***Filter*** � a list of acceptable asset extensions, separated by vertical bar (e.g. "*.node|.txt|.mat*")
- ***ParameterMask*** � an *integer* parameter to be displayed using the Mask widget in UnigineEditor. It has the following *attribute*:

  - ***MaskType*** � one of values included in the *ParameterMaskAttribute.TYPE* enumeration and corresponding to a [bit mask type](../../../../../../principles/bit_masking/index.md):

    - GENERAL = 0
    - INTERSECTION
    - COLLISION
    - EXCLUSION
    - VIEWPORT
    - SHADOWS
    - MATERIAL
    - SOUND_SOURCE
    - SOUND_REVERB
    - SOUND_OCCLUSION
    - NAVIGATION
    - OBSTACLE
    - PHYSICAL
    - FIELD
- ***ParameterSlider*** � an *integer* parameter to be displayed as a slider in UnigineEditor. It has the following *attributes*:

  - ***Min*** � the minimum slider value (int, float, or double)
  - ***Max*** � the maximum slider value (int, float, or double)
  - ***Logarithmic*** � use nonlinear scale (with base 10) for the slider (bool)
  - ***Expand*** � A value indicating if the minimum and maximum values of the slider can be exceeded (bool)
  - ***MinExpand*** � A value indicating if the minimum value of the slider can be decreased (bool)
  - ***MaxExpand*** � A value indicating if the maximum value of the slider can be increased (bool)
- ***ParameterSwitch*** � an integer parameter to be displayed as a combobox in UnigineEditor. *Attributes:*

  - ***Items*** � a comma-separated list of options to be displayed in the combobox
- ***ParameterProperty*** � a Property asset parameter to be displayed as a combobox in UnigineEditor. *Attributes:*

  - ***InternalOnly*** � sets a filter allowing to use only properties that are attached to a node ([internal](../../../../../../principles/properties/index.md#internal))
  - ***ParentGUID*** � sets a [GUID](../../../../../../principles/properties/inheritance.md#property_guid)-based filter indicating the parent property for allowed properties.
- ***ParameterMaterial*** � a Material asset parameter to be displayed as a combobox in UnigineEditor. *Attributes:*

  - ***ParentGUID*** � sets a [GUID](../../../../../../principles/properties/inheritance.md#property_guid)-based filter indicating the parent material for allowed materials.


> **Notice:** By default, parameters are displayed or hidden in UI in accordance with access modifiers: *public* � displayed, otherwise � hidden. But you can hide a *public* parameter, or show a *private* or *protected* one by specifying the corresponding visibility option (**ShowInEditor** or **HideInEditor**) in the brackets (see examples below).


#### Parameter Conditions


You can selectively display component parameters if certain conditions are met. So, it is possible to define such conditions like: "Show parameter A only when parameter selected parameter B value is this, and parameter C value is that".


**Example:**


```csharp
public bool my_toggle;
public int my_int;

[ParameterCondition(nameof(my_toggle), 0)]
[ParameterCondition(nameof(my_int), 1, 3, 5)]
[ParameterCondition("other_field_name", 2)]
public float my_float;

```


#### Parameter Declaration Examples


Parameter declaration examples are shown below:


<details>
<summary>Parameter Declaration Examples | Close</summary>

**Parameter Declaration Examples**


```csharp
// int parameter to be displayed as a slider in the Editor
[ParameterSlider(Min=0.0f, Max=20.0f, Title="MySlider", Tooltip="This is my float parameter", Group="MyGroup")]
public float p_slider = 2.0f;

// int parameter to be displayed as a combobox in the Editor
[ParameterSwitch(Items="Option 1,Option 2,Option 3",Title="MySwitch")]
public int p_switch;

// enum parameter to be displayed as a combobox in the Editor
public enum MySwitch { Item1, Item2, Item3 }
public MySwitch p_switch2;

// int parameter to be displayed as a mask in the Editor
[ParameterMask(Title="MyMask")]
public int p_mask;

// vec4 parameter to be displayed as a vector in the Editor
[Parameter(Title="MyVector", Tooltip="My Vector parameter")]
public vec4 p_vector;

// vec4 parameter to be displayed using a Color widget in the Editor
[ParameterColor(Title="MyColor", Tooltip="My Color parameter")]
public vec4 p_color;

// protected string parameter you'd like to show in the Editor
[ShowInEditor, Parameter(Tooltip="This is a protected parameter displayed in the Editor!")]
protected string MyProtectedParam = "This is a string";

// string parameter to be displayed using a File Asset widget in the Editor
[ParameterFile(Tooltip="This is a protected parameter displayed in the Editor!")]
public string MyFile = "my_file.txt";

// parameter accepting a node with a preset default value to be displayed using a File Asset widget in the Editor
public AssetLinkNode node_asset_link = new AssetLinkNode("some_node.node");

// public parameter you don't want to show in the Editor
[HideInEditor]
public string MyPublicParam = "This is a string";

// Material parameter
public Material MyMaterial;

```

</details>


Complex parameters, such as structures and arrays, can be declared as follows:


<details>
<summary>Complex Parameter Declaration Examples | Close</summary>

**Complex Parameter Declaration Examples**


```csharp
// structure declaration
public struct MyStruct{
	public int p_int;
	public float p_float;
   	public MyStruct(int p1, float p2)
   	{
   	 	p_int = p1;
   	 	p_float = p2;
	}
};

// struct parameter
[Parameter(Title="My Struct Parameter")]
public MyStruct p_struct = new MyStruct(5, 2.0f);

// integer array parameter
[Parameter(Title="Integer Array")]
public int [] int_array = new int[5]  { 99,  98, 92, 97, 95};

// Parameter with the Node links array
public List<Node> world_nodes;

// Parameter with the array of links to ".node" files
public List<AssetLinkNode> file_nodes;

// array of structures parameter
[Parameter(Title="Array Of Structs")]
public List<MyStruct> my_structures;

```

</details>


Below is an example of a component named **MyComponent** that has multiple parameters of various types including structures:


<details>
<summary>Component Example | Close</summary>

**Component Example**


```csharp
public partial class MyComponent : Component
{
	[ParameterSlider(Min=0.0f, Max=20.0f, Title="SLIDER", Tooltip="This is my float parameter", Group="MyGroup")]
	public float MyParam = 2.0f;

	// int parameter to be displayed as a combobox in the Editor
	[ParameterSwitch(Items="Option 1, Option2, Option 3",Title="MySwitch")]
	public int p_switch;

	// enum parameter to be displayed as a combobox in the Editor
	public enum MySwitch { Item1, Item2, Item3 }
	public MySwitch p_switch2;

	// int parameter to be displayed as a slider in the Editor
	[ParameterSlider(Min=1, Max=8,Title="MySlider")]
	public int p_slider;

	// int parameter to be displayed as a mask in the Editor
	[ParameterMask(Title="MyMask")]
	public int p_mask;

	// vec4 parameter to be displayed as a vector in the Editor
	[Parameter(Title="MyVector", Tooltip="My Vector parameter")]
	public vec4 p_vector;

	// vec4 parameter to be displayed using a Color widget in the Editor
	[ParameterColor(Title="MyColor", Tooltip="My Color parameter")]
	public vec4 p_color;

	// protected string parameter you'd like to show in the Editor
	[ShowInEditor, Parameter(Tooltip="This is a protected parameter displayed in the Editor!")]
	protected string MyProtectedParam = "This is a string";

	// string parameter to be displayed using a File Asset widget in the Editor
	[ParameterFile(Tooltip="This is a protected parameter displayed in the Editor!")]
	public string MyFile = "";

	// parameter you don't want to show in the Editor
	[HideInEditor]
	public  string MyPublicParam = "This is a string";

	// Material parameter
	public Material MyMaterial;

	// Node array parameter
	public List<Node> MyNodes;

	// structure declaration
	public struct MyStruct{
		public int p_int;
		public float p_float;
    	public MyStruct(int p1, float p2)
    	{
       	 	p_int = p1;
       	 	p_float = p2;
   		}
	};

	// struct parameter
	[Parameter(Title="My Struct Parameter")]
	public MyStruct p_struct = new MyStruct(5, 2.0f);

	// integer array parameter
	[Parameter(Title="Integer Array")]
	public int [] int_array = new int[5]  { 99,  98, 92, 97, 95};

	// array of structures parameter
	[ParameterColor(Title="My Struct Array Parameter")]
	public List<MyStruct> my_structures;

	// ...
};

```

</details>


##### Using External Structures


In your components you can also use **external** classes and structures (declared outside the component). Sometimes the logic of your application may require using structures to pass data between the components and methods, definitions of such structures are declared at the logics layer so they can be passed to the methods themselves.


<details>
<summary>External Structure Declaration Example | Close</summary>

**External Structure Declaration Example**


```csharp
// External structure declaration
public struct ExternStruct
{
	public int i;
}

// ...
// first component declaring the NestedStruct structure
public class SomeComponent : Component
{
	public struct NestedStruct
	{
		public float f;
	}
}

// ...

// second component using the NestedStruct and ExternStruct structures
public class TestComponent : Component
{
	public ExternStruct extern_struct;
	public SomeComponent.NestedStruct nested_struct;
}

```

</details>


### Component Methods


Each component has a set of methods implementing its logic. These methods can be divided into two groups: methods of the [main loop](../../../../../../code/fundamentals/execution_sequence/index.md) (such as *void Init(), void Update(), void UpdateSyncThread()*, etc.) and arbitrary methods.


The methods from the first group have names that define their behavior and are executed during the corresponding stages of the [World Logic](../../../../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic). There is only one attribute � *Method*. You can set multiple methods for each stage � they are executed according to their **order** value (optional) or in the order they appear in the declaration. For example:


```csharp
// Component1
[Method(Order=2)]
void Init() {
    // ...
}

// Component2
[Method(Order=3)]
void Init() {
    //...
}

```


The ***InvokeDisabled*** value (optional) indicates if the method should be executed even if the component or the node is disabled. For example:


```csharp
[Method(InvokeDisabled = true)]
void Init() {
    // initialize data even when disabled
}

void Update() {
    // execute only when enabled
}

```


In addition to the methods of the main loop, methods with arbitrary names can be created for any purpose and in any amount. They have such attributes as *MethodInit, MethodUpdate, MethodShutdown*, etc.


You can also define an order of the method execution, which is applied globally for all types of components.


Let's review the following example:


```csharp
class A : Component {
    [MethodUpdate(Order=5)] void Update() {}
    [MethodPostUpdate(Order=-10)] void PostUpdate() {}
}

class B : Component {
    [MethodUpdate(Order=-1)] void Update1() {}
    [MethodUpdate(Order=1)] void Update2() {}
    void PostUpdate() {}
}

class C : Component {
    [MethodUpdate] void Update1() {}
    [MethodUpdate(Order=2)] void Update2() {}
}

```


Suppose, we have 3 objects of class A, 2 objects of class B and 1 objects of class C. The methods for them are executed in the following order:


- Order **-1** � B::Update1 and B::Update1
- Order **0** � C::Update1
- Order **1** � B::Update2 and B::Update2
- Order **2** � C::Update2
- Order **5** � A::Update, A::Update, A::Update
- Order **-10** � A::PostUpdate, A::PostUpdate, A::PostUpdate
- Order **0** � B::PostUpdate and B::PostUpdate


Components can also override several lifecycle callbacks. These are invoked by the Component System when the component is created and when its enabled state changes:


```csharp
protected override void OnReady() {}		// called once when component was created
protected override void OnEnable() {}		// called once when component/node was enabled
protected override void OnDisable() {}	// ... was disabled

```


#### Invoking and Overriding Private Methods


Private methods in derived components are now invoked and can be overridden, giving you an exceptional flexibility in implementing your application�s logic via components.


**Example:**


```csharp
public class ClassBase : Component {
	 void Init() { Log.Message("ClassBase::Init()\n"); }
	 void Update() { Log.Message("ClassBase::Update()\n"); }
}
public class ClassDerived : ClassBase {
	 void Update() { Log.Message("ClassDerived::Update()\n"); }
}

```


Now if we create a ClassDerived component, the calling order shall be as follows:


- *ClassBase::Init()* - private method of the base class (was not invoked earlier).
- *ClassDerived::Update()* - private method of the base class was overridden by the private method in the derived class having the same name.


### See Also


- [C# Component System usage example](../../../../../../code/csharp/usage/using_cs_component_system/index.md) for more details on using the C# Component System
- Sample illustrating all possible types of component parameters


## Component Class

### Properties

## 🔒︎ bool Enabled

The Value indicating whether the component is enabled: **true** if the component is enabled; otherwise **false**.
## 🔒︎ bool Initialized

The Value indicating whether the component is initialized (its *init()* method was already called): **true** if the component is initialized; otherwise **false**.
### Members

---

## protected void OnReady ( )

This method is called **immediately** after the component was created and attached to a node.
You can override this method and use it instead of the constructor for initialization, as the component is in an "undefined" state at construction time.


> **Notice:** The *Init()* method is called only on [initializing a world](../../../../../../code/fundamentals/execution_sequence/main_loop.md#world_init). Implementing component initialization in *OnReady()* enables you to do all necessary preparations beforehand, if your component is to be accessed by other components on world initialization.

## protected void OnEnable ( )

This method is called by the Engine, when the component and node become enabled and active. You can override this method to implement some specific actions to be performed each time, when the component becomes enabled.
## protected void OnDisable ( )

This method is called by the Engine, when the component and node become disabled. You can override this method to implement some specific actions to be performed each time, when the component becomes disabled.
## protected T AddComponent < T > ( Node node ) # where T : Component

Adds the component to the specified node. This method is equivalent to *[ComponentSystem.AddComponent()](../../../../../../api/library/common/logic/component_system/cs/class.componentsystem_cs.md#addComponent_Node_T)* method.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, to which the component is to be added.

### Return value

New added component instance, if it was successfully added to the specified node; otherwise null.
## protected T GetComponent < T > ( Node node , bool enabled_only ) # where T : Class

Returns the first component of the specified type associated with the specified node. This method is equivalent to *[ComponentSystem.GetComponent()](../../../../../../api/library/common/logic/component_system/cs/class.componentsystem_cs.md#getComponent_Node_bool_T)* method.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, for which the component of this type is to be found.
- *bool* **enabled_only** - Enabled flag: true to get enabled component only, false to get component in any case.

### Return value

Component if it exists; otherwise, null.
## protected T[] GetComponents < T > ( Node node , bool enabled_only ) # where T : Class

Returns all components of this type assigned to the specified node. This method is equivalent to *[ComponentSystem.GetComponents()](../../../../../../api/library/common/logic/component_system/cs/class.componentsystem_cs.md#getComponents_Node_bool_VectorT)* method.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, whose components are to be retrieved.
- *bool* **enabled_only** - Enabled flag: true to get only enabled components, false to get all components.

### Return value

Array containing all found components of this type (if any); otherwise null.
## protected T GetComponentInChildren < T > ( Node node , bool enabled_only ) # where T : Class


Returns the first component of this type found among all the children of the specified node (including the node itself). This method searches for the component in the following order:


- node itself
- node reference
- node's children
- children of node's children


This method is equivalent to *[ComponentSystem.GetComponentInChildren()](../../../../../../api/library/common/logic/component_system/cs/class.componentsystem_cs.md#getComponentInChildren_Node_bool_T)* method.

### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, whose hierarchy is to be checked for the components of this type.
- *bool* **enabled_only** - Enabled flag: true to get enabled component only, false to get component in any case.

### Return value

Component if it exists; otherwise, null.
## protected T[] GetComponentsInChildren < T > ( Node node , bool enabled_only ) # where T : Class

Searches for all components of this type down the hierarchy of the specified node. This method is equivalent to *[ComponentSystem.GetComponentsInChildren()](../../../../../../api/library/common/logic/component_system/cs/class.componentsystem_cs.md#getComponentsInChildren_Node_bool_VectorT)* method.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, whose hierarchy is to be checked for the components of this type.
- *bool* **enabled_only** - Enabled flag: true to get only enabled components, false to get all components.

### Return value

Array containing all found components of this type (if any); otherwise null.
## protected T GetComponentInParent < T > ( Node node , bool enabled_only ) # where T : Class

Returns the first component of this type found among all predecessors and [posessors](../../../../../../api/library/nodes/class.node_cs.md#getPossessor_Node) of the specified node. This method is equivalent to *[ComponentSystem.GetComponentInParent()](../../../../../../api/library/common/logic/component_system/cs/class.componentsystem_cs.md#getComponentInParent_Node_bool_T)* method.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, whose hierarchy is to be checked for the components of this type.
- *bool* **enabled_only** - Enabled flag: true to get enabled component only, false to get component in any case.

### Return value

Component if it exists; otherwise, null.
## protected T[] GetComponentsInParent < T > ( Node node , bool enabled_only ) # where T : Class

Searches for all components of this type up the hierarchy of the specified node. This method is equivalent to *[ComponentSystem.GetComponentsInParent()](../../../../../../api/library/common/logic/component_system/cs/class.componentsystem_cs.md#getComponentsInParent_Node_bool_VectorT)* method.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **node** - Node, whose hierarchy is to be checked for the components of this type.
- *bool* **enabled_only** - Enabled flag: true to get only enabled components, false to get all components.

### Return value

Array containing all found components of this type (if any); otherwise null.
## protected T FindComponentInWorld < T > ( bool enabled_only ) # where T : Class

Returns the first component of this type found in the current world. This method is equivalent to *[ComponentSystem.FindComponentInWorld()](../../../../../../api/library/common/logic/component_system/cs/class.componentsystem_cs.md#findComponentInWorld_bool_T)* method.
### Arguments

- *bool* **enabled_only** - Enabled flag: true to get enabled component only, false to get component in any case.

### Return value

Component if it exists; otherwise, null.
## protected T[] FindComponentsInWorld < T > ( bool enabled_only ) # where T : Class

Returns the list of all components of this type found in the current world. This method is equivalent to *[ComponentSystem.FindComponentsInWorld()](../../../../../../api/library/common/logic/component_system/cs/class.componentsystem_cs.md#findComponentsInWorld_bool_VectorT)* method.
### Arguments

- *bool* **enabled_only** - Enabled flag: true to get only enabled components, false to get all components.

### Return value

Array containing all found components of this type (if any); otherwise null.
## protected int RemoveComponent < T > ( Node component ) # where T : Class

Removes the component from the specified node. This method is equivalent to *[ComponentSystem.RemoveComponent()](../../../../../../api/library/common/logic/component_system/cs/class.componentsystem_cs.md#removeComponent_Node_int)* method.
### Arguments

- *[Node](../../../../../../api/library/nodes/class.node_cs.md)* **component** - Node, from which the component is to be removed.

### Return value

**1** if the component was successfully removed from the specified node; otherwise **0**.
## protected int RemoveComponent ( Component node )

Removes the specified component. This method is equivalent to *[ComponentSystem.RemoveComponent()](../../../../../../api/library/common/logic/component_system/cs/class.componentsystem_cs.md#removeComponent_Component_int)* method.
### Arguments

- *Component* **node** - Component to be removed.

### Return value

**1** if the specified component was successfully removed; otherwise **0**.
