# Generator Component

**Inherits from:** ComponentBase, EventSignal


Generator is a component that monitors two sockets and sends a signal when both are connected via a physical cable. It listens for grab/throw events on its sockets and emits a float signal (0 or 1) through the **[EventSignal](../../../../api/modules/vr/components/class.eventsignal.md)** interface.


The component checks if a **[VRObjectPhysicalCable](../../../../api/modules/vr/components/objects/class.vrobjectphysicalcable.md)** connects both sockets. When connected, the signal value is 1; otherwise, it is 0.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| first_socket | *Node* | First socket node (should have a **[VRSocketObject](../../../../api/modules/vr/components/objects/class.vrsocketobject.md)** component). |
| second_socket | *Node* | Second socket node (should have a **[VRSocketObject](../../../../api/modules/vr/components/objects/class.vrsocketobject.md)** component). |


### See Also


- **[EventSignal](../../../../api/modules/vr/components/class.eventsignal.md)**
- **[VRObjectPhysicalCable](../../../../api/modules/vr/components/objects/class.vrobjectphysicalcable.md)**
- **[VRSocketObject](../../../../api/modules/vr/components/objects/class.vrsocketobject.md)**
- **[Lamp](../../../../api/templates/template_vr/objects/class.lamp.md)**
