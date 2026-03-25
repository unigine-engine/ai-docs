# Unigine::WidgetManipulator Class (CS)

**Inherits from:** Widget


This base class creates a draggable 3D manipulator.


### See Also


- Usage example: [Using Manipulators to Transform Objects](../../../code/usage/manipulator_component/index_cs.md)
- C++ sample


## WidgetManipulator Class

### Properties

## mat4 Modelview

The current projection matrix of the handler.
## mat4 Projection

The current model-view matrix of the handler.
## mat4 Transform

The current transformation matrix of the handler.
## mat4 Basis

The current basis of the coordinate system for the handler. it can either be the world coordinates (the identity matrix) or coordinates of the parent node if the manipulated node is a child.
## vec4 Color

The current color for a manipulator.
## int Size

The current handle size of the manipulator. depending on the handle shape, this can be a radius or an altitude.
## float Step

The step which is used to align objects.
## int Mask

The mask that hides axis arrows (along *X*, *Y* or *Z*) of the handler.
## Gui RenderGui

The current render gui.
## 🔒︎ bool IsFocusAxis

The value indicating if any axis of the manipulator is currently in focus.
## 🔒︎ bool IsHoverAxis

The value indicating if any axis of the manipulator is currently hovered.
## 🔒︎ int FocusedAxis

The number of the manipulator axis, that is currently in focus.
### Members

---

## WidgetManipulator ( Gui gui )

WidgetManipulator constructor. Creates a manipulator widget and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - GUI instance.

## WidgetManipulator ( )

WidgetManipulator constructor. Creates a manipulator widget and adds it to the Engine GUI.
