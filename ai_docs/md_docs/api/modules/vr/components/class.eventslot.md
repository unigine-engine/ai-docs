# EventSlot Class


EventSlot is an abstract interface class that provides event reception capabilities for VR components. It defines virtual methods for receiving typed events (float, string, int) that are emitted by **[EventSignal](../../../../api/modules/vr/components/class.eventsignal.md)** implementations.


Components that need to receive events should inherit from this class and override the receive methods to handle incoming events.


### See Also


- **[EventSignal](../../../../api/modules/vr/components/class.eventsignal.md)**
- **[EventLinkOneToMany](../../../../api/modules/vr/components/class.eventlinkonetomany.md)**


## EventSlot Class

---

## void receiveFloat ( )

Called when a float value is received from an event signal. Override this method to handle float events.
### Arguments

## void receiveString ( )

Called when a string value is received from an event signal. Override this method to handle string events.
### Arguments

## void receiveInt ( )

Called when an integer value is received from an event signal. Override this method to handle integer events.
### Arguments
