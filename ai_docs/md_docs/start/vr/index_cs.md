# Getting Started with VR (CS)


> **Notice:** The article reviews the creation of C# VR projects only. You can switch to the C++ version in the upper right corner of the page.


This article is for anyone who wants to start developing Virtual Reality projects in UNIGINE and is highly recommended for all new users. We're going to use the **VR Template** for C# to easily get started on our own project for VR. We will also look into a **VR sample** (included in the C# VR template), which can be used as the basis for a VR application, and consider some simple examples of extending the basic functionality of this sample.


So, let's get started!


## 1. Making a Template Project


UNIGINE has a **ready-to-use template for development of C# VR projects**. It supports *multiple runtime backends* and works out of the box with devices that are compatible with those runtimes. It also includes a sample called ***vr_sample*** the corresponding world with a set of props and components is located in the `data/vr_template/vr_sample/` folder (please **do not confuse it with** the [***VR Sample*** Demo](../...md) project which is available for *C++ API* only). The template provides automatic loading of controller models in run-time. Additionally, it includes the implementation of basic mechanics such as grabbing and throwing objects, pressing buttons, opening/closing drawers, and a lot more.


> **Notice:** The world in this sample project has its settings optimized for the best performance in VR.


Both the template and the sample project are created using the [Component System](../../principles/component_system/index.md) - components attached to objects determine their functionality.


> **Notice:** A brief overview of the template structure and a description of its main components are available through the [link](../../start/vr/classes_components.md).


You can extend object's functionality simply by assigning it more components. For example, the laser pointer object in the ***vr_sample*** has the following components attached:


