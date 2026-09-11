# In-World UI (CPP)


VR interfaces don't have to live on a flat screen - the VR Template lets you place menus, tooltips, and visual indicators right inside the 3D world, where they feel natural and stay within arm's reach.


### Switching Nodes


Menus in the VR Template are opened and closed using utility properties that toggle node state based on player input:


- **[NodeSwitchEnableByKey](../../../api/templates/template_vr/global/class.nodeswitchenablebykey.md)** Toggles assigned nodes when the Menu button on the chosen controller is pressed. Used for opening UI panels like the Hand Menu or Mixed Reality Menu.
- **[NodeSwitchEnableByGrab](../../../api/templates/template_vr/global/class.nodeswitchenablebygrab.md)** Activates or hides nodes when the player **grabs** the object carrying this property.
- **[NodeSwitchEnableByGesture](../../../api/templates/template_vr/global/class.nodeswitchenablebygesture.md)** Switches node states in response to a recognized hand-tracking gesture (e.g., touching the wrist).


Each property simply inverts the enabled state of linked nodes.


## Attaching Objects to the Player


In VR, you often need objects that follow the player - a menu pinned to your wrist, a HUD floating in front of your eyes, or even a hat stuck to your head. The VR Template provides two utility properties for this:


- **[AttachToHand](../../../api/modules/vr/components/objects/class.attachtohand.md)** Locks a node to one of the VR controllers. You choose which hand (left or right) and set the offset. The Hand Menu uses this to stay near your wrist.
- **[AttachToHead](../../../api/modules/vr/components/objects/class.attachtohead.md)** Locks a node to the headset so it follows your gaze. The Head Menu uses this to stay in view.


Assign either property to any node you want to follow the player, and configure the target controller and transform offset in the property settings.


## World Menu


The World Menu is a panel placed directly in the scene - think of it as a touchscreen bolted to a wall or a table.


In the VR Template, it is attached to a button on the table in front of you. Press the button and a small menu pops up, showing the basic structure of a world-space UI. Use it as a starting point for building your own in-world menus.


Built with: [WorldMenuSampleGui](../../../api/templates/template_vr/gui/class.worldmenusamplegui.md)


## Hand Menu


The Hand Menu is always attached to the player's hand. Press the Menu button on the left controller and a small panel appears near your wrist, letting you toggle options like teleportation or joystick movement on the fly.


You can interact with it using either controller rays or direct hand-tracking gestures.


Built with: [AttachToHand](../../../api/modules/vr/components/objects/class.attachtohand.md), [HandMenuSampleGui](../../../api/templates/template_vr/gui/class.handmenusamplegui.md)


## Head Menu


The Head Menu stays fixed relative to your view - it moves and rotates together with your head, so it's always in sight.


In the VR Template, the Head Menu is used as the [Mixed Reality Menu](../../../vr_development/vr_template/vr_template_mixed_reality/index.md), providing controls for camera passthrough and video settings.


Built with: [AttachToHead](../../../api/modules/vr/components/objects/class.attachtohead.md), [MixedRealityMenuGui](../../../api/templates/template_vr/gui/class.mixedrealitymenugui.md)


## Tooltips


Point at an object and a floating label appears next to it - that's the tooltip system. The *[Tooltip](../../../api/modules/vr/components/objects/tooltip/class.tooltip.md)* property displays text on a dynamically sized widget background and can be configured per-object.


The *[TooltipTextSwitcher](../../../api/templates/template_vr/objects/class.tooltiptextswitcher.md)* property allows switching tooltip text depending on the object's current state (e.g. showing "Grab" when idle and "Release" when held).


## Object Outlining


When your hand or controller gets close to an interactable object, it lights up with an outline - instant feedback showing you what you're about to grab.


The *[ObjectOutliner](../../../api/modules/vr/components/objects/class.objectoutliner.md)* property handles the outline rendering. It activates the outline material on hover and removes it when the hand moves away. A specialized *[SocketOutliner](../../../api/modules/vr/components/objects/class.socketoutliner.md)* variant highlights sockets when a compatible plug is nearby.
