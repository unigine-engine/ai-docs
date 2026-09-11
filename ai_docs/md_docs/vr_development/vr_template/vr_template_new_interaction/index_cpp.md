# Customizing VR Controls (CPP)


So you've got the VR Template running - now you want to change what the buttons do. Maybe grab should be on the trigger instead of the grip, or you don't need the inventory and want that button for something else entirely. Let's see how the input system works and how to tweak it.


### How Input Works


The template doesn't scatter button checks across gameplay code. Instead, there's a clean three-layer setup:


- **Physical button** - what the player actually presses on the controller (grip, trigger, X, Y, stick click, etc.)
- **Intent** - an abstract action: *GRAB*, *USE*, *TELEPORT*, *MENU*, *INVENTORY*. All gameplay code speaks in these terms - it never asks "is button X pressed?", it asks "is GRAB pressed?"
- **Callback** - when an intent fires, *[VRPlayer](../../../api/modules/vr/components/players/class.vrplayer.md)* calls the matching method (*grabIt*, *useIt*, *throwIt*, etc.) on every *[VRInteractable](../../../api/modules/vr/components/class.vrinteractable.md)* property of the object you're interacting with.


The translation from physical buttons to intents happens in one place - *[VRHandController](../../../api/modules/vr/components/players/class.vrhandcontroller.md)*. That's the only file you need to touch when remapping controls.


### Remapping a Button


Let's say you want to swap two buttons, or move an action to a different one. Open *[VRHandController](../../../api/modules/vr/components/players/class.vrhandcontroller.md)* and find these three methods:


- *getControllerButtonDown()* - fires once when the button is first pressed
- *getControllerButtonPressed()* - fires every frame while the button is held
- *getControllerButtonUp()* - fires once when the button is released


Each one is a switch-case that maps intents to physical buttons. Here's a fragment from *getControllerButtonDown()* with the default mappings:


```cpp
switch (button)
{
// ... TELEPORT and USE have more complex axis-based logic ...

case Buttons::GRAB:
	return controller->isButtonDown(Input::VR_BUTTON_GRIP);
case Buttons::MENU:
	return controller->isButtonDown(Input::VR_BUTTON_APPLICATION)
		|| controller->isButtonDown(Input::VR_BUTTON_Y);
case Buttons::INVENTORY:
	return controller->isButtonDown(Input::VR_BUTTON_X);
}

```


Want to move *INVENTORY* from *X* to *Y*? Just change the constant:


```cpp
case Buttons::INVENTORY:
	return controller->isButtonDown(Input::VR_BUTTON_Y); // was VR_BUTTON_X

```


> **Warning:** Make sure you update all three methods - *getControllerButtonDown*, *getControllerButtonPressed*, and *getControllerButtonUp*. They must stay in sync, otherwise an action might start on one button and end on another.


One thing to keep in mind: standard VR controllers don't have many buttons, and the template already uses most of them. If you put two actions on the same button, both will fire at once. Check the other cases in the switch before remapping to avoid surprises.


> **Notice:** Hand tracking uses a separate controller - *[VRHandTracking](../../../api/modules/vr/components/players/class.vrhandtracking.md)*. It maps intents to hand gestures instead of physical buttons, so it has its own mapping logic.


### What About Adding a New Action?


If remapping existing buttons isn't enough and you need a completely new action (say, a secondary use for held objects), the steps are:


1. Add a new value to the *Buttons* enum in *[VRController](../../../api/modules/vr/components/players/class.vrcontroller.md)*.
2. Add a corresponding case to the three mapping methods in *[VRHandController](../../../api/modules/vr/components/players/class.vrhandcontroller.md)*.
3. Add a new virtual method to *[VRInteractable](../../../api/modules/vr/components/class.vrinteractable.md)*.
4. Call it from *[VRPlayer](../../../api/modules/vr/components/players/class.vrplayer.md)*'s game loop, next to the existing action checks.


Sounds straightforward, but there's a catch: **standard VR controllers have very few buttons, and the template already uses all of them.** Any new intent either takes over a button from an existing action or shares one - both lead to conflicts.


In practice, most VR projects solve this differently: instead of adding new intents, they give objects custom behavior through the existing *USE* action. Each object decides for itself what "use" means - a door opens, a lever toggles, a tool activates. One button, many behaviors. For a hands-on example of this approach, see [Adding a New Interactable Object](../../../vr_development/vr_template/vr_template_new_interactable/index_cpp.md).
