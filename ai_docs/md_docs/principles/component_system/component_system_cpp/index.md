# C++ Component System


**Component System** enables you to implement your application�s logic via a set of building blocks � **components**, and assign these blocks to nodes, giving them additional functionality. By combining these small and simple blocks you can create a very sophisticated logic system.


A logic component integrates a [node](../../../start/index.md#node), a C++ class, containing logic implementation (actions to be performed), and a [property](../../../principles/properties/index.md), defining a set of additional parameters to be used. The list of parameters as well as their types are the same for both the component and the corresponding property.


![](components.png)

*Components assigned to a node via properties*


Components give you more flexibility in implementing your logic, enabling you to:


- Control which parts of code (implemented as component methods) are to be executed, and which of them are not.
- Control execution order of these parts of code.
- Repeatedly use parts of code, written once, for as many objects as you need, with no modifications required. If you want to change your code, you modify a single source (similar to *[NodeReference](../../../objects/nodes/reference/index.md)*, if we talk about content).
- Combine certain parts of code to be executed for certain nodes. Build a very sophisticated system from numerous small and simple blocks (like you would use a *[NodeReference](../../../objects/nodes/reference/index.md)* to build a large complex structure using many simple nodes).


### See Also


- [C++ Component System API](../../../api/library/common/logic/component_system/index.md) for more details on managing components via C++ API.
- [C++ Component System Usage Example](../../../code/usage/using_component_system/index.md) for more details on implementing logic using the Component System.
- C++ Sample: `source/samples/Api/Logics/ComponentSystem`


## Logic


Logic of components is implemented via a set of methods, that are called by the corresponding functions of the [world script](../../../code/fundamentals/execution_sequence/code_update.md):


- ***init()*** � create and initialize all necessary resources.
- ***updateAsyncThread()*** � specify all logic functions you want to be called every frame independent of the rendering thread. > **Notice:** This method does not have protection locks, so it is not recommended to modify other components inside this method, unless you are absolutely sure, that these components won't be modified or removed elsewhere.
- ***updateSyncThread()*** � specify all parallel logic functions you want to be executed before the *update()*. This method can be used to perform some heavy resource-consuming calculations such as pathfinding, generation of procedural textures, and so on. > **Notice:** This method should be used to call only the API methods related to the current node: the node itself, its materials and properties.
- ***update()*** � specify all logic functions you want to be called every frame.
- ***postUpdate()*** � correct behavior according to the updated node states in the same frame.
- ***updatePhysics()*** � simulate physics: perform continuous operations (pushing a car forward depending on current motor's RPM, simulating a wind blowing constantly, perform immediate collision response, etc.).
- ***swap()*** � operate with the results of the *updateAsyncThread()* method � all other methods (threads) have already been performed and are idle. After this function, only two actions occur:

  - All objects that are queued for deletion are deleted.
  - Profiler is rendered.
- ***shutdown()*** � perform cleanup on world shutdown.


> **Notice:** You can set [multiple methods for each stage](../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md#methods) (e.g. multiple *update()* methods or just a single *init()*).


> **Warning:** The ***updateAsyncThread()** and **updateSyncThread()*** methods allow calling only [thread-safe](../../../code/fundamentals/thread_safety/index.md) engine functions.


## Workflow


The **basic workflow** is as follows:


1. Inherit a new C++ class representing your component from the *[ComponentBase](../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md)* class. The template of this class is available in the `UnigineComponentSystem.h` header as a comment.
2. In the header file determine and declare the list of parameters to be used by this component. All of these parameters with their default values (if specified) will be stored in a dedicated property file.
3. Implement component logic inside the certain methods (**init(), update(), postUpdate()**, etc.), that will be called by the corresponding functions of the Engine's [main loop](../../../code/fundamentals/execution_sequence/code_update.md).
4. Assemble the project and run it once to have the properties for all components generated.
5. Assign the created property to a node to give it the desired functionality.


Each time a property registered in the Component System is assigned to a node, an instance of the corresponding component is created. This instance will be deleted when the corresponding property is replaced with another one or removed from the node�s list, or when the node is deleted.


The logic of a certain component is active only when the corresponding node and property are enabled. Thus, you can enable/disable logic of each particular component at run time when necessary.


You can assign several properties corresponding to different components to a single node. The sequence, in which the logic of components is executed, is determined by the *[order](../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md#methods)* value specified for the corresponding methods (if *order* values are the same or not specified, the sequence is determined in accordance with the hierarchy of nodes).


> **Notice:** Components are assigned to nodes by property name (so beware not to create user properties having the same name as the component's property).


You can also create components for existing properties.


Components can interact with other components and nodes.


## Usage


As an example, you can use components to implement logic of enemies chasing the player in your game: regardless of their size, shape, speed, all of them will check player's position, and try to find a path to move closer to it as fast as they can. The code will be basically the same, it'll just use different parameters (speed, mesh, or sounds maybe), so you can put all these parameters to a [property](../../../principles/properties/index.md) (to be able to change them at any time) and the code to the corresponding component class (e.g. place enemies in the world in the *init()* and chase the player in the *update()* method).


Then you should simply assign the property to all enemy objects and set up parameters (define meshes, sounds, etc.) The Component System will do the rest: execute your code at the corresponding stages of the Engine's [main loop](../../../code/fundamentals/execution_sequence/code_update.md) for all enemy objects using their specific parameters. Should you decide to modify your code later, you can do that in a single source � component class.


Integration with the [**Microprofile**](../../../tools/profiling/microprofile/index_cpp.md) tool, enables you to monitor overall performance of the Component System, as well as to add profiling information for your components.
