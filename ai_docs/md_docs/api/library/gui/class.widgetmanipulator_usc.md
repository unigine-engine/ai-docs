# Unigine::WidgetManipulator Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This base class creates a draggable 3D manipulator.


### See Also


- Usage example: [Using Manipulators to Transform Objects](../../../code/usage/manipulator_component/index.md)
- C++ sample


## WidgetManipulator Class

### Members

---

## static WidgetManipulator ( Gui gui )

WidgetManipulator constructor. Creates a manipulator widget and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - GUI instance.

## static WidgetManipulator ( )

WidgetManipulator constructor. Creates a manipulator widget and adds it to the Engine GUI.
## void setBasis ( Mat4 basis )

Sets a basis of the coordinate system for the handler. It can either be the world coordinates (the identity matrix) or coordinates of the parent node if the manipulated node is a child.
### Arguments

- *Mat4* **basis** - Matrix, with columns specifying basis vectors.

## Mat4 getBasis ( )

Returns the current basis of the coordinate system for the handler. It can either be the world coordinates (the identity matrix) or coordinates of the parent node if the manipulated node is a child.
### Return value

Matrix, with columns specifying basis vectors.
## void setColor ( vec4 color )

Sets the color for a manipulator.
### Arguments

- *vec4* **color** - Manipulator color. The provided value is clamped to a range **[0;1]**.

## vec4 getColor ( )

Returns the current color for a manipulator.
### Return value

Manipulator color.
## void setMask ( int mask )

Hides axis arrows (along *X*, *Y* or *Z*) of the handler.
### Arguments

- *int* **mask** - 3-bit mask for axes.

## int getMask ( )

Returns a mask that hides axis arrows (along *X*, *Y* or *Z*) of the handler.
### Return value

3-bit mask for axes.
## void setModelview ( Mat4 modelview )

Sets a model-view matrix for the handler.
### Arguments

- *Mat4* **modelview** - Model-view matrix.

## Mat4 getModelview ( )

Returns the current projection matrix of the handler.
### Return value

Model-view matrix.
## void setProjection ( mat4 projection )

Sets a projection matrix for the handler.
### Arguments

- *mat4* **projection** - Projection matrix.

## mat4 getProjection ( )

Returns the current model-view matrix of the handler.
### Return value

Projection matrix.
## void setRenderGui ( Gui gui )

Sets the render GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md) smart pointer.

## Gui getRenderGui ( )

Returns the current render GUI.
### Return value

[GUI](../../../api/library/gui/class.gui_usc.md) smart pointer.
## void setSize ( int size )

Sets a handle size of the manipulator. Depending on the handle shape, this can be a radius or an altitude.
### Arguments

- *int* **size** - Size in pixels.

## int getSize ( )

Returns the current handle size of the manipulator. Depending on the handle shape, this can be a radius or an altitude.
### Return value

Size in pixels.
## void setStep ( float step )

Sets a step, which is used to align objects.
### Arguments

- *float* **step** - Step in units.

## float getStep ( )

Returns a step, which is used to align objects.
### Return value

Step in units.
## void setTransform ( Mat4 transform )

Sets a transformation matrix for the handler.
### Arguments

- *Mat4* **transform** - Transformation matrix.

## Mat4 getTransform ( )

Returns the current transformation matrix of the handler.
### Return value

Transformation matrix.
## int getFocusedAxis ( )

Returns the number of the manipulator axis, that is currently in focus.
### Return value

Number of the manipulator axis, that is currently in focus. The values depend on the manipulator's type:
- [WidgetManipulatorRotator](../../../api/library/gui/class.widgetmanipulatorrotator_usc.md): one of the [AXIS_*](../../../api/library/gui/class.widgetmanipulatorrotator_usc.md#AXIS_UNKNOWN) variables.
- [WidgetManipulatorScaler](../../../api/library/gui/class.widgetmanipulatorscaler_usc.md): one of the [AXIS_*](../../../api/library/gui/class.widgetmanipulatorscaler_usc.md#AXIS_UNKNOWN) variables.
- [WidgetManipulatorTranslator](../../../api/library/gui/class.widgetmanipulatortranslator_usc.md): one of the [AXIS_*](../../../api/library/gui/class.widgetmanipulatortranslator_usc.md#AXIS_UNKNOWN) variables.


## int isFocusAxis ( )

Returns a value indicating if any axis of the manipulator is currently in focus.
### Return value

**1** if any axis of the manipulator is currently in focus; otherwise, **0**.
## int isHoverAxis ( )

Returns a value indicating if any axis of the manipulator is currently hovered.
### Return value

**1** if any axis of the manipulator is currently hovered; otherwise, **0**.
