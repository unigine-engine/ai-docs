# Unigine::WidgetManipulator Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This base class creates a draggable 3D manipulator.


### See Also


- Usage example: [Using Manipulators to Transform Objects](../../../code/usage/manipulator_component/index_cpp.md)
- C++ sample


## WidgetManipulator Class

### Members

---

## static WidgetManipulatorPtr create ( const Ptr < Gui > & gui )

WidgetManipulator constructor. Creates a manipulator widget and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - Pointer to GUI.

## static WidgetManipulatorPtr create ( )

WidgetManipulator constructor. Creates a manipulator widget and adds it to the Engine GUI.
## void setBasis ( const Math:: Mat4 & basis )

Sets a basis of the coordinate system for the handler. It can either be the world coordinates (the identity matrix) or coordinates of the parent node if the manipulated node is a child.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **basis** - Matrix, with columns specifying basis vectors.

## Math:: Mat4 getBasis ( ) const

Returns the current basis of the coordinate system for the handler. It can either be the world coordinates (the identity matrix) or coordinates of the parent node if the manipulated node is a child.
### Return value

Matrix, with columns specifying basis vectors.
## void setColor ( const Math:: vec4 & color )

Sets the color for a manipulator.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Manipulator color. The provided value is clamped to a range **[0;1]**.

## Math:: vec4 getColor ( ) const

Returns the current color for a manipulator.
### Return value

Manipulator color.
## void setMask ( int mask )

Hides axis arrows (along *X*, *Y* or *Z*) of the handler.
### Arguments

- *int* **mask** - 3-bit mask for axes.

## int getMask ( ) const

Returns a mask that hides axis arrows (along *X*, *Y* or *Z*) of the handler.
### Return value

3-bit mask for axes.
## void setModelview ( const Math:: Mat4 & modelview )

Sets a model-view matrix for the handler.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **modelview** - Model-view matrix.

## Math:: Mat4 getModelview ( ) const

Returns the current projection matrix of the handler.
### Return value

Model-view matrix.
## void setProjection ( const Math:: mat4 & projection )

Sets a projection matrix for the handler.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **projection** - Projection matrix.

## Math:: mat4 getProjection ( ) const

Returns the current model-view matrix of the handler.
### Return value

Projection matrix.
## void setRenderGui ( const Ptr < Gui > & gui )

Sets the render GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md) smart pointer.

## Ptr < Gui > getRenderGui ( ) const

Returns the current render GUI.
### Return value

[GUI](../../../api/library/gui/class.gui_cpp.md) smart pointer.
## void setSize ( int size )

Sets a handle size of the manipulator. Depending on the handle shape, this can be a radius or an altitude.
### Arguments

- *int* **size** - Size in pixels.

## int getSize ( ) const

Returns the current handle size of the manipulator. Depending on the handle shape, this can be a radius or an altitude.
### Return value

Size in pixels.
## void setStep ( float step )

Sets a step, which is used to align objects.
### Arguments

- *float* **step** - Step in units.

## float getStep ( ) const

Returns a step, which is used to align objects.
### Return value

Step in units.
## void setTransform ( const Math:: Mat4 & transform )

Sets a transformation matrix for the handler.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## Math:: Mat4 getTransform ( ) const

Returns the current transformation matrix of the handler.
### Return value

Transformation matrix.
## int getFocusedAxis ( ) const

Returns the number of the manipulator axis, that is currently in focus.
### Return value

Number of the manipulator axis, that is currently in focus. The values depend on the manipulator's type:
- [WidgetManipulatorRotator](../../../api/library/gui/class.widgetmanipulatorrotator_cpp.md): one of the [AXIS_*](../../../api/library/gui/class.widgetmanipulatorrotator_cpp.md#AXIS_UNKNOWN) variables.
- [WidgetManipulatorScaler](../../../api/library/gui/class.widgetmanipulatorscaler_cpp.md): one of the [AXIS_*](../../../api/library/gui/class.widgetmanipulatorscaler_cpp.md#AXIS_UNKNOWN) variables.
- [WidgetManipulatorTranslator](../../../api/library/gui/class.widgetmanipulatortranslator_cpp.md): one of the [AXIS_*](../../../api/library/gui/class.widgetmanipulatortranslator_cpp.md#AXIS_UNKNOWN) variables.


## bool isFocusAxis ( ) const

Returns a value indicating if any axis of the manipulator is currently in focus.
### Return value

true if any axis of the manipulator is currently in focus; otherwise, false.
## bool isHoverAxis ( ) const

Returns a value indicating if any axis of the manipulator is currently hovered.
### Return value

true if any axis of the manipulator is currently hovered; otherwise, false.
