# Unigine::WidgetManipulator Class (CS)

**Inherits from:** Widget


This base class creates a draggable 3D manipulator.


### See Also


- Usage example: [Using Manipulators to Transform Objects](../../../code/usage/manipulator_component/index_cs.md)
- C++ sample


## WidgetManipulator Class

### Properties

## mat4 Modelview

The model-view matrix of the handler.
## mat4 Projection

The projection matrix of the handler.
## mat4 Transform

The transformation matrix of the handler.
## mat4 Basis

The basis of the coordinate system for the handler. It can either be the world coordinates (the identity matrix) or coordinates of the parent node if the manipulated node is a child.
## vec4 Color

The color for the manipulator. The provided value is clamped to a range **[0;1]**.
## int Size

The handle size of the manipulator, in pixels. Depending on the handle shape, this can be a radius or an altitude.
## float Step

The step used to align objects, in units.
## int Mask

The mask that hides axis arrows (along *X*, *Y*, or *Z*) of the handler.
## Gui RenderGui

The render GUI for the manipulator.
## 🔒︎ bool IsFocusAxis

The value indicating if any axis of the manipulator is currently in focus.
## 🔒︎ bool IsHoverAxis

The value indicating if any axis of the manipulator is currently hovered.
## 🔒︎ int FocusedAxis

The number of the manipulator axis that is currently in focus. The values depend on the manipulator's type:
- [WidgetManipulatorRotator](../../../api/library/gui/class.widgetmanipulatorrotator_cs.md): one of the [AXIS_*](../../../api/library/gui/class.widgetmanipulatorrotator_cs.md#AXIS_UNKNOWN) variables.
- [WidgetManipulatorScaler](../../../api/library/gui/class.widgetmanipulatorscaler_cs.md): one of the [AXIS_*](../../../api/library/gui/class.widgetmanipulatorscaler_cs.md#AXIS_UNKNOWN) variables.
- [WidgetManipulatorTranslator](../../../api/library/gui/class.widgetmanipulatortranslator_cs.md): one of the [AXIS_*](../../../api/library/gui/class.widgetmanipulatortranslator_cs.md#AXIS_UNKNOWN) variables.


### Members

---

## WidgetManipulator ( Gui gui )

WidgetManipulator constructor. Creates a manipulator widget and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - GUI instance.

## WidgetManipulator ( )

WidgetManipulator constructor. Creates a manipulator widget and adds it to the Engine GUI.
