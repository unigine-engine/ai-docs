# Unigine::InputVRHead Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputVRDevice


The class handles head-mounted display (HMD) input.


## InputVRHead Class

### Enums

## MODEL_TYPE

| Name | Description |
|---|---|
| **MODEL_TYPE_UNKNOWN** = 0 | Unknown HMD. |
| **MODEL_TYPE_OCULUS_BEGIN** = 1 | The first element to be used for iteration through the model types of the Oculus Rift HMD. |
| **MODEL_TYPE_OCULUS_DK2** = 1 | Oculus Rift DK2 |
| **MODEL_TYPE_OCULUS_CB** = 2 | Oculus Rift CB |
| **MODEL_TYPE_OCULUS_OTHER** = 3 | Other model of the Oculus Rift HMD. |
| **MODEL_TYPE_OCULUS_E3_2015** = 4 | Oculus Rift E3 2015 |
| **MODEL_TYPE_OCULUS_ES06** = 5 | Oculus Rift ES06 |
| **MODEL_TYPE_OCULUS_ES09** = 6 | Oculus Rift ES09 |
| **MODEL_TYPE_OCULUS_ES11** = 7 | Oculus Rift ES11 |
| **MODEL_TYPE_OCULUS_RIFT** = 8 | Oculus Rift CV1 |
| **MODEL_TYPE_OCULUS_RIFT_S** = 9 | Oculus Rift Rift S |
| **MODEL_TYPE_OCULUS_END** = 9 | The last element to be used for iteration through the model types of the Oculus Rift HMD. |
| **MODEL_TYPE_VARJO_BEGIN** = 10 | The first element to be used for iteration through the model types of the Varjo HMD. |
| **MODEL_TYPE_VARJO_VR_1** = 10 | Varjo VR-1 |
| **MODEL_TYPE_VARJO_XR_1** = 11 | Varjo XR-1 |
| **MODEL_TYPE_VARJO_VR_2** = 12 | Varjo VR-2 |
| **MODEL_TYPE_VARJO_VR_2_PRO** = 13 | Varjo VR-2 Pro |
| **MODEL_TYPE_VARJO_VR_3** = 14 | Varjo VR-3 |
| **MODEL_TYPE_VARJO_XR_3** = 15 | Varjo XR-3 |
| **MODEL_TYPE_VARJO_AERO** = 16 | Varjo AERO |
| **MODEL_TYPE_VARJO_END** = 16 | The last element to be used for iteration through the model types of the Varjo HMD. |
| **MODEL_TYPE_OPENVR_BEGIN** = 17 | The first element to be used for iteration through the model types of the HMD. |
| **MODEL_TYPE_OPENVR_HTC_VIVE** = 17 | HTC Vive |
| **MODEL_TYPE_OPENVR_HTC_VIVE_PRO** = 18 | HTC Vive Pro MV |
| **MODEL_TYPE_OPENVR_HTC_FOCUS** = 19 | HTC Vive Focus |
| **MODEL_TYPE_OPENVR_VALVE_INDEX** = 20 | Valve Index |
| **MODEL_TYPE_OPENVR_END** = 20 | The last element to be used for iteration through the model types of the HMD. |
| **NUM_MODEL_TYPES** = 21 | Total number of HMD model types. |

### Members

---

## InputVRHead::MODEL_TYPE getModelType ( ) const

Returns the model type of the HMD.
### Return value

HMD model type.
## bool hasButtons ( ) const

Returns a value indicating if the HMD has buttons.
### Return value

true if there are buttons; otherwise, false.
## Vector <float> getSupportedRefreshRates ( ) const

Returns an array of supported display refresh rates, in Hz, with at least one supported refresh rate.
### Return value

The vector of supported display refresh rates, in Hz.
## void setRefreshRate ( float rate )

Sets the display refresh rate, if supported.
### Arguments

- *float* **rate** - The display refresh rate, in Hz.

## float getRefreshRate ( ) const

Returns the current display refresh rate, in Hz.
### Return value

The display refresh rate, in Hz.
## void setTrackingPositionEnabled ( bool enabled )

Sets the value indicating if head position tracking is enabled.
### Arguments

- *bool* **enabled** - true to enable position tracking; false to disable it.

## bool isTrackingPositionEnabled ( ) const

Returns a value indicating if head position tracking is enabled.
### Return value

true if position tracking is enabled; otherwise, false.
## void setTrackingRotationEnabled ( bool enabled )

Sets the value indicating if head rotation tracking is enabled.
### Arguments

- *bool* **enabled** - true to enable rotation tracking; false to disable it.

## bool isTrackingRotationEnabled ( ) const

Returns a value indicating if head rotation tracking is enabled.
### Return value

true if rotation tracking is enabled; otherwise, false.
## bool isButtonPressed ( Input::VR_BUTTON button ) const

Returns a value indicating if the specified button is pressed. Check this value to perform continuous actions.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **button** - Button.

### Return value

true if the button is pressed; otherwise, false.
## bool isButtonDown ( Input::VR_BUTTON button ) const

Returns a value indicating if the specified button was pressed during the current frame.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **button** - Button.

### Return value

true if the button was pressed; otherwise, false.
## bool isButtonUp ( Input::VR_BUTTON button ) const

Returns a value indicating if the specified button was released during the current frame.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **button** - Button.

### Return value

true if the button was released; otherwise, false.
## Ptr < InputEventVRButton > getButtonEvent ( Input::VR_BUTTON button ) const

Returns the currently processed HMD button input event.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **button** - Button.

### Return value

HMD button input event, or nullptr if there are no events for the specified button in the current frame.
## int getButtonEvents ( Input::VR_BUTTON button , Vector < Ptr < InputEventVRButton >> & OUT_events )

Returns the number of input events for the specified HMD button and puts the events to the specified output buffer.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **button** - Button.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[InputEventVRButton](../../../api/library/controls/class.inputeventvrbutton_cpp.md)>> &* **OUT_events** - Buffer with HMD button input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of input events for the specified HMD button.
