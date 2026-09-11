# JSBSim::WidgetJSBSimProperties Component

**Inherits from:** ComponentBase


WidgetJSBSimProperties provides a debug UI for viewing and editing **JSBSim** property values at runtime. It displays all properties exposed by the **JSBSim** **FDM** in a searchable, scrollable list.


Features include live property value display with values updating in real-time, editable values allowing modification of writable properties directly, search filter to quickly find properties by name, and read/write indicators showing which properties can be modified.


This widget is primarily intended for debugging and tuning aircraft models during development.


### See Also


- **[JSBSim::FDMJSBSim](../../../api/modules/jsbsim/class.fdmjsbsim.md)**


## WidgetJSBSimProperties Class

---

## void setFDM ( )

Sets the FDM instance whose properties will be displayed.
### Arguments
