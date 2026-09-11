# Customizing VR Controls (CS)


So you've got the VR Template running - now you want to change what the buttons do. Maybe grab should be on the trigger instead of the grip, or you don't need the inventory and want that button for something else entirely. Let's see how the input system works and how to tweak it.


### How Input Works


The template doesn't scatter button checks across gameplay code. Instead, there's a clean three-layer setup:


- **Physical button** - what the player actually presses on the controller (grip, trigger, X, Y, stick click, etc.)
- **Intent** - an abstract action: *GRAB_BUTTON*, *USE_BUTTON*, *TELEPORTATION_BUTTON*, etc., defined in *[InputSystem](../../../api/templates/template_vr_csharp/vr_input/class.inputsystem.md)*. All gameplay code speaks in these terms.
- **Callback** - when an intent fires, the interaction handler calls methods like *OnGrabBegin*, *OnUseBegin*, *OnGrabEnd* on every *[VRBaseInteractable](../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)* component of the target object.


The translation from physical buttons to intents is stored in *[VRControllerInput](../../../api/templates/template_vr_csharp/vr_input/class.vrcontrollerinput.md)* components - and you configure them right in the Editor, no code required.


### Remapping a Button


Let's say you want to move an action to a different button. Open your world and find the controller nodes (e.g. *left_preset_0*, *right_preset_0*) - they have *[VRControllerInput](../../../api/templates/template_vr_csharp/vr_input/class.vrcontrollerinput.md)* components attached.


Each action has a **Bind** with a type that determines how the physical input is read:


- **BUTTON** - a regular button press (e.g. *VR_BUTTON_GRIP*, *VR_BUTTON_X*)
- **TOUCH** - a touch sensor on a button (finger resting on it without pressing)
- **CLICK_ON_AXIS** - an axis crossing a threshold (e.g. trigger pulled past halfway)


To remap, simply change the physical button in the dropdown. For example, to move *Inventory* from *X* to *Y*, select *Y* in the *Inventory Button* bind. That's it - no rebuild needed.


![VRControllerInput Component](../../../learn/13_vr_app/vr_controller_input.png)


> **Warning:** Each hand has its own *[VRControllerInput](../../../api/templates/template_vr_csharp/vr_input/class.vrcontrollerinput.md)* component. If you want the same change on both hands, update both.


One thing to keep in mind: standard VR controllers don't have many buttons, and the template already uses most of them. If you put two actions on the same button, both will fire at once - so check what's already assigned before remapping.


> **Notice:** Hand tracking uses a separate component - *[VRHandTrackingInput](../../../api/templates/template_vr_csharp/vr_input/class.vrhandtrackinginput.md)*. It maps intents to hand gestures instead of physical buttons.


### What About Adding a New Action?


If remapping existing buttons isn't enough and you need a completely new action, the steps are:


1. Add a new value to the *ControllerButtons* enum in *[InputSystem](../../../api/templates/template_vr_csharp/vr_input/class.inputsystem.md)*.
2. Add a new *Bind* field and matching cases in *[VRControllerInput](../../../api/templates/template_vr_csharp/vr_input/class.vrcontrollerinput.md)*.
3. Add new virtual callbacks to *[VRBaseInteractable](../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)*.
4. Dispatch them from the interaction handler (e.g. *[VRHandShapeInteraction](../../../api/templates/template_vr_csharp/interactions/class.vrhandshapeinteraction.md)*).
5. After rebuilding, configure the physical button for the new bind in the Editor.


Sounds straightforward, but there's a catch: **standard VR controllers have very few buttons, and the template already uses all of them.** Any new intent either takes over a button from an existing action or shares one - both lead to conflicts.


In practice, most VR projects solve this differently: instead of adding new intents, they give objects custom behavior through the existing *USE* action. Each object decides for itself what "use" means - a door opens, a lever toggles, a tool activates. One button, many behaviors. For a hands-on example of this approach, see [Adding a New Interactable Object](../../../vr_development/vr_template/vr_template_new_interactable/index_cs.md).
