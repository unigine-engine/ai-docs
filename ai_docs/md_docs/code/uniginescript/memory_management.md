# Handling Ownership When Using Scripts

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This article dwells on objects management and communication between the UNIGINE scripts, external C++ classes and C++ part of UNIGINE Engine (internal C++ classes).


### See Also


- [Garbage collection for UnigineScript](../../code/uniginescript/language/features.md#memory)
- [Memory Management for external classes](../../code/cpp/usage/script/classes.md#memory_management)
- [Working with Smart Pointers](../../code/fundamentals/smartpointers.md)


## UNIGINE Ownership System


UNIGINE has its own optimized memory allocator for faster and more efficient memory management. It works within a particular preallocated memory pool, which is shared by all of the UNIGINE modules. Custom C++ modules, which extend UNIGINE functionality with external C++ classes, use an underlying system-provided allocator, which has a separate memory pool.


Allocating memory, keeping track of those allocations and freeing memory blocks when they are no longer needed is mainly the task of managing objects. UNIGINE consists of several modules (including C++ modules mentioned above) each of which can establish the ownership of an object, meaning that it would be responsible for deallocating the memory when the object is no longer needed. By that, the object is accessible by all these modules. Ownership can also be released and transferred for another module to take responsibility and delete the unnecessary object at the right time. If failing to set only one owner that deallocates the object, memory leaks are imminent.


**Internal C++ classes**. Instances of these classes are low-level built-in objects, that are actually created on the C++ side when a script or a C++ module declares them, such as: *mesh*, *body*, *image* and so on. Such **internal instances** can be owned by one of the following modules:

- **Scripts**. These are: Scripts are written in the UnigineScript language and allow creating user classes. > **Notice:** An internal instance can be handled by any of the scripts (world, system or editor one), no matter whom it belongs to. The ownership matters when ***deleting*** it.

  - *World script* that contains world logic.
  - *Editor script* that wraps editor functionality and editor GUI.
  - *System script* that does system housekeeping and controls the system menu GUI.
- **API C++ classes** are wrapper classes that hide implementation of internal C++ classes and store pointers to instances of these internal classes (internal instances, in other words).  By default, ownership of such instances is handled by the Engine. API C++ classes can be owners of the internal instances if these instances are created on the C++ side of the user application via the *create()* function. As instances of C++ API classes only store pointers to instances of internal C++ classes, they cannot be created and deleted via the standard ***new / delete*** operators. So they should be declared as *smart pointers* (*Unigine::Ptr*) that allow you to automatically manage their [lifetime](../../code/fundamentals/smartpointers.md#lifetime).


There is also **Engine World**, which is also a C++ part of UNIGINE Engine (do not confuse with the world script!). All the instances created via the *new* operator or the *create()* function are automatically added to Engine World. Engine World is responsible for loading a world with all its nodes, for managing a spatial tree and handling collisions and intersections of nodes. However, it doesn't take ownership of internal instances.


## Handling Ownership in the Main Loop


Pointers to nodes (C++/C# API) created in the [Main Loop](../../code/fundamentals/execution_sequence/main_loop.md) are automatically handled by the **Engine** preventing unexpected memory leaks and crashes. Every node created via any of the following ways is added to the current world and is deleted automatically on the world shutdown (or Engine shutdown if the corresponding [lifetime management policy](../../code/fundamentals/smartpointers.md#non_ownership_object) was selected):


```cpp
// creating a new node
NodeDummyPtr nodeDummy = NodeDummy::create();
NodeReferencePtr nodeReference = NodeReference::create("object.node");
ObjectMeshStaticPtr mesh = ObjectMeshStatic::create("data/template_assets/template_material_ball/material_ball.mesh");﻿﻿

// loading a node
NodePtr node = World::loadNode("object.node");

// cloning a node
node->clone();

```


Node removal should be performed via the following code:

```cpp
node.deleteLater();

```


## Managing Ownership


The basic principles of managing ownership of internal instances are the following:

- Whoever creates an instance of an internal C++ class will automatically become the owner of this instance. Afterwards, the module that owns the internal instance can delete it. For example:

  - If you create an instance on the script side of the application via the ***new*** operator, the script will become the owner and you will be able to delete the instance by using the ***delete*** operator.
  - If you create an instance on the C++ side via the *create()* function, you will be able to delete it via the *deleteLater()* function ([non-ownership object](../../code/fundamentals/smartpointers.md#non_ownership_object)), or it will be deleted as its reference counter reaches zero([ownership objects](../../code/fundamentals/smartpointers.md#ownership_object)).
- When transferring ownership of an instance, it must be released from the previous owner and assigned to a new one. The order of these operations is of no importance.


> **Notice:** Ownership is automatically reassigned in the following cases. That is why it is required to use *[class_remove()](#class_remove)* for created bodies, shapes or joints to release the script ownership.
> - If a new ***body*** was assigned to an ***object*** via call ***class_remove(body)*** so that only the object will manage this body.
>
>   - *[body.setObject()](../../api/library/physics/class.body_cpp.md#setObject_Object_void)*
>   - *[object.setBody()](../../api/library/objects/class.object_cpp.md#setBody_Body_int_int)*
>   - an object was specified in the constructor, for example, *new [BodyRigid(object)](../../api/library/physics/class.bodyrigid_cpp.md#BodyRigid_constPtrObject)*
> - If a new ***shape*** was assigned to a ***body*** via call ***class_remove(shape)*** so that only the body will manage this shape.
>
>   - *[body.addShape()](../../api/library/physics/class.body_cpp.md#addShape_Shape_void)*
>   - *[shape.setBody()](../../api/library/physics/class.shape_cpp.md#setBody_Body_void)*
>   - a body was specified in the constructor, for example, *new [ShapeSphere(body,radius)](../../api/library/physics/class.shapesphere_cpp.md#ShapeSphere_constPtrBody_float)*
> - If a new ***joint*** was assigned to a ***body*** via call ***class_remove(joint)*** so that only the body will manage this joint.
>
>   - *[body.addJoint()](../../api/library/physics/class.body_cpp.md#addJoint_Joint_void)*
>   - *[joint.setBody0()](../../api/library/physics/class.joint_cpp.md#setBody0_Body_void)* or*[joint.setBody1()](../../api/library/physics/class.joint_cpp.md#setBody1_Body_void)*
>   - a body was specified in the constructor, for example, *new [JointFixed(body0,body1)](../../api/library/physics/class.jointfixed_cpp.md#JointFixed_constPtrBody_constPtrBody)*


## Script Ownership


By default, any instance of an internal C++ class (a node, a mesh, an image and so on) created in a script is owned by this script:

```cpp
NodeDummy node_1 = new NodeDummy(); // the script owns node_1
NodeDummy node_2 = new NodeDummy(); // the script owns node_2

// after adding node_2 as a child to node_1
// node_1 WILL become an owner of node_2
node_1.addChild(node_2);

// node_1 will be deleted together with node_2 as the latter is its child
delete node_1;

```

 If you assign a body to an object and call *class_remove()* for this body (as described above), such body will be owned by the object. So, when deleting the object, the body will be deleted too. The same goes for bodies and shapes and for bodies and joints.
```cpp
ObjectDummy object = new ObjectDummy(); // the script owns the object
BodyRigid body = new BodyRigid(object); // both the script and the object own the body

// remove script ownership for the body
class_remove(body);

// both the object and its body will be deleted
delete object;

```


### Handling Ownership of Internal Instances


Scripts can handle ownership of an instance of an internal C++ class using the following system functions:

- *class_append()* assigns ownership of the internal instance to the current script module. All appended instances will be automatically deleted on the script shutdown; or they can be deleted using the ***delete*** operator. For example: ```cpp // clone an existing node. The cloned node will be orphaned Node clone = node.clone(); // set script ownership for the node class_append(clone); // delete the cloned node later if necessary delete clone; ``` Here, *clone()* returns a new node, which is orphaned. To prevent the memory leak, a script takes ownership and safely deletes it.
- *class_manage()* indicates that reference counting should be performed for the internal instance. When the number of references that point to the instance reaches 0, the memory previously allocated for it is automatically deleted, thus freeing the developer from carefully managing the lifetime of pointed-to instances. Before calling this function, the internal instance should be appended to the script. ```cpp // create an image that will be automatically owned by the script Image image = new Image(); // enable reference counting for the image class_manage(image); // the image will be deleted when there are no references left to it image = 0; ``` Here, the *image* is automatically owned by the script, because it was created using a *new* operator. It will be deleted, because there are no references left to it.
- *class_release()* removes all references to the instance of the internal C++ class. It removes even the smallest memory leaks. ```cpp // create a new node that will be automatically owned by the script NodeDummy node = new NodeDummy(); // delete the reference to the node node = class_release(node); ```
- *class_remove()* releases the ownership of the instance. ```cpp Body body = class_remove(new BodyRigid(object)); // bodies are automatically managed by objects they are assigned to ShapeSphere shape = class_remove(new ShapeSphere(body,radius)); // shapes are automatically managed by bodies they are assigned to JointFixed joint = class_remove(new JointFixed(body,body0)); // joints are automatically managed by bodies they are assigned to ```
- *class_cast()* converts the pointer to an internal instance of a given type into another type. > **Notice:** Conversions of the pointer are unsafe and allow specifying any type, because neither the pointer nor its type is checked. When converting into the other type a new internal instance isn't constructed, so you cannot delete it via the ***delete*** operator. ```cpp // get a node Node node = engine.world.getNode(id); // cast the node to the ObjectMeshStatic type ObjectMeshStatic mesh = class_cast("ObjectMeshStatic",node); // call a member function of the class to which the node has been cast string name = mesh.getMeshName(); ``` If you try to delete the mesh declared in the example above via the ***delete*** operator, you will get an error. However, it you delete the node, the mesh will also be deleted.


### Handling Ownership of Hierarchical Nodes


There is also a group of functions that allow you to safely handle ***hierarchical nodes*** together with all of their children. They can be found in the `data/core/unigine.h` file of UNIGINE SDK.

- *[Node node_append(Node node)](../../code/uniginescript/scripts/utility/unigine.md#node_append_node)* registers script ownership of the given node and its children. ```cpp // load a node. The node will be automatically owned by the script Node node = engine.world.loadNode("my.node"); // ... // release script ownership of the instance // add an orphan child node to the loaded node node.addChild(class_remove(new NodeDummy())); // set script ownership for both the parent and the child nodes node_append(node); ``` Here, the script takes ownership of both *my* node and its child node (*NodeDummy*). > **Notice:** The situation presented in the example is created intentionally in order to show that *node_append()* sets script ownership for the whole node hierarchy. So, for example, you don't need to call *class_remove()* before adding a child to a node in your application.
- *[Node node_remove(Node node)](../../code/uniginescript/scripts/utility/unigine.md#node_remove_node)* releases script ownership of the given node and its children and casts them to their types. ```cpp // create a static mesh that will be automatically owned by the script ObjectMeshStatic mesh = new ObjectMeshStatic("samples/common/meshes/statue.mesh"); // release script ownership node_remove(mesh); ```
- *[void node_delete(Node node)](../../code/uniginescript/scripts/utility/unigine.md#node_delete_node)* deletes the parent node together with its children. Before calling this function, the node should be [appended](../../code/uniginescript/scripts/utility/unigine.md#node_append_node) for the script to take ownership. ```cpp // load a node. The node will be automatically owned by the script Node node = engine.world.loadNode("my.node"); // ... // release script ownership of the node // add an orphan child node to the loaded node node.addChild(class_remove(new NodeDummy())); // set script ownership for the node and its child node_append(node); // perform something here // delete the node and its child node_delete(node); ``` Here, both the node and its child will be deleted. > **Notice:** The situation presented in the example is created intentionally in order to show that *node_delete()* deletes the whole node hierarchy. So, for example, you don't need to call *class_remove()* before adding a child to a node in your application.
- *[Node node_clone(Node node)](../../code/uniginescript/scripts/utility/unigine.md#node_clone_node)* clones the node. Herewith, a new instance of the internal C++ class is created. Like for all other *clone()* functions, the created instance is orphaned and its ownership is to be passed to some module. For example, this function is useful when the node is an object with a body and joints. A usual *clone()* function does not recreate connected joints. ```cpp // create a node that is automatically owned by the script ObjectMeshStatic mesh = new ObjectMeshStatic("samples/common/meshes/statue.mesh"); // set script ownership for the cloned node node_append(node_clone(mesh)); ``` Here, the first mesh object is automatically owned by the script as it is created using *new* operator, while the copied one should be appended manually. Functions for ***non-hierarchical*** nodes:
- *[Node node_cast(Node node)](../../code/uniginescript/scripts/utility/unigine.md#node_cast_node)* allows you to safely convert the given base node to its derived type. > **Notice:** When converting into the other type a new internal instance isn't constructed, so you cannot delete it via the ***delete*** operator. ```cpp // get a node that will be automatically owned by the script Node node = engine.world.getNode(id); // cast the node to ObjectMeshStatic ObjectMeshStatic mesh = node_cast(node); // call a member function of the ObjectMeshStatic class int num_targets = mesh.getNumSurfaceTargets(0); ``` After downcasting, the node can call member functions of the *ObjectMeshStatic* class. If you try to delete the mesh declared in the example above via the ***delete*** operator, you will get an error as there is no such internal instance. However, if you delete the node, the mesh will also be deleted.


### Pass Ownership Between Scripts


Ownership of an internal instance can be passed between the scripts: world, system and editor ones. For the scripts to interact, use the following functions:

- One of the *[engine.world.call()](../../api/library/engine/class.world_cpp.md#call_Variable_Variable_Variable_Variable_Variable_Variable)* to call functions of the world script.
- One of the engine.system.call() to call functions of the system script.
- One of the *[engine.editor.call()](../../api/library/engine/class.editor_cpp.md#call_Variable_Variable_Variable_Variable_Variable_Variable)* to call functions of the editor script.


For example, you can create an internal instance in the world script and then pass its ownership to the system script:

1. Create an instance in the world script and release world script ownership of this object, so that the system script can grab its ownership. Then pass the object to the system script function via the *engine.system.call()* function. ```cpp int init() { // 1. Create a new dummy object. The internal instance to which the dummy object points will be created automatically ObjectDummy dummy = new ObjectDummy(); // 2. Release world script ownership of this object class_remove(dummy); // 3. Pass the object to the system script function engine.system.call("receive_dummy_ownership",dummy); return 1; } ```
2. In the system script function, set the system script ownership for the received orphan instance. Now this instance can be deleted using the ***delete*** operator; otherwise, the instance will be automatically deleted on the system script shut down. ```cpp void receive_dummy_ownership(ObjectDummy dummy) { // 1. Set system script ownership of the dummy object constructed in the world script class_append(dummy); // 2. The system script can delete the internal instance to which the dummy object points. Or it will be deleted on the system script shut down delete dummy; } ```


## C++ Ownership


There are different variants to create and handle ownership of the internal instance:

1. Create an instance of an internal C++ class by the script and pass it to be received by the function defined on the C++ side:

  - [Receive an instance as a smart pointer](#receive_node)
  - [Receive a released instance as a smart pointer](#receive_and_grab)
  - [Receive an instance of a specific type](#receive_object)
  - [Receive an instance as a variable](#receive_variable)
2. Create a smart pointer to an instance of the C++ API class and pass it to the script:

  - [Create and pass an instance as a smart pointer](#create_pass_pointer)
  - [Create and pass an instance as a variable](#create_pass_variable)


### Receive Instance as Smart Pointer


The first option is the following: a node that is created and handled by the world script is passed to the C++ function that receives a smart pointer.


1. Create a custom function on the C++ side, which will receive a NodePtr smart pointer. Then a function needs to be registered with the UNIGINE interpreter, so that the script could call it at its run time. ```cpp //main.cpp #include <UnigineEngine.h> #include <UnigineInterpreter.h> #include <UnigineInterface.h> /* */ using namespace Unigine; /* */ // 1. Create an external function that receives a smart pointer NodePtr void my_node_set(NodePtr node) { // 1.1. Call the node member function exposed through the C++ API node->setTransform(translate(vec3(1.0f,2.0f,3.0f))); } /* */ int main(int argc,char **argv) { // 2. Register the function for export into UNIGINE Interpreter::addExternFunction("my_node_set",MakeExternFunction(&my_node_set)); // 3. Initialize the engine. It will be shut down automatically EnginePtr engine(argc,argv); // 4. Enter the engine main loop engine->main(); return 0; } ```
2. Create a node in the world script and call the registered C++ function. The ownership of the node will belong to the script, so only it could call the ***delete*** operator to destroy the node. ```cpp // world script (myworld.usc) int init() { // 1. Create a new dummy node, so it could be passed to the external C++ function Node node = new NodeDummy(); // 2. Call the registered C++ function my_node_set(node); // 3. Delete the node if no longer needed; otherwise, the node will be automatically deleted by the script shutdown delete node; return 1; } ```


### Receive a Released Instance as Smart Pointer


In this case, a node with released script ownership is passed to the C++ function that receives it as a smart pointer, so that it could be deleted in accordance with the reference counter.


1. Create a custom function on the C++ side, which will receive an ImagePtr smart pointer. Then a function needs to be registered with UNIGINE interpreter, so that the script could call at in its run time. ```cpp #include <UnigineEngine.h> #include <UnigineInterpreter.h> #include <UnigineInterface.h> /* */ using namespace Unigine; /* */ // 1. Create an external function that receives a script image as a smart pointer ImagePtr void my_image_set(ImagePtr image) { // 1.1. Grab ownership of the received pointer image->setOwner(true); // 1.2. Call the image member function exposed through the C++ API image->create2D(256,256,IMAGE_FORMAT_R8); // 1.3. Delete the image if necessary (setting the reference counter to zero) image = nullptr; } /* */ int main(int argc,char **argv) { // 2. Register the function for export into UNIGINE Interpreter::addExternFunction("my_image_set",MakeExternFunction(&my_image_set)); // 3. Initialize the engine. It will be shut down automatically EnginePtr engine(argc,argv); // 4. Enter the engine main loop engine->main(); return 0; } ```
2. Create an image in the world script, release script ownership and call the registered C++ function. The ownership of the image will no longer belong to the script, so you don't need to call *delete* operator to destroy the image. ```cpp int init() { // 1. Create a new image, so it could be passed to the C++ function Image image = new Image(); // 2. Release script ownership so that it can be grabbed by the C++ function class_remove(image); // 3. Call the registered C++ function my_image_set(image); return 1; } ```


### Receive Instance of Specific Type


This variant is similar to the first one: a node that is created and handled by the world script is passed to a C++ function that receives it as a smart pointer of a specific type. Here, "specific type" means a C++ API class that is wrapped with a smart pointer (for example, *ObjectMeshStaticPtr*, *DecalDefferedMeshPtr* and so on).


1. Create a custom function on the C++ side, which will receive an [ObjectMeshDynamicPtr](../../api/library/objects/class.objectmeshdynamic_cpp.md) smart pointer. The external function should be registered to be called by the script. ```cpp //main.cpp #include <UnigineEngine.h> #include <UnigineInterpreter.h> #include <UnigineObjectMeshDynamic.h> #include <UnigineInterface.h> #include <UnigineLog.h> /* */ using namespace Unigine; /* */ // 1.0. Create an external function that receives a smart pointer ObjectMeshDynamicPtr void my_object_update(ObjectMeshDynamicPtr object,float time) { // 1.1. Call the member function of the ObjectMeshDynamic object->updateSurfaceBegin(0); object->updateSurfaceEnd(0); Log::message("Surface indices was updated\n"); } /* */ int main(int argc,char **argv) { // 2. Register the function for export into UNIGINE Interpreter::addExternFunction("my_object_update",MakeExternFunction(&my_object_update)); // 3. Initialize the engine. It will be shut down automatically EnginePtr engine(argc,argv); // 4. Enter the engine main loop engine->main(); return 0; } ```
2. On the script side, create an object and pass it to the external function. After that, the registered external C++ function call receive it, when called by the script. Ownership remains by the script, so it can delete the object. ```cpp // world script (myworld.usc) int init() { // 1. Create a new ObjectMeshDynamic Object object = new ObjectMeshDynamic(); // 1.1. Call the member function object.setMaterialPath("materials/mesh_base","*"); // 3. Call the registered external C++ function my_object_update(object,engine.game.getTime()); // 4. The script can delete the object, as it was the one that allocated it delete object; return 1; } ```


### Receive Instance as Variable


The third variant is to create an internal instance in the script (for example, the [image](../../api/library/common/class.image_cpp.md)) and pass it to the C++ function that receives a ***variable***. The external function is called by the script thereafter.


1. Create a custom function on the C++ side, which will receive a variable. The variable is cast to the *ImagePtr* smart pointer type using the dedicated function *getImage()*. After that, the C++ function should be registered to be called by the script. > **Notice:** You should set the [script runtime](../../code/cpp/usage/script/classes.md#memory_management) when calling the *getImage()* function: pass the pointer to the current interpreter via the Unigine::Interpreter::get() function. ```cpp //main.cpp #include <UnigineEngine.h> #include <UnigineInterpreter.h> #include <UnigineImage.h> #include <UnigineInterface.h> /* */ using namespace Unigine; /* */ // 1. Create an external function that receives a variable const char* my_image_get(const Variable &v) { // 1.1. Cast the received variable to the ImagePtr type ImagePtr image = v.getImage(Interpreter::get()); // 1.2. Call the image member functions exposed through C++ API return image->getFormatName(); } /* */ int main(int argc,char **argv) { // 2. Register the function for export into UNIGINE Interpreter::addExternFunction("my_image_get",MakeExternFunction(&my_image_get)); // 3. Initialize the engine. It will be shut down automatically EnginePtr engine(argc,argv); // 4. Enter the engine main loop engine->main(); return 0; } ``` There also exists another way to cast the variable into the image pointer type using the *VariableToType()* function: ```cpp //main.cpp ... // 1. The same external function const char* my_image_get(const Variable &v) { // 1.1. Another way of casting the variable value into ImagePtr: ImagePtr image = VariableToType<ImagePtr>(Interpreter::get(),v).value; return image->getFormatName(); } ... ```
2. On the script side, the image needs to be created and simply passed to the C++ function. The image will be converted into the *ImagePtr* smart pointer automatically. ```cpp //world script (myworld.usc) int init() { // 1. Create a new image Image image = new Image(); // 1.1. Specify parameters of the image and fill it with black color image.create2D(256,256,IMAGE_FORMAT_R8); // 2. Call the registered external function and simply pass the image to it my_image_get(image); // 3. The script can delete the image explicitly, if necessary delete image; return 1; } ```


### Create and Pass Instance as Smart Pointer


Smart pointers allow the C++ function not only to receive instances of [internal C++ classes](#native_class) created by the script, but also create such instances.

> **Notice:** You cannot create and pass an instance of a C++ API class as a raw pointer, as instances of C++ API classes cannot be created or deleted via the standard ***new*** and ***delete*** operators: such instances must be declared using smart pointers only.


Here, a script calls an external function that creates a new image using *ImagePtr*.


1. In the external C++ function, declare *ImagePtr*, call API function *[create()](../../api/library/common/class.image_cpp.md#Image)* and pass the pointer to the script. However, if you just pass the pointer, it will be dangling, i.e. it will not point to the valid image object as it isn't visible outside the external function scope. To avoid it, you should pass ownership of the pointer to the script via calling *setOwner(false)*. Then a custom function is registered to be called on the script side. ```cpp //main.cpp #include <UnigineEngine.h> #include <UnigineInterpreter.h> #include <UnigineImage.h> #include <UnigineInterface.h> /* */ using namespace Unigine; /* */ // 1. Create an external function that returns an ImagePtr smart pointer ImagePtr my_image_create_0() { // 1.1. Declare an image smart pointer ImagePtr image; // 1.2. Create an image in the UNIGINE memory pool through the ImagePtr smart pointer image = Image::create(); // 1.3. Specify parameters of the image and fill it with black color image->create2D(128,128,Image::FORMAT_RG8); // 1.4. Pass ownership of the pointer to the script image->setOwner(false); return image; } /* */ int main(int argc,char **argv) { // 2. Register the function for export into UNIGINE Interpreter::addExternFunction("my_image_create_0",MakeExternFunction(&my_image_create_0)); // 3. Initialize the engine. It will be shut down automatically EnginePtr engine(argc,argv); // 4. Enter the engine main loop engine->main(); return 0; } ```
2. Call the registered C++ function. The image it returns can be simply passed to the script, as conversion from the *ImagePtr* into the *Image* will be done automatically. As ownership of the image has been passed from the external function to the script, it can be deleted by the script any time (or it will be automatically deleted on engine shut down). ```cpp //world script (myworld.usc) int init() { // 1. Call the external function in the script Image image = my_image_create_0(); // 2. Set the script ownership for the image class_append(image); // 3. The script will automatically handle the ImagePtr returned by the C++ function as a simple image log.message("%s\n",image.getFormatName()); // 4. Delete the image if necessary delete image; return 1; } ```


### Create and Pass Instance as Variable


In this variant, the external function creates a new image as a ***variable*** and then the script calls this external function.


1. In the C++ function, declare an *ImagePtr*, call the API function *[create()](../../api/library/common/class.image_cpp.md#Image)* to create a smart pointer, which will allocate an internal UNIGINE image, and set it to the variable using the dedicated function *setImage()*. > **Notice:** You should set the [script runtime](../../code/cpp/usage/script/classes.md#memory_management) when calling the *setImage()* function: pass the pointer to the current interpreter via the Unigine::Interpreter::get() function. ```cpp //main.cpp #include <UnigineEngine.h> #include <UnigineInterpreter.h> #include <UnigineImage.h> #include <UnigineInterface.h> /* */ using namespace Unigine; /* */ // 1. Create an external function that returns a variable Variable my_image_create_1() { // 1.1. Declare an image smart pointer ImagePtr image; // 1.2. Create an image in the UNIGINE memory pool image = Image::create(); // 1.3. Specify parameters of the image and fill it with black color image->create2D(128,128,Image::FORMAT_RG8); // 1.4. Define the variable Variable v; // 1.5. Set the image smart pointer to the variable v.setImage(Interpreter::get(),image); return v; } /* */ int main(int argc,char **argv) { // 2. Register the function for export into UNIGINE Interpreter::addExternFunction("my_image_create_1",MakeExternFunction(&my_image_create_1)); // 3. Initialize the engine. It will be shut down automatically EnginePtr engine(argc,argv); // 4. Enter the engine main loop engine->main(); return 0; } ``` Another way to set the *ImagePtr* smart pointer to the variable is to use the *TypeToVariable* construction: ```cpp //main.cpp ... // The same external function Variable my_image_create_1() { image = Image::create(); image->create2D(128,128,Image::FORMAT_RG8); // Another way of setting the image smart pointer to the variable: Variable v = TypeToVariable<ImagePtr>(Interpreter::get(),image).value; return v; } ... ``` > **Notice:** Only core classes (like Node, Object, etc.) instances can be converted to variables via *TypeToVariable*. In other cases, you need to cast a class instance to the core class first.
2. A script calls the registered C++ function. After that, it handles the returned variable as a simple image, because conversion is done automatically. Remember, the script cannot delete the image, as the ownership belongs to the external function. The smart pointer will be automatically released when the reference count reaches zero. ```cpp //world script (myworld.usc) int init() { // 1. Call the external function in the script Image image = my_image_create_1(); // 2. The script automatically handles the returned ImagePrt as a simple image log.message("%s\n",image.getFormatName()); return 1; } ```


## Manage Script Ownership from C++ Side


If an instance has been created in the script and then passed as a variable to the C++ function, you can handle script ownership from this function by using the following methods of the *Unigine::Variable* class:

- *class_append()*
- *class_manage()*
- *class_remove()*
- *class_release()*


These functions receive a pointer to the required context, which allows you to correctly set ownership of the required script. To get the right context, use the following functions:

- *Unigine::Engine::getWorldInterpreter()* to manage world script ownership of the pointer.
- *Unigine::Engine::getSystemInterpreter()* to manage system script ownership of the pointer.
- *Unigine::Engine::getEditorInterpreter()* to manage editor script ownership of the pointer.


Setting the context is required as we perform conversion between external class variables and script ones.

> **Notice:** When calling the functions listed above, the corresponding script should already be loaded. Otherwise, NULL will be returned.


For example:

1. Create a custom function on the C++ side, which will receive a variable. Release script ownership of the received variable. ```cpp #include <UnigineEngine.h> #include <UnigineInterpreter.h> #include <UnigineImage.h> #include <UnigineInterface.h> /* */ using namespace Unigine; /* */ // 1. Create an external function that receives a variable const char* change_owner(const Variable &v) { // 1.1 Release script ownership of the received variable Engine *engine = Engine::get(); v.removeExternClass(engine->getWorldInterpreter()); // the world script context should be set, as removeExternClass() requires a script environment // 1.2. Cast the received variable to the ImagePtr type ImagePtr image = v.getImage(Interpreter::get()); // 1.3. Call the image member functions exposed through C++ API return image->getFormatName(); } /* */ int main(int argc,char **argv) { // 2. Register the function for export into UNIGINE Interpreter::addExternFunction("change_owner",MakeExternFunction(&change_owner)); // 3. Initialize the engine. It will be shut down automatically EnginePtr engine(argc,argv); // 4. Enter the engine main loop engine->main(); return 0; } ```
2. On the script side, create an image and pass it to the external C++ function. As the script ownership is released in the external function, there is no need to delete the image here. ```cpp int init() { // 1. Create a new image Image image = new Image(); // 1.1. Specify parameters of the image and fill it with black color image.create2D(256,256,IMAGE_FORMAT_R8); // 2. Call the registered external function and simply pass the image to it log.message("%s\n",change_owner(image)); } ```
