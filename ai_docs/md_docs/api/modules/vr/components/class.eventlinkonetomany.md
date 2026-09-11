# EventLinkOneToMany Component

**Inherits from:** ComponentBase


EventLinkOneToMany is a component that connects a single **[EventSignal](../../../../api/modules/vr/components/class.eventsignal.md)** emitter to multiple **[EventSlot](../../../../api/modules/vr/components/class.eventslot.md)** receivers. It provides a one-to-many event routing mechanism, allowing one signal source to broadcast events to multiple slot receivers.


When the emitter triggers an event (*float*, *string*, or *int*), the component forwards the event to all connected slots.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| emitter_param | *Node* | Reference to the node containing the EventSignal component that emits events. |
| slots_param | *Array<Node>* | Array of nodes containing EventSlot components that receive events. |


### See Also


- **[EventSignal](../../../../api/modules/vr/components/class.eventsignal.md)**
- **[EventSlot](../../../../api/modules/vr/components/class.eventslot.md)**
