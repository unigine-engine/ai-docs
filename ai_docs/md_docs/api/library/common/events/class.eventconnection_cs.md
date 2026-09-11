# Unigine.EventConnection Class (CS)


This class stores the information on the link between the event and the callback (`UnigineCallback.h`).


## EventConnection Class

### Properties

## bool Enabled

The value indicating if the callback is enabled. If the callback is disabled, it won't be called when the event is triggered.
## 🔒︎ bool IsValid

The value indicating if the connection between the event and the callback is valid.
### Members

---

## void Disconnect ( )

Cancels the connection between the event and the callback.
