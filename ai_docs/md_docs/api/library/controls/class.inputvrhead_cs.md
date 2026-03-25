# Unigine::InputVRHead Class (CS)

**Inherits from:** InputVRDevice


The class handles head-mounted display (HMD) input.


## InputVRHead Class

### Enums

## MODEL_TYPE

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | Unknown HMD. |
| **OCULUS_BEGIN** = 1 | The first element to be used for iteration through the model types of the Oculus Rift HMD. |
| **OCULUS_DK2** = 1 | Oculus Rift DK2 |
| **OCULUS_CB** = 2 | Oculus Rift CB |
| **OCULUS_OTHER** = 3 | Other model of the Oculus Rift HMD. |
| **OCULUS_E3_2015** = 4 | Oculus Rift E3 2015 |
| **OCULUS_ES06** = 5 | Oculus Rift ES06 |
| **OCULUS_ES09** = 6 | Oculus Rift ES09 |
| **OCULUS_ES11** = 7 | Oculus Rift ES11 |
| **OCULUS_RIFT** = 8 | Oculus Rift CV1 |
| **OCULUS_RIFT_S** = 9 | Oculus Rift Rift S |
| **OCULUS_END** = 9 | The last element to be used for iteration through the model types of the Oculus Rift HMD. |
| **VARJO_BEGIN** = 10 | The first element to be used for iteration through the model types of the Varjo HMD. |
| **VARJO_VR_1** = 10 | Varjo VR-1 |
| **VARJO_XR_1** = 11 | Varjo XR-1 |
| **VARJO_VR_2** = 12 | Varjo VR-2 |
| **VARJO_VR_2_PRO** = 13 | Varjo VR-2 Pro |
| **VARJO_VR_3** = 14 | Varjo VR-3 |
| **VARJO_XR_3** = 15 | Varjo XR-3 |
| **VARJO_AERO** = 16 | Varjo AERO |
| **VARJO_END** = 16 | The last element to be used for iteration through the model types of the Varjo HMD. |
| **OPENVR_BEGIN** = 17 | The first element to be used for iteration through the model types of the HMD. |
| **OPENVR_HTC_VIVE** = 17 | HTC Vive |
| **OPENVR_HTC_VIVE_PRO** = 18 | HTC Vive Pro MV |
| **OPENVR_HTC_FOCUS** = 19 | HTC Vive Focus |
| **OPENVR_VALVE_INDEX** = 20 | Valve Index |
| **OPENVR_END** = 20 | The last element to be used for iteration through the model types of the HMD. |
| **NUM_MODEL_TYPES** = 21 | Total number of HMD model types. |

### Properties

## 🔒︎ InputVRHead.MODEL_TYPE ModelType

The HMD model type.
## bool TrackingPositionEnabled

The true if position tracking is enabled; otherwise, false.
## bool TrackingRotationEnabled

The true if rotation tracking is enabled; otherwise, false.
## float RefreshRate

The display refresh rate, in Hz.
## 🔒︎ float[] SupportedRefreshRates

The vector of supported display refresh rates, in Hz.
### Members

---

## bool HasButtons ( )

Returns a value indicating if the HMD has buttons.
### Return value

true if there are buttons; otherwise, false.
## float[] GetSupportedRefreshRates ( )

Returns an array of supported display refresh rates, in Hz, with at least one supported refresh rate.
### Return value

The vector of supported display refresh rates, in Hz.
## void SetRefreshRate ( float rate )

Sets the display refresh rate, if supported.
### Arguments

- *float* **rate** - The display refresh rate, in Hz.

## float GetRefreshRate ( )

Returns the current display refresh rate, in Hz.
### Return value

The display refresh rate, in Hz.
## bool IsButtonPressed ( Input.VR_BUTTON button )

Returns a value indicating if the specified button is pressed. Check this value to perform continuous actions.
### Arguments

- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **button** - Button.

### Return value

true if the button is pressed; otherwise, false.
## bool IsButtonDown ( Input.VR_BUTTON button )

Returns a value indicating if the specified button was pressed during the current frame.
### Arguments

- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **button** - Button.

### Return value

true if the button was pressed; otherwise, false.
## bool IsButtonUp ( Input.VR_BUTTON button )

Returns a value indicating if the specified button was released during the current frame.
### Arguments

- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **button** - Button.

### Return value

true if the button was released; otherwise, false.
## InputEventVRButton GetButtonEvent ( Input.VR_BUTTON button )

Returns the currently processed HMD button input event.
### Arguments

- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **button** - Button.

### Return value

HMD button input event, or null if there are no events for the specified button in the current frame.
## int GetButtonEvents ( Input.VR_BUTTON button , InputEventVRButton [] OUT_events )

Returns the number of input events for the specified HMD button and puts the events to the specified output buffer.
### Arguments

- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **button** - Button.
- *[InputEventVRButton](../../../api/library/controls/class.inputeventvrbutton_cs.md)[]* **OUT_events** - Buffer with HMD button input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of input events for the specified HMD button.
