# Unigine.EventConnections Class (CPP)

**Header:** #include <UnigineCallback.h>


This class is a container for the *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* class used to store several *EventConnection* instances. The connections stored in one and the same *EventConnections* container may refer to different events.


## EventConnections Class

### Members

## bool empty () const

Returns the current value indicating if the container is empty.
### Return value

**true** if the container is empty; otherwise **false**.
---

## void disconnectAll ( )

Cancels the connection for all *EventConnection* instances in the container.