- ***[VRTransformMovableObject](../../start/vr/classes_components.md#vr_base_interactable)*** - enables grabbing and throwing an object
- ***[VRLaserPointer](../../start/vr/classes_components.md#vr_base_interactable)*** - enables casting a ray of light by the object
- ***[VRSelectionTest](../../start/vr/classes_components.md#vr_base_interactable)*** - enables visual highlighting on hover and grab.


![](pointer_example.gif)


You can also implement your own components to extend functionality.


The main VR features of the embedded ***vr_sample*** include:


- A set of interactive physical objects (e.g., buttons, drawers, movable items)
- Controller-based interaction with objects
- Hand Tracking
- An interactive laser pointer
- Teleportation within the scene
- GUI system integration
- GUI interaction via VR controllers


Let's create a project based on the C# *VR Template*.


1. Open **SDK Browser**, go to the *My Projects* tab, and click *Create New*.
2. In the *Create New Project* window, specify the project name VRProject, select VR in the *Template* menu, then C#(.NET) in the *API+IDE* menu, and select Float in the *Precision* menu. Then click *Create New Project*. ![](create_project_cs.png)
3. When the project is successfully created, open it in UnigineEditor.
4. In the Asset Browser, open the `vr_sample.world` file located in the `data/vr_template/vr_sample/` folder. We will work with this world.


## 2. Setting Up a Device and Configuring Project


Suppose you have successfully installed your Head-Mounted Display (HMD) of choice.


[Learn more](../../vr_development/index.md#vr_development) on setting up devices for diffent VR platforms. For guidance on configuring your device, refer to the official documentation provided by your runtime or hardware vendor. If you encounter issues, consult the corresponding support resources.


> **Notice:** *Mixed Reality* functionality is supported through both the [OpenXR](../../vr_development/index.md#vr_openxr) and [Varjo](../../vr_development/index.md#integration_varjo) backends.
> If you're using a Varjo headset, just make sure *[Varjo Base](https://varjo.com/downloads/#varjo-base)* is installed and running. In some cases, you might also need *[SteamVR](https://store.steampowered.com/about/)*, depending on how your system is configured.


This demo supports [any VR device](../../vr_development/index.md#vr_devices) that exposes input and tracking through a supported runtime backend.


By default, VR is not initialized. So, you need to perform one of the following:


- If you run the application via UNIGINE SDK Browser, set the **Stereo 3D** option to the value that corresponds to the installed HMD (*OpenVR* or *Varjo*) in the **Global Options** tab and click **Apply**. ![](options_openxr.png) Alternatively, you can specify the *[-vr_app](../../code/command_line.md#vr)* command-line option in the *Customize Run Options* window, when running the application via the SDK Browser. ![](customize_run_cs.png)
- When running the application from the command line, you must specify the desired VR runtime backend using the *[-vr_app](../../code/command_line.md#vr_app)* command line option on the application start-up. ```bash your_app_name -vr_app <backend> ``` The following backends are supported: For example: ```bash your_app_name -vr_app openxr ```

  - *openxr* - for devices compatible with the OpenXR standard.
  - *openvr* - for devices running via OpenVR-compatible runtimes.
  - *varjo* - for use with Varjo headsets via the Varjo SDK.
- If you launch the application from UnigineEditor, specify the corresponding *VR mode*: ![](openxr_mode.png)


Run the application and learn about basic mechanics, grab and throw objects, try to teleport and interact with objects in the scene.


## 3. Extending Functionality


So, as a part of our first VR project, let's learn how to use the ***vr_sample*** functionality and how it can be extended.


### 3.1. Attaching Object to HMD


Sometimes it might be necessary to attach some object to the HMD to follow it. It can be a menu (like the ***menu_attached_to_head*** node in the sample), or glasses with colored lenses, or a smoking cigar. To attach a node to the HMD position, just assign the ***VRAttachToHead*** component to this node and specify the required settings: distance, forward direction axis, and flags indicating whether the node position is fixed and updated when the component is enabled.


![](attach_hmd_cs.png)


### 3.2. Attaching Objects to Controllers


If you need to attach some object loaded in run-time to a controller (e.g., a menu), you can assign the `VRAttachToHand` component to this object.


For example, if you have a GUI object and want to attach it to the controller, select this object in the *World Hierarchy*, click **Add New Component or Property** in the *Parameters* window, and specify the `VRAttachToHand` component.


![](attach_to_hand_cs.png)


The component settings allow specifying the controller to which the object should be attached (either left or right), as well as the object's transformation.


In the ***vr_sample***, this component is attached to the **menu_attached_to_hand** node and initializes widgets in run-time.


### 3.3. Restricting Teleportations


In VR projects, sometimes we use teleporting to move around, especially in large scenes. By default, it is possible to teleport to any point of the scene. But sometimes, it might be necessary to restrict teleportation to certain areas (for example, to the roof). VR Template provides the ***TeleportationMovement*** component (assigned to the ***vr_layer** -> **vr_movement_manager** -> **teleportation_movement*** node) that implements teleportation logic and allows specifying the maximum teleportation distance, the appearance of the ray and target point, and so on.


You can teleport to an object if its *Physics Intersection mask* matches the *Teleportation mask* in the component settings. By default, the 2nd bit of the *Teleportation mask* is used. So, you can teleport to objects, for which the *Physics Intersection* option is enabled and the 2nd bit of the *Physics Intersection mask* is set.


![](teleportation_mask.png)


To restrict teleportation to a certain area, do the following:


1. Create a new *Static Mesh* object by using the default plane (`core/meshes/plane.mesh`) or an arbitrary mesh that will define the restricted area.
2. Place the *Static Mesh* in the scene just above the floor.
3. In the Parameters window, enable the *Physics Intersection* option for the object and check that the 2nd bit of the *Physics Intersection Mask* is disabled. ![](physics_intersection_on.png)
4. Save and run the application. Now you cannot teleport to the area defined by the rectangular plane (the ray and the target point are red). ![](teleport_restricted.png)
5. To hide the *Static Mesh*, disable all bits of its *Viewport* and *Shadow* masks. ![](masks_off.png)
6. Save changes and run the application: the rectangular plane is invisible now. ![](plane_hidden.png)


### 3.4. Changing Controller Grip Button to Trigger


You might want to remap actions or swap the controls in your VR application. As an example, let's do this for the controller. We will remap the *Grab* action from the *Grip* button to *Trigger*, and the *Use* action to the *Grip* button.


> **Notice:** You can discover [how inputs on different types of controllers are mapped](../../vr_development/vr_input.md#openvr_input) to the buttons and axes within the UNIGINE input system.


User input for the controller is defined in the ***VRControllerInput*** component. It is assigned to the ***left_preset_0*** and ***right_preset_0*** nodes (***vr_player** -> **vr_input***) in our VR sample.


To remap actions, do the following:


1. Select the ***left_preset_0*** node that contains settings for the left controller (the *Bind -> Side* parameter value is set to LEFT).
2. Change the *Grab Button -> Button* value to LEFT_AXIS1, and the *Use Button -> Button* value to LEFT_GRIP: ![](change_grab_button.png)
3. Select the ***right_preset_0*** node that contains settings for the right controller.
4. Change the *Grab Button -> Button* value to RIGHT_AXIS1, and the *Use Button -> Button* value to RIGHT_GRIP.
5. Save changes (*Ctrl+S*) and press the **Play** button to run the application.


Now you can grab objects by the trigger, and use them by the *Grip* side button.


### 3.5. Adding an Interactive Area


In games and VR applications, some actions are performed when you enter a special area in the scene (for example, music starts, sound or visual effects appear). Let's implement this in our project: when you enter or teleport to a certain area, it rains inside it.


In UNIGINE, the *[World Trigger](../../objects/worlds/world_trigger/index.md)* node is used to track when any node (collider or not) gets inside or outside of it (for objects with physical bodies, the *[Physical Trigger](../../objects/effects/physicals/physical_trigger/index.md)* node is used).


1. First of all, create a trigger to define the rain area. On the Menu bar, choose *Create -> Logic -> World Trigger* and place the trigger near the ***Material Ball***, for example. Set the trigger size to (2, 2, 2). ![](add_trigger.png)
2. Create a new ***TriggerZone*** component that will turn the rain node on and off (in our case, it is a particle system simulating rain), depending on the trigger state. Add the following code to the component and then assign it to the *World Trigger* node: <details> <summary>TriggerZone.cs | Close</summary> `TriggerZone.cs` ```csharp using System; using System.Collections; using System.Collections.Generic; using Unigine; public partial class TriggerZone : Component { private WorldTrigger trigger = null; public Node ControlledNode = null; private void Init() { // check if the component is assigned to WorldTrigger if (node.Type != Node.TYPE.WORLD_TRIGGER) { Log.Error($"{nameof(TriggerZone)} error: this component can only be assigned to a WorldTrigger.\n"); Enabled = false; return; } // check if ControlledNode is specified if (ControlledNode == null) { Log.Error($"{nameof(TriggerZone)} error: 'ControlledNode' is not set.\n"); Enabled = false; return; } // add event handlers to be fired when a node gets inside and outside the trigger trigger = node as WorldTrigger; trigger.EventEnter.Connect(trigger_enter); trigger.EventLeave.Connect(trigger_leave); } private void Update() { // write here code to be called before updating each render frame } // handler function that enables ControlledNode when vr_player enters the trigger private void trigger_enter(Node node) { ControlledNode.Enabled = true; } // handler function that disables ControlledNode when vr_player leaves the trigger private void trigger_leave(Node node) { if (node.Name != "vr_player") return; ControlledNode.Enabled = false; } } ``` </details>
3. Now let's add the rain effect. Drag the `rain_effect.node` asset (available in the `vr/particles` folder of the *UNIGINE Starter Course Project* add-on) to the scene, add it as the child to the trigger node and turn it off (the component will turn it on later). ![](rain_effect_node.png)
4. Drag the ***rain_effect*** node from the *World Hierarchy* window to the *Controlled Node* field of the ***TriggerZone*** (in the *Parameters* window). ![](triggerzone_component.png)
5. Select the ***vr_player** (PlayerDummy)* node in the *World Hierarchy* and check the ***Triggers Interaction*** option for it to make the trigger react on contacting it. ![](../../learn/13_vr_app/triggers_interaction.png)
6. Save changes (*Ctrl+S*), click **Play** to run the application, and try to enter the area defined by the trigger - it is raining inside. ![](local_rain.png)


### 3.6. Adding a New Interaction


Another way to extend functionality is to add a new action for the object.


We have a laser pointer that we can *grab*, *throw*, and *use* (turn on a laser beam). Now, let's add an alternative use action - change the pointed object's material. This action will be executed when we press and hold the Grip side button on one controller while using the laser pointer gripped by the opposite controller.


The ***VRLaserPointer.cs*** component implements the base functionality of the laser pointer.


The base component for all interactive objects is ***[VRBaseInteractable](../../start/vr/classes_components.md#vr_base_interactable)*** (`vr_template/components/base/VRInteractable.cs`). It defines all available states of the interactive objects (*NOT_INTERACT, HOVERED, GRABBED, USED*) and methods executed on certain actions performed on the objects (*OnHoverBegin, OnHoverEnd, OnGrabBegin, OnGrabEnd, OnUseBegin, OnUseEnd*).


Components inherited from ***VRBaseInteractable*** must implement overrides of these methods (for example, the grab logic for the object must be implemented in the *OnGrabBegin* method of the inherited component).


So, we need to add a new action and map it to a new state (the *Grip* side button is pressed on one controller while the laser pointer gripped (*Grip*) by the opposite controller is used):


1. Add a new ***OnAltUse*** action (alternative use) and a new ***ALT_USED*** state to the ***VRBaseInteractable*** base component: <details> <summary>VRBaseInteractable.cs | Close</summary> `VRBaseInteractable.cs` ```csharp using System; using System.Collections; using System.Collections.Generic; using Unigine; public partial class VRBaseInteractable : Component { static public event Action onInit; public enum INTERACTABLE_STATE { NOT_INTERACT, HOVERED, GRABBED, USED, ALT_USED   // add a new state } public INTERACTABLE_STATE CurrentState { get; set; } protected void Init() { onInit?.Invoke(this); } public virtual void OnHoverBegin(VRBaseInteraction interaction, VRBaseController controller) { } public virtual void OnHoverEnd(VRBaseInteraction interaction, VRBaseController controller) { } public virtual void OnGrabBegin(VRBaseInteraction interaction, VRBaseController controller) { } public virtual void OnGrabEnd(VRBaseInteraction interaction, VRBaseController controller) { } public virtual void OnUseBegin(VRBaseInteraction interaction, VRBaseController controller) { } public virtual void OnUseEnd(VRBaseInteraction interaction, VRBaseController controller) { } // add methods for a new "alternative use" action public virtual void OnAltUse(VRBaseInteraction interaction, VRBaseController controller) { } public virtual void OnAltUseEnd(VRBaseInteraction interaction, VRBaseController controller) { } } ``` </details>
2. Add overrides of the *OnAltUse()* and *OnAltUseEnd()* methods to the ***VRLaserPointer*** component (as we are going to add a new action for the laser pointer). In the *Update()* method, implement the logic of the *AltUse* action that is executed when the corresponding flags are set. <details> <summary>VRLaserPointer.cs | Close</summary> `VRLaserPointer.cs` ```csharp #region Math Variables #if UNIGINE_DOUBLE using Scalar = System.Double; using Vec2 = Unigine.dvec2; using Vec3 = Unigine.dvec3; using Vec4 = Unigine.dvec4; using Mat4 = Unigine.dmat4; #else using Scalar = System.Single; using Vec2 = Unigine.vec2; using Vec3 = Unigine.vec3; using Vec4 = Unigine.vec4; using Mat4 = Unigine.mat4; using WorldBoundBox = Unigine.BoundBox; using WorldBoundSphere = Unigine.BoundSphere; using WorldBoundFrustum = Unigine.BoundFrustum; #endif #endregion using System; using System.Collections; using System.Collections.Generic; using Unigine; public partial class VRLaserPointer : VRBaseInteractable { [ShowInEditor] [Parameter(Title = "Laser", Group = "VR Laser Pointer")] private Node laser = null; [ShowInEditor] [Parameter(Title = "Laser Ray", Group = "VR Laser Pointer")] private Node laserRay = null; [ShowInEditor] [Parameter(Title = "Laser Hit", Group = "VR Laser Pointer")] private Node laserHit = null; [ShowInEditor] [Parameter(Title = "Object Text", Group = "VR Laser Pointer")] private ObjectText objText = null; private Mat4 laserRayMat; private WorldIntersection intersection = new WorldIntersection(); private float rayOffset = 0.05f; private bool grabbed = false; private bool altuse = false; public  List<Material> materials = null; private int current_material = 0; protected override void OnReady() { laserRayMat = new Mat4(laserRay.Transform); laser.Enabled = false; // if the list of textures is empty/not defined, report an error if(materials == null || materials.Count < 0) { Log.Error($"{nameof(VRLaserPointer)} error: materials list is empty.\n"); Enabled = false; return; } } private void Update() { if(laser.Enabled && grabbed) { laserRay.Transform = laserRayMat; vec3 dir = laserRay.GetWorldDirection(MathLib.AXIS.Y); Vec3 p0 = laserRay.WorldPosition + dir * rayOffset; Vec3 p1 = p0 + dir * 1000; Unigine.Object hitObj = World.GetIntersection(p0, p1, 1, intersection); if(hitObj != null) { laserRay.Scale = new vec3(laserRay.Scale.x, MathLib.Length(intersection.Point - p0) + rayOffset, laserRay.Scale.z); laserHit.WorldPosition = intersection.Point; laserHit.Enabled = true; } else { laserHit.Enabled = false; } if (hitObj != null) { objText.Enabled = true; objText.Text = hitObj.Name; float radius = objText.BoundSphere.Radius; vec3 shift = vec3.UP * radius; objText.WorldTransform = MathLib.SetTo(laserHit.WorldPosition + shift, VRPlayer.LastPlayer.HeadController.WorldPosition, vec3.UP, MathLib.AXIS.Z); // implement logic of the "alternative use" action (cyclic change of materials on the object according to the list) if(altuse) { current_material++; if (current_material >= materials.Capacity) current_material = 0; hitObj.SetMaterial(materials[current_material], 0); Log.Message("ALTUSE HIT\n"); altuse = false; } } else objText.Enabled = false; } } public override void OnGrabBegin(VRBaseInteraction interaction, VRBaseController controller) { grabbed = true; } public override void OnGrabEnd(VRBaseInteraction interaction, VRBaseController controller) { grabbed = false; laser.Enabled = false; objText.Enabled = false; } public override void OnUseBegin(VRBaseInteraction interaction, VRBaseController controller) { if(grabbed) laser.Enabled = true; } public override void OnUseEnd(VRBaseInteraction interaction, VRBaseController controller) { laser.Enabled = false; objText.Enabled = false; } // override the method that is called when the "alternative use" action is performed on the object public override void OnAltUse(VRBaseInteraction interaction, VRBaseController controller) { altuse = true; CurrentState = VRBaseInteractable.INTERACTABLE_STATE.ALT_USED; } // override the method that is called when the "alternative use" action is done public override void OnAltUseEnd(VRBaseInteraction interaction, VRBaseController controller) { altuse = false; CurrentState = VRBaseInteractable.INTERACTABLE_STATE.NOT_INTERACT; } } ``` </details>
3. Add an execution condition for the *OnAltUse* action. All available types of interactions are implemented in the ***VRHandShapeInteraction*** component (`vr_template/components/interactions/interactions/VRHandShapeInteraction.cs`). So, add the following code to the *Interact()* method of this component: <details> <summary>VRHandShapeInteraction.cs | Close</summary> `VRHandShapeInteraction.cs` ```csharp public override void Interact(VRInteractionManager.InteractablesState interactablesState, float ifps) { // ... // update current input bool grabDown = false; bool grabUp = false; bool useDown = false; bool useUp = false; // reset flags before checking the current input bool altUse = false; bool altUseUp = false; switch (controller.Device) { case VRInput.VRDevice.LEFT_CONTROLLER: grabDown = VRInput.IsLeftButtonDown(VRInput.ControllerButtons.GRAB_BUTTON); grabUp = VRInput.IsLeftButtonUp(VRInput.ControllerButtons.GRAB_BUTTON); useDown = VRInput.IsLeftButtonDown(VRInput.ControllerButtons.USE_BUTTON); useUp = VRInput.IsLeftButtonUp(VRInput.ControllerButtons.USE_BUTTON); // for the left controller, the Use button must be hold on the right controller altUse = VRInput.IsRightButtonPress(VRInput.ControllerButtons.USE_BUTTON); altUseUp = VRInput.IsRightButtonUp(VRInput.ControllerButtons.USE_BUTTON); break; case VRInput.VRDevice.RIGHT_CONTROLLER: grabDown = VRInput.IsRightButtonDown(VRInput.ControllerButtons.GRAB_BUTTON); grabUp = VRInput.IsRightButtonUp(VRInput.ControllerButtons.GRAB_BUTTON); useDown = VRInput.IsRightButtonDown(VRInput.ControllerButtons.USE_BUTTON); useUp = VRInput.IsRightButtonUp(VRInput.ControllerButtons.USE_BUTTON); // for the right controller, the Use button must be hold on the left controller altUse = VRInput.IsLeftButtonPress(VRInput.ControllerButtons.USE_BUTTON); altUseUp = VRInput.IsLeftButtonUp(VRInput.ControllerButtons.USE_BUTTON); break; case VRInput.VRDevice.PC_HAND: grabDown = VRInput.IsGeneralButtonDown(VRInput.GeneralButtons.FIRE_1); grabUp = VRInput.IsGeneralButtonUp(VRInput.GeneralButtons.FIRE_1); useDown = VRInput.IsGeneralButtonDown(VRInput.GeneralButtons.FIRE_2); useUp = VRInput.IsGeneralButtonUp(VRInput.GeneralButtons.FIRE_2); // for the keyboard, the JUMP button must be held altUse = VRInput.IsGeneralButtonDown(VRInput.GeneralButtons.JUMP); altUseUp = VRInput.IsGeneralButtonUp(VRInput.GeneralButtons.JUMP); break; default: break; } // stop the "alternative use" action - call OnAltUseEnd // for all components of the hovered object that have an implementation of this method if (altUseUp) { foreach (var hoveredObjectComponent in hoveredObjectComponents) hoveredObjectComponent.OnAltUseEnd(this, controller); } // can grab and use hovered object if (hoveredObject != null) { if (grabDown && grabbedObject == null) { grabbedObject = hoveredObject; grabbedObjectComponents.Clear(); grabbedObjectComponents.AddRange(hoveredObjectComponents); foreach (var grabbedObjectComponent in grabbedObjectComponents) { if (VRInteractionManager.IsGrabbed(grabbedObjectComponent)) { VRBaseInteraction inter = VRInteractionManager.GetGrabInteraction(grabbedObjectComponent); VRInteractionManager.StopGrab(inter); } grabbedObjectComponent.OnGrabBegin(this, controller); interactablesState.SetGrabbed(grabbedObjectComponent, true, this); } } if (useDown) { usedObject = hoveredObject; usedObjectComponents.Clear(); usedObjectComponents.AddRange(hoveredObjectComponents); foreach (var usedObjectComponent in usedObjectComponents) { usedObjectComponent.OnUseBegin(this, controller); interactablesState.SetUsed(usedObjectComponent, true, this); } } // call OnAltUse for all components of the hovered object that have an implementation of this method if (altUse) { foreach (var hoveredObjectComponent in hoveredObjectComponents) if (hoveredObjectComponent.CurrentState != VRBaseInteractable.INTERACTABLE_STATE.ALT_USED) hoveredObjectComponent.OnAltUse(this, controller); altUse = false; } } // ... } ``` </details>
4. Specify the list of materials that will be applied to the object. Select the ***laser_pointer*** node and click **Edit** in the *Parameters* window. Then find the ***VRLaserPointer*** component, specify the number of elements for the *Materials* array (for example, 3) and drag the required materials from the *Materials* window to fill the array. ![](laser_pointer_materials.png)
5. Save changes (*Ctrl+S*) and press the **Play** button to run the application.


### 3.7. Customizing Menu


The VR template includes two menus: the first one is attached to the HMD position, and the second - to the hand. In the VR sample, the ***menu_attached_to_head*** node (*ObjectGui*) is used for the main menu, and the ***menu_attached_to_hand*** node (*ObjectGui*) - for the additional menu.


![](custom_menu_nodes.png)


All menu nodes have the same `VRMenuSample.cs` component assigned. It is inherited from the base ***VRBaseUI*** component that implements a user interface. In general, the user interface is implemented as follows:


1. Inherit a new component from the base ***VRBaseUI***.
2. Implement the user interface with the required widgets in the overridden *InitGui()* method.
3. Implement handlers for processing widgets events (pressing a button, selecting elements in the drop-down menu, etc.).
4. Subscribe the corresponding widgets to the events in the *InitGui()* method.
5. Assign the component to the *ObjectGui* node that will display the user interface.


Let's create a new menu for the left controller and add the quit button:


1. Inherit a new component from the base ***VRBaseUI***, call it ***VRHandMenu*** and copy the following code to it: <details> <summary>VRHandMenu.cs | Close</summary> `VRHandMenu.cs` ```csharp using System; using System.Collections; using System.Collections.Generic; using Unigine; public partial class VRHandMenu : VRBaseUI { // declare required widgets private WidgetSprite background; private WidgetVBox VBox; private WidgetButton quitButton; private WidgetWindow window; private WidgetButton okButton; private WidgetButton cancelButton; private WidgetHBox HBox; // overriden method that is called on interface initialization, // it adds the required widgets and subscribes to events protected override void InitGui() { if (gui == null) return; background= new WidgetSprite(gui, "core/textures/common/black.texture"); background.Color = new vec4(1.0f, 1.0f, 1.0f, 0.5f); gui.AddChild(background, Gui.ALIGN_BACKGROUND | Gui.ALIGN_EXPAND); // add a vertical column container WidgetVBox to GUI VBox = new WidgetVBox(); VBox.Width = gui.Width; VBox.Height = 100; gui.AddChild(VBox, Gui.ALIGN_OVERLAP|Gui.ALIGN_CENTER); // add the quit button to the container quitButton = new WidgetButton(gui, "QUIT APPLICATION"); quitButton.FontSize = 20; VBox.AddChild(quitButton); quitButton.EventClicked.Connect(ButtonQuitClicked); VBox.Arrange(); // create a quit confirmation window window = new WidgetWindow(gui, "Quit Application"); window.FontSize = 20; // add a horizontal row container WidgetHBox to the confirmation window HBox = new WidgetHBox(); HBox.Width = window.Width; HBox.Height = 100; window.AddChild(HBox); // add the "OK" button and assign the "OkClicked" handler that will close the application okButton = new WidgetButton(gui, "OK"); okButton.FontSize = 20; HBox.AddChild(okButton); okButton.EventClicked.Connect(OkClicked); // add the "Cancel" button and assign the "OkClicked" handler that will close the confirmation window cancelButton = new WidgetButton(gui, "Cancel"); cancelButton.FontSize = 20; HBox.AddChild(cancelButton); cancelButton.EventClicked.Connect(CancelClicked); } // function to be executed on clicking "quitButton" private void ButtonQuitClicked() { gui.AddChild(window, Gui.ALIGN_OVERLAP | Gui.ALIGN_CENTER); } // function to be executed on clicking "cancelButton" private void CancelClicked() { gui.RemoveChild(window); } // function to be executed on clicking "okButton" private void OkClicked() { // quit the application Engine.Quit(); } } ``` </details>
2. Assign the `VRHandMenu.cs` component to the ***menu_attached_to_hand*** node. And disable the `VRMenuSample.cs` component which is assigned to this node by default. ![](../../learn/13_vr_app/menu_attached_to_hand.png)
3. Save changes (*Ctrl+S*) and click **Play** to run the application.


![](custom_menu.png)


### 3.8. Adding a New Interactable Object


Let's add a new type of interactable object that we can grab, hold, and throw (i.e. it will be inherited from the ***VRBaseInteractable*** component) with an additional feature: some visual effect (for example, smoke) will appear when we grab the object and, it will disappear when we release the object. In addition, it will display certain text in the console, if the corresponding option is enabled.


1. Create a new ***VRObjectVFX*** component and add the following code to it: <details> <summary>VRObjectVFX.cs | Close</summary> `VRObjectVFX.cs` ```csharp using System; using System.Collections; using System.Collections.Generic; using Unigine; public partial class VRObjectVFX : VRBaseInteractable { // an asset with an effect that occurs when the object is grabbed public AssetLinkNode vfx_node = null; private Node vfx = null; private Unigine.Object obj = null; // this method is called for the interactable object each frame private void Update() { // update transformation of the effect if the object is grabbed if(CurrentState == VRBaseInteractable.INTERACTABLE_STATE.GRABBED) vfx.WorldTransform = node.WorldTransform; } // this overridden method is called after component initialization // (you can implement checks here) protected override void OnReady() { // check if the asset with the visual effect is specified if (vfx_node == null) { Log.Error($"{nameof(VRObjectVFX)} error: 'vfx_node' is not assigned.\n"); Enabled = false; return; } else { vfx = vfx_node.Load(); vfx.Enabled = false; } } // this overridden method is called when grabbing the interactable object public override void OnGrabBegin(VRBaseInteraction interaction, VRBaseController controller) { // show the effect vfx.Enabled = true; // set the current object state to GRABBED CurrentState = VRBaseInteractable.INTERACTABLE_STATE.GRABBED; } // this overridden method is called when releasing the interactable object public override void OnGrabEnd(VRBaseInteraction interaction, VRBaseController controller) { // hide the effect vfx.Enabled = false; // set the current object state to NOT_INTERACT CurrentState = VRBaseInteractable.INTERACTABLE_STATE.NOT_INTERACT; } } ``` </details>
2. Assign the `VRObjectVFX.cs` component to the ***cylinder*** node (the child of the ***kinematic_movable*** dummy node).
3. Drag the `vr/particles/smoke.node` asset to the *Vfx Node* field. This node stores the particle system representing the smoke effect. It is available in the `vr/particles` folder of *UNIGINE Starter Course Projects* add-on. ![](smoke_node.png)
4. Save changes (*Ctrl+S*) and press the **Play** button to run the application.


Now if you grab and hold the cylinder, it will emit smoke:


![](smoke_effect.png)


## 4. Packing a Final Build


Now, you can build the project. Specify the required settings and ensure the final build includes all content, code, and necessary libraries. Ensure all unused assets are deleted. And don't forget to enable the VR modes!


To get more information on how to pack the final build, refer to the [Programming Quick Start](../../start/quick_start/build/index_cs.md) section.


## Where to Go From Here


Congratulations! Now, you can continue developing the project on your own. Here are some helpful recommendations for you:


- Try to analyze the source code of the sample further to figure out how it works and use it as a reference to write your own code.
- Read the *[Virtual Reality Best Practices](../../content/vr/index.md)* article for more information and tips on preparing content for VR and enhancing the user experience.
- Learn more about the Component System by reading the *[Component System](../../principles/component_system/component_system_cs/index.md)* article.
- Check out the *[Component System Usage Example](../../code/csharp/usage/using_cs_component_system/index.md)* for more details on implementing logic using the Component System.
