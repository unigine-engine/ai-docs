# In-World UI (CS)


VR interfaces don't have to live on a flat screen - the VR Template lets you place menus, tooltips, and visual indicators right inside the 3D world, where they feel natural and stay within arm's reach.


### Switching Nodes


Menus in the VR Template are opened and closed using utility components that toggle node state based on player input:


- **[VRNodeSwitchEnableByKey](../../../api/templates/template_vr_csharp/interactions/class.vrnodeswitchenablebykey.md)** Toggles assigned nodes when the Action Button on the chosen controller is pressed. Used for opening UI panels like the Hand Menu.
- **[VRNodeSwitchEnableByGrab](../../../api/templates/template_vr_csharp/interactions/class.vrnodeswitchenablebygrab.md)** Activates or hides nodes when the player **grabs** the object carrying this component.


Each component simply inverts the enabled state of linked nodes.


## Attaching Objects to the Player


In VR, you often need objects that follow the player - a menu pinned to your wrist, a HUD floating in front of your eyes, or even a hat stuck to your head. The VR Template provides two utility components for this:


- **[VRAttachToHand](../../../api/templates/template_vr_csharp/transformations/class.vrattachtohand.md)** Locks a node to one of the VR controllers. You choose which hand (left or right) and set the offset. The Hand Menu uses this to stay near your wrist.
- **[VRAttachToHead](../../../api/templates/template_vr_csharp/transformations/class.vrattachtohead.md)** Locks a node to the headset so it follows your gaze. The Head Menu uses this to stay in view.


Assign either component to any node you want to follow the player, and configure the target controller and transform offset in the component settings.


## World Menu


The World Menu is a panel placed directly in the scene - think of it as a touchscreen bolted to a wall or a table.


In the VR Template, it is attached to a button on the table in front of you. Press the button and a small menu pops up, showing the basic structure of a world-space UI. Use it as a starting point for building your own in-world menus.


## Hand Menu


The Hand Menu is always attached to the player's hand. Press the Action Button on the left controller and a small panel appears near your wrist, letting you toggle options like teleportation or joystick movement on the fly.


You can interact with it using either controller rays or direct hand-tracking gestures.


Built with: [VRAttachToHand](../../../api/templates/template_vr_csharp/transformations/class.vrattachtohand.md), [VRHandMenuInteraction](../../../api/templates/template_vr_csharp/interactions/class.vrhandmenuinteraction.md), [VRHandTrackingMenuInteraction](../../../api/templates/template_vr_csharp/interactions/class.vrhandtrackingmenuinteraction.md)


## Head Menu


The Head Menu stays fixed relative to your view - it moves and rotates together with your head, so it's always in sight.


Built with: [VRAttachToHead](../../../api/templates/template_vr_csharp/transformations/class.vrattachtohead.md), [VRPCHeadMenuInteraction](../../../api/templates/template_vr_csharp/interactions/class.vrpcheadmenuinteraction.md)


## Tooltips


Point at an object and a floating label appears next to it - that's the tooltip system. The *[VRTooltip](../../../api/templates/template_vr_csharp/ui/class.vrtooltip.md)* component displays text on a dynamically sized widget background and can be configured per-object.


The *[TooltipTextSwitcher](../../../api/templates/template_vr_csharp/ui/class.tooltiptextswitcher.md)* component allows switching tooltip text depending on the input mode - for example, showing one text for VR controllers and another for keyboard and mouse.


## Object Outlining


When your hand or controller gets close to an interactable object, it lights up with an outline - instant feedback showing you what you're about to grab.


The *[ObjectOutliner](../../../api/templates/template_vr_csharp/interactions/class.objectoutliner.md)* component handles the outline rendering. For socket objects, a specialized *[VRSocketOutliner](../../../api/templates/template_vr_csharp/interactions/class.vrsocketoutliner.md)* variant highlights sockets when a compatible plug is nearby.
