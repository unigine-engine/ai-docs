# DoorTranslatable Component

**Inherits from:** ComponentBase, EventSlot


DoorTranslatable is a component that translates a node (e.g., a door) between two positions based on a received float signal value. The value is clamped to the [0, 1] range and linearly interpolated between the minimum and maximum translation offsets.


The component implements the **[EventSlot](../../../../api/modules/vr/components/class.eventslot.md)** interface to receive float values from an **[EventSignal](../../../../api/modules/vr/components/class.eventsignal.md)** source (e.g., a handle or generator).


### Component Parameters


| Name | Type | Description |
|---|---|---|
| min_translate | *Vec3* | Translation offset when the signal value is 0. |
| max_translate | *Vec3* | Translation offset when the signal value is 1. |


### See Also


- **[EventSlot](../../../../api/modules/vr/components/class.eventslot.md)**
- **[EventSignal](../../../../api/modules/vr/components/class.eventsignal.md)**
- **[ObjectHandleTranslatable](../../../../api/modules/vr/components/objects/class.objecthandletranslatable.md)**


## DoorTranslatable Class

---

## void receiveFloat ( )

Receives a float value and translates the node accordingly between min_translate and max_translate.
### Arguments
