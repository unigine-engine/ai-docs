# Unigine.EventConnection Class (CPP)

**Header:** #include <UnigineCallback.h>


This class stores the information on the link between the event and the callback (`UnigineCallback.h`).


## EventConnection Class

### Members

## void setEnabled ( bool enabled )

Sets a new value indicating if the callback is enabled. If the callback is disabled, it won't be called when the event is triggered.
### Arguments

- *bool* **enabled** - Set **true** to enable callback; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if the callback is enabled. If the callback is disabled, it won't be called when the event is triggered.
### Return value

**true** if callback is enabled ; otherwise **false**.
## bool isValid () const

Returns the current value indicating if the connection between the event and the callback is valid.
### Return value

**true** if connection between the event and the callback is enabled ; otherwise **false**.
---

## void disconnect ( )

Cancels the connection between the event and the callback.
