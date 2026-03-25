# Getting Started with VR (CPP)


> **Notice:** The article reviews the creation of C++ VR projects only. You can switch to the C# version in the upper right corner of the page.


This article is for anyone who wants to start developing Virtual Reality projects in UNIGINE and is highly recommended for all new users. We're going to look into the **VR Sample** demo to see what's inside and learn how to use it to create our own project for VR. We're also going to consider some simple examples of making modifications and extending the basic functionality of this sample.


So, let's get started!


## VR Sample


Thinking about VR developers, we created the **[VR Sample](../...md)** demo, enabling you to jump straight in and start creating projects of your own. We recommend using this demo as a basis for your VR project.


![](../../content/vr/vr_template.jpg)


The demo is based on the *VR Template* that supports a wide range of runtime environments through a unified interface. It includes default implementations for core VR interactions and automatically handles controller model loading depending on runtime and device capabilities. Additionally, the template includes the implementation of basic mechanics such as grabbing and throwing objects, pressing buttons, opening/closing drawers, and a lot more.


> **Notice:** The world in this sample project has its settings optimized for the best performance in VR and includes the `*.render` asset that can be loaded at any time by simply double-clicking on it in the [Asset Browser](../../editor2/assets_workflow/index.md#asset_browser) to reset any changes you made to default optimized values.


The sample project is created using the [Component System](../../principles/component_system/index.md), so the functionality of each object is determined by the components attached.


You can extend an object's functionality simply by adding more components. For example, the laser pointer object has the following components attached:


- *[ObjMovable](../../start/vr/classes_components.md#class_objmovable)* - enables grabbing and throwing an object
- *[ObjLaserPointer](../../start/vr/classes_components.md#class_objlaserpointer)* - enables casting a ray of light by the object


![](pointer_example.gif)


## 1. Making a Template Project


So, well, we have a cool demo with some stuff inside, but how do we use it as a template? It's simple – just open your SDK Browser, go to the *Samples* tab, and select **Demos**.


Find the **VR Sample** in the *Available* section and click **Install**. After installation, the demo will appear in the *Installed* section, and you can click **Copy as Project** to create a project based on this sample.


![](copy_as_project.png)


In the **Create New Project** window that opens, enter the name for your new VR project in the corresponding field and click **Create New Project**.


![](create_project.png)


## 2. Setting Up a Device and Configuring Project


Suppose you have successfully installed your Head-Mounted Display (HMD) of choice.


[Learn more](../../vr_development/index.md#vr_development) on setting up devices for diffent VR platforms. For guidance on configuring your device, refer to the official documentation provided by your runtime or hardware vendor. If you encounter issues, consult the corresponding support resources.


> **Notice:** *Mixed Reality* functionality is supported through both the [OpenXR](../../vr_development/index.md#vr_openxr) and [Varjo](../../vr_development/index.md#integration_varjo) backends.
> If you're using a Varjo headset, just make sure *[Varjo Base](https://varjo.com/downloads/#varjo-base)* is installed and running. In some cases, you might also need *[SteamVR](https://store.steampowered.com/about/)*, depending on how your system is configured.


This demo supports [any VR device](../../vr_development/index.md#vr_devices) that exposes input and tracking through a supported runtime backend.


By default, VR is not initialized. So, you need to perform one of the following:


- If you run the application via UNIGINE SDK Browser, set the **Stereo 3D** option to the value that corresponds to the installed HMD (*OpenXR*, *OpenVR* or *Varjo*) in the **Global Options** tab and click **Apply**. ![](options_openxr.png)
- When running the application from the command line, you must specify the desired VR runtime backend using the *[-vr_app](../../code/command_line.md#vr_app)* command line option on the application start-up. ```bash your_app_name -vr_app <backend> ``` The following backends are supported: For example: ```bash your_app_name -vr_app openxr ``` Alternatively, you can specify this command-line option in the *Customize Run Options* window when running the application via the SDK Browser: ![](customize_run.png)

  - *openxr* - for devices compatible with the OpenXR standard.
  - *openvr* - for devices running via OpenVR-compatible runtimes.
  - *varjo* - for use with Varjo headsets via the Varjo SDK.


## 3. Open Project's Source


To open your VR project in an IDE, select it on the *Projects* tab of the UNIGINE SDK Browser and click *Open Code IDE*.


![](edit_code.png)


As the IDE opens, you can see, that the project contains a lot of different classes. [This brief overview](../../start/vr/classes_components.md) will give you a hint on what are they all about.


Don't forget to set the appropriate platform and configuration settings for your project before compiling your code in *Visual Studio*.


![](ide_project_settings.png)


Now, we can try and build our application for the first time.


Build your application in *Visual Studio* (*Build -> Build Solution*) or otherwise, and launch it by selecting the project on the *Projects* tab of the UNIGINE SDK Browser and clicking **Run**.


Before running your application via the UNIGINE SDK Browser make sure, that appropriate *Customize Run Options* (*Debug* version in our case) are selected, by clicking an ellipsis under the **Run** button.


![](customize_run_debug.png)


## 4. Attaching Objects to HMD


Sometimes it might be necessary to attach some object to the HMD to follow it (e.g. a hat). All movable objects (having the `movable.prop` property assigned and the *Dynamic* flag enabled) have a switch enabling this option.


For example, if you want to make a cylinder on the table attachable to the HMD, just select the corresponding node named "cylinder" in the *World Hierarchy* click **Edit** in the *Reference* section and enable the **Can Attach to Head** option.


![](attach_hmd.png)


Then select the parent node reference, and click **Apply**.


The same thing can be done via code at run time:


<details>
<summary>Show Code Snippet (C++) | Close</summary>

```cpp
#include "Framework/Components/Objects/ObjMovable.h"
#include <UnigineWorld.h>

using namespace Unigine;

...

// retrieving a NodeReference named "cylinder" and getting its reference node
NodePtr node = checked_ptr_cast<NodeReference>(World::getNodeByName("cylinder"))->getReference();

// checking if this node is a movable object by trying to get its ObjMovable component
ObjMovable *obj = ComponentSystem::get()->getComponent<ObjMovable>(node);
if (obj != nullptr)
{
	// making the object attachable to the HMD
	obj->can_attach_to_head = 1;
}

```

</details>


## 5. Accessing Mixed Reality Features (Optional)


> **Notice:** UNIGINE supports Mixed Reality via both **OpenXR** and **Varjo** backends, including full integration with Varjo's XR capabilities on supported devices such as *Varjo XR-3* and *XR-4*. A full list of supported Mixed Reality features available through Varjo integration can be found [here](../../vr_development/index.md#integration_varjo)


To begin developing a Mixed Reality application in UNIGINE, simply set up your environment as described [above](#vr_setup). If you're using Varjo hardware, ensure that *[Varjo Base](https://varjo.com/downloads/#varjo-base)* is installed and running, and that VR initializes correctly at startup.


The *VR Template* provides the `MixedRealityMenuGui` property assigned to the **head_menu** GUI node. It demonstrates the operation of the available Mixed Reality settings: you can tweak them to see how they affect the rendered image.


![](mr_property.png)


Via this menu, you can toggle the video signal from the real-world view, adjust different settings for the camera, such as white balance correction, ISO, and others. The widgets for the menu are initialized in run-time, but the node is created via UnigineEditor.


![](mixed_reality_menu.png)


To manage mixed reality, use methods of the *[VRMixedReality](../../api/library/vr/class.vrmixedreality_cpp.md)* and *[VRMarkerObject](../../api/library/vr/class.vrmarkerobject_cpp.md)* classes of UNIGINE API.


## 6. Accessing Eye-Tracking Feature (Optional)


> **Notice:** UNIGINE provides out-of-the-box support for *eye-tracking* on devices such as Varjo headsets and other systems that expose this functionality via **OpenXR** or **Varjo SDK**.


In the *VR Sample*, there is the `eyetracking_pointer` property assigned to the node of the same name. It shows the name of the node towards which the gaze is directed. The implementation of this feature is available in the [project's source](#open_source) and can be extended or changed by modifying the `EyetrackingPointer` component.


![](eye_tracking.gif)


## 7. Attaching Objects to Controllers


If you need to attach some object loaded in run-time to a controller (e.g., a menu), you can assign the `AttachToHand` property to this object.


For example, if you have a GUI object and want to attach it to the controller, select this object in the *World Hierarchy*, click **Add New Property** in the *Parameters* window, and specify the `AttachToHand` property.


![](attach_to_hand.png)


The property settings allow specifying the controller to which the object should be attached (either left or right), as well as the object's transformation.


In the *VR Sample*, this component is attached to the **hand_menu** node and initializes widgets in run-time.


## 8. Switching Nodes by Gesture (Optional)


When the application is launched, you can control the objects with your hands if you have the Varjo HMD with *[Ultraleap](../../code/plugins/ultraleap/index_cpp.md)* plugin enabled or if your HMD supports OpenXR hand-tracking extensions.


> **Notice:** For detailed setup, refer to the [Hand Tracking](../../vr_development/vr_hand_tracking.md) article.


The *VR Template* provides the `NodeSwitchEnableByGesture` property assigned to the ***vr_layer** -> **VR** -> **Ultraleap*** dummy node and is available when using a VR device with hand-tracking support. The property settings allow specifying the number of nodes you can switch between, the nodes to switch, and the gesture type for switching.


![](ultraleap_property.png)


When you hold your left wrist with your right hand, the menu appears:


![](switch_by_gesture.gif)


## 9. Adding a New Interaction


Suppose we want to extend the functionality of the laser pointer in our project, that we can *grab*, *throw*, and *use* (turn on) for now, by adding an alternative use action (change material of the object being pointed at, when certain button is pressed).


![](alt_use.gif)


So, we're going to add a new *altUseIt()* method to the *[VRInteractable](../../start/vr/classes_components.md#class_vrinteractable)* class for this new action and map it to the state of a certain controller button.


<details>
<summary>VRInteractable.h | Close</summary>

`VRInteractable.h`


```cpp
#pragma once
#include <UnigineNode.h>
#include <UniginePhysics.h>
#include "../Framework/ComponentSystem.h"
#include "Players/VRPlayer.h"

using namespace Unigine;
using namespace Math;

class VRPlayer;

class VRInteractable : public ComponentBase
{
public:
	// ...

	// interact methods
	virtual void grabIt(VRPlayer* player, int hand_num) {}
	virtual void holdIt(VRPlayer* player, int hand_num) {}
	virtual void useIt(VRPlayer* player, int hand_num) {}
	virtual void altuseIt(VRPlayer* player, int hand_num) {} //<-- method for new alternative use action
	virtual void throwIt(VRPlayer* player, int hand_num) {}
};

```

</details>


Declare and implement an override of the *altUseIt()* method for our laser pointer in the `ObjLaserPointer.h` and `ObjLaserPointer.cpp` files respectively:


<details>
<summary>ObjLaserPointer.h | Close</summary>

`ObjLaserPointer.h`


```cpp
#pragma once
#include <UnigineWorld.h>
#include "../VRInteractable.h"

class ObjLaserPointer : public VRInteractable
{
public:
	// ...

	// interact methods
	// ...
	// alternative use method override
	void altuseIt(VRPlayer* player, int hand_num) override;

	// ...

private:
	// ...
	int change_material;	//<-- "change material" state

	// ...
};

```

</details>


<details>
<summary>ObjLaserPointer.cpp | Close</summary>

`ObjLaserPointer.cpp`


```cpp
// ...

void ObjLaserPointer::init()
{
  	// setting the "change material" state to 0
	change_material = 0;

    // ...
}

void ObjLaserPointer::update()
{
	if (laser->isEnabled())
	{
      	// ...
      		// show text

		if (hit_obj && hit_obj->getProperty() && grabbed)
		{
			//---------CODE TO BE ADDED TO PERFORM MATERIAL SWITCHING--------------------
			if (change_material)// if "alternative use" button was pressed
			{
				// change object's material to mesh_base
				hit_obj->setMaterialPath("Unigine::mesh_base", "*");
			}
			//---------------------------------------------------------------------------
			// ...
		}
		else
			obj_text->setEnabled(0);
	}
	// unsetting the "change material" state
	change_material = 0;
}

// ...

// alternative use method override
void ObjLaserPointer::altuseIt(VRPlayer* player, int hand_num)
{
	// setting the "change material" state
	change_material = 1;
}

// ...

```

</details>


Now, we're going to map this action to the state of the **YB** controller button. For this purpose we should modify the *[VRPlayer](../../start/vr/classes_components.md#class_vrplayer)* class (which is the base class for all VR players) by adding the following code to its *postUpdate()* method:


<details>
<summary>VRPlayer.cpp | Close</summary>

`VRPlayer.cpp`


```cpp
// ...

void VRPlayer::postUpdate()
{
	for (int i = 0; i < getNumHands(); i++)
	{
		int hand_state = getHandState(i);
		if (hand_state != HAND_FREE)
		{
			auto &components = getGrabComponents(i);

            // ...
            //-------------CODE TO BE ADDED--------------------------
			// alternative use of the grabbed object
			if (getControllerButtonDown(i, BUTTON::YB))
			{
				for (int j = 0; j < components.size(); j++)
					components[j]->altuseIt(this, i);
				// add callback processing if necessary
			}
            //--------------------------------------------------------
		}
	}
	update_button_states();
}

// ...

```

</details>


## 10. Adding a New Interactable Object


The next step in extending the functionality of our **VR Sample** is adding a new interactable object.


Let's add a new type of interactable object, that we can grab, hold and throw with an additional feature: object will change its form (to a certain preset) when we grab it, and restore it back, when we release it. It will also display certain text in the console, if the corresponding option is enabled.


![](transformer.gif)


So, we're going to use the following components:


- **[ObjMovable](../../start/vr/classes_components.md#class_objmovable)** - to enable basic grabbing and throwing functionality
- new **ObjTransformer** component to enable form changing and log message printing functionality


The following steps are to be performed:


1. Add a new **ObjTransformer** class inherited from the *[VRInteractable](../../start/vr/classes_components.md#class_vrinteractable)*. In *Visual Studio* we can do it by choosing *Project -> Add Class* from the main menu, clicking ***Add***, specifying class name and base class in the window that opens, and clicking ***Finish***: ![](add_class.png)
2. Implement functionality of transformation to the specified node on grabbing, and restoring previous form on releasing a node. Below you'll find header and implementation files for our new **ObjTransformer** class: <details> <summary>ObjTransformer.h | Close</summary> `ObjTransformer.h` ```cpp #pragma once #include <UnigineNode.h> #include "Components/VRInteractable.h" #include "Framework/Utils.h" class ObjTransformer : public VRInteractable { public: ObjTransformer(const NodePtr &node, int num) : VRInteractable(node, num) {} virtual ~ObjTransformer() {} // property name UNIGINE_INLINE static const char* getPropertyName() { return "transformer"; } // parameters PROPERTY_PARAMETER(Toggle, show_text, 1);			// Flag indicating if messages are to be printed to the console PROPERTY_PARAMETER(String, text, "TRANSFORMATION");	// Text to be printed to the console when grabbing or releasing the node PROPERTY_PARAMETER(Node, target_object);			// Node to be displayed instead of the transformer-node, when it is grabbed // interact methods void grabIt(VRPlayer* player, int hand_num) override;	// override grab action handler void throwIt(VRPlayer* player, int hand_num) override;	// override trow action handler void holdIt(VRPlayer* player, int hand_num) override;	// override hold action handler protected: void init() override; }; ``` </details> <details> <summary>ObjTransformer.cpp | Close</summary> `ObjTransformer.cpp` ```cpp #include "ObjTransformer.h" REGISTER_COMPONENT( ObjTransformer );		// macro for component registration by the Component System // initialization void ObjTransformer::init(){ // hiding the target object (if any) if (target_object){ target_object->setEnabled(0); } } // grab action handler void ObjTransformer::grabIt(VRPlayer* player, int hand_num) { // if a target object is assigned, showing it, hiding the original object and displaying a message in the log if (target_object){ target_object->setEnabled(1); // hide original object's surfaces without disabling components ObjectPtr obj = checked_ptr_cast<Object>(node); for (int i = 0; i < obj->getNumSurfaces(); i++) obj->setEnabled(0, i); if (show_text) Log::message("\n Transformer's message: %s", text.get()); } } // throw action handler void ObjTransformer::throwIt(VRPlayer* player, int hand_num) { // if a target object is assigned, hiding it, and showing back the original object if (target_object){ target_object->setEnabled(0); // show original object's surfaces back ObjectPtr obj = checked_ptr_cast<Object>(node); for (int i = 0; i < obj->getNumSurfaces(); i++) obj->setEnabled(1, i); } } // hold action handler void ObjTransformer::holdIt(VRPlayer* player, int hand_num) { // changing the position of the target object target_object->setWorldPosition(player->getHandNode(hand_num)->getWorldPosition()); } ``` </details>
3. Build your application and launch it as we did [earlier](#open_source), a new property file (`transformer.prop`) will be generated for our new component.
4. Open the world in the [UnigineEditor](../../editor2/index.md), create a new box primitive (*Create -> Primitive -> Box*), and place it somewhere near the table, create a sphere primitive (*Create -> Primitive -> Sphere*) to be used for transformation.
5. To add components to the box object select it and click **Add New Property** in the *Node Properties* section, then drag the `movable.prop` property to the new empty field that appears. Repeat the same for the `transformer.prop` property, and drag the sphere from the *World Hierarchy* window to the **Target Object** field. ![](assignment.gif)
6. Save your world and close the UnigineEditor.
7. Launch your application.


## 11. Restricting Teleportations


By default, it is possible to teleport to any point on the scene. To avoid user interaction errors in VR (e.g., teleporting into walls or ceilings), you can restrict teleportation to certain areas. To do so, perform the following:


1. Create a mesh defining the area you want to restrict user teleportation to.
2. Set an *[intersection mask](../../principles/bit_masking/index.md#intersection_mask)* to the desired surface(s) of this mesh either in the UnigineEditor or using the *[setIntersectionMask()](../../api/library/objects/class.object_cpp.md#setIntersectionMask_int_int_void)* method: ```cpp // defining the teleportation mask as a hexadecimal value (e.g. with only the last bit enabled) int teleport_mask = 0x80000000; // setting the teleportation mask to the MyAreaMesh object's surface with the num index MyAreaMesh->setIntersectionMask(num, teleport_mask); ```
3. Set the same intersection mask for the teleport ray using the following method: ***VRPlayerVR::setTeleportationMask(teleport_mask)***.


> **Notice:** Multiple meshes can be used to define teleportation area.


## Where to Go From Here


Congratulations! Now, you know how to create your own VR project on the basis of the **[VR Sample](#vr_template)** demo, and extend its functionality. So, you can continue developing it on your own. There are some recommendations for you, that might be useful:


- Try to analyse the source code of the sample further and figure out how it works, use it to write your own.
- Read the *[Virtual Reality Best Practices](../../content/vr/index.md)* article for more information and useful tips on preparing content for VR and making user experience better.
- Read the *[Component System](../../principles/component_system/index.md)* article for more information on working with the Component System.
- Check out the *[Component System Usage Example](../../code/usage/using_component_system/index.md)* for more details on implementing logic using the Component System.


> **Notice:** You can select the **VR** project template when [creating a new application via the SDK Browser](../../sdk/projects/index_cpp.md#application_settings) to create an empty VR application from scratch (having demo content and code stripped off).
