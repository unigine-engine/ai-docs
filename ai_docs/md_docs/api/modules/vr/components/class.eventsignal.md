# EventSignal Class


EventSignal is an interface class that provides event emission capabilities for VR components. It allows components to emit typed events (float, string, int) that can be received by **[EventSlot](../../../../api/modules/vr/components/class.eventslot.md)** implementations.


Components that need to emit events should inherit from this class and use the protected emit methods to trigger events.


### See Also


- **[EventSlot](../../../../api/modules/vr/components/class.eventslot.md)**
- **[EventLinkOneToMany](../../../../api/modules/vr/components/class.eventlinkonetomany.md)**


## EventSignal Class

---

## getEventEmitFloat ( )

Returns the event that is triggered when a float value is emitted.
### Return value

Event for float values.
## getEventEmitString ( )

Returns the event that is triggered when a string value is emitted.
### Return value

Event for string values.
## getEventEmitInt ( )

Returns the event that is triggered when an integer value is emitted.
### Return value

Event for integer values.
