# Unigine::WidgetManipulator Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This base class creates a draggable 3D manipulator.


### See Also


- Usage example: [Using Manipulators to Transform Objects](../../../code/usage/manipulator_component/index.md)
- C++ sample


## WidgetManipulator Class

### Members

## void setModelview ( Mat4 modelview )

Sets a new model-view matrix of the handler.
### Arguments

- *Mat4* **modelview** - The model-view matrix of the handler

## Mat4 getModelview () const

Returns the current model-view matrix of the handler.
### Return value

Current model-view matrix of the handler
## void setProjection ( mat4 projection )

Sets a new projection matrix of the handler.
### Arguments

- *mat4* **projection** - The projection matrix of the handler

## mat4 getProjection () const

Returns the current projection matrix of the handler.
### Return value

Current projection matrix of the handler
## void setTransform ( Mat4 transform )

Sets a new transformation matrix of the handler.
### Arguments

- *Mat4* **transform** - The transformation matrix of the handler

## Mat4 getTransform () const

Returns the current transformation matrix of the handler.
### Return value

Current transformation matrix of the handler
## void setBasis ( Mat4 basis )

Sets a new basis of the coordinate system for the handler. It can either be the world coordinates (the identity matrix) or coordinates of the parent node if the manipulated node is a child.
### Arguments

- *Mat4* **basis** - The basis of the coordinate system for the handler

## Mat4 getBasis () const

Returns the current basis of the coordinate system for the handler. It can either be the world coordinates (the identity matrix) or coordinates of the parent node if the manipulated node is a child.
### Return value

Current basis of the coordinate system for the handler
## void setColor ( vec4 color )

Sets a new color for the manipulator. The provided value is clamped to a range **[0;1]**.
### Arguments

- *vec4* **color** - The color for the manipulator

## vec4 getColor () const

Returns the current color for the manipulator. The provided value is clamped to a range **[0;1]**.
### Return value

Current color for the manipulator
## void setSize ( int size )

Sets a new handle size of the manipulator, in pixels. Depending on the handle shape, this can be a radius or an altitude.
### Arguments

- *int* **size** - The handle size of the manipulator

## int getSize () const

Returns the current handle size of the manipulator, in pixels. Depending on the handle shape, this can be a radius or an altitude.
### Return value

Current handle size of the manipulator
## void setStep ( float step )

Sets a new step used to align objects, in units.
### Arguments

- *float* **step** - The step used to align objects

## float getStep () const

Returns the current step used to align objects, in units.
### Return value

Current step used to align objects
## void setMask ( int mask )

Sets a new mask that hides axis arrows (along *X*, *Y*, or *Z*) of the handler.
### Arguments

- *int* **mask** - The mask that hides axis arrows of the handler

## int getMask () const

Returns the current mask that hides axis arrows (along *X*, *Y*, or *Z*) of the handler.
### Return value

Current mask that hides axis arrows of the handler
## void setRenderGui ( Gui gui )

Sets a new render GUI for the manipulator.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - The render GUI for the manipulator

## Gui getRenderGui () const

Returns the current render GUI for the manipulator.
### Return value

Current render GUI for the manipulator
## int isFocusAxis () const

Returns the current value indicating if any axis of the manipulator is currently in focus.
### Return value

Current any axis of the manipulator is currently in focus
## int isHoverAxis () const

Returns the current value indicating if any axis of the manipulator is currently hovered.
### Return value

Current any axis of the manipulator is currently hovered
## int getFocusedAxis () const

Returns the current number of the manipulator axis that is currently in focus. The values depend on the manipulator's type:
- [WidgetManipulatorRotator](../../../api/library/gui/class.widgetmanipulatorrotator_usc.md): one of the [AXIS_*](../../../api/library/gui/class.widgetmanipulatorrotator_usc.md#AXIS_UNKNOWN) variables.
- [WidgetManipulatorScaler](../../../api/library/gui/class.widgetmanipulatorscaler_usc.md): one of the [AXIS_*](../../../api/library/gui/class.widgetmanipulatorscaler_usc.md#AXIS_UNKNOWN) variables.
- [WidgetManipulatorTranslator](../../../api/library/gui/class.widgetmanipulatortranslator_usc.md): one of the [AXIS_*](../../../api/library/gui/class.widgetmanipulatortranslator_usc.md#AXIS_UNKNOWN) variables.


### Return value

Current number of the manipulator axis that is currently in focus
---

## static WidgetManipulator ( Gui gui )

WidgetManipulator constructor. Creates a manipulator widget and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - GUI instance.

## static WidgetManipulator ( )

WidgetManipulator constructor. Creates a manipulator widget and adds it to the Engine GUI.
