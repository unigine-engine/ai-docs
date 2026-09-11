# Unigine.EventConnection Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class stores the information on the link between the event and the callback (`UnigineCallback.h`).


## EventConnection Class

### Members

## void setEnabled ( int enabled )

Sets a new value indicating if the callback is enabled. If the callback is disabled, it won't be called when the event is triggered.
### Arguments

- *int* **enabled** - The callback

## int isEnabled () const

Returns the current value indicating if the callback is enabled. If the callback is disabled, it won't be called when the event is triggered.
### Return value

Current callback
## bool isValid () const

Returns the current value indicating if the connection between the event and the callback is valid.
### Return value

**true** if connection between the event and the callback is enabled ; otherwise **false**.
---
