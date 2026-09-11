# ObjectLabeling Component

**Inherits from:** ComponentBase


ObjectLabeling is a singleton component that displays a text label on objects in the scene. When a target object is set, the label is positioned at the hit point and shows the object's name.


Typically used with eye tracking or ray intersection to label the object the user is looking at or pointing to.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| text | *Node* | Reference to the ObjectText node used to display the label. |


### See Also


- **[EyetrackingPointer](../../../../api/templates/template_vr/global/class.eyetrackingpointer.md)**


## ObjectLabeling Class

---

## static get ( )

Returns the singleton instance of the ObjectLabeling component.
### Return value

Singleton instance of the ObjectLabeling component.
## void setTarget ( )

Sets the target object and positions the label at the specified hit point.
### Arguments
