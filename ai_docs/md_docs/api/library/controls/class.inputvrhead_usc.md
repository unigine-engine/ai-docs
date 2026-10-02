# Unigine::InputVRHead Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputVRDevice


The class handles head-mounted display (HMD) input.


## InputVRHead Class

### Members

---

## int getModelType ( )

Returns the head-mounted display model recognised by the engine � one of the [MODEL_TYPE](#MODEL_TYPE) values. [MODEL_TYPE_UNKNOWN](#MODEL_TYPE_UNKNOWN) is returned for a device the engine has no profile for.
### Return value

HMD model type.
## int hasButtons ( )

Returns a value indicating if the headset reports buttons the engine can read. Headsets without any controls of their own return false.
### Return value

true if there are buttons; otherwise, false.
## Vector<float> getSupportedRefreshRates ( )

Returns an array of supported display refresh rates, in Hz, with at least one supported refresh rate.
### Return value

The vector of supported display refresh rates, in Hz.
## void setRefreshRate ( float rate )

Sets the display refresh rate, if supported.
### Arguments

- *float* **rate** - The display refresh rate, in Hz.

## float getRefreshRate ( )

Returns the display refresh rate the HMD currently runs at, in Hz. The rates the device accepts are listed by *[getSupportedRefreshRates()()](../../...md#getSupportedRefreshRates_VECfloat)*, and *[setRefreshRate()()](../../...md#setRefreshRate_float_void)* switches between them.
### Return value

The display refresh rate, in Hz.
## void setTrackingPositionEnabled ( int enabled )

Sets the value indicating if head position tracking is enabled.
### Arguments

- *int* **enabled** - true to enable position tracking; false to disable it.

## int isTrackingPositionEnabled ( )

Returns a value indicating if positional tracking of the head is enabled � that is, whether the head transformation follows the physical movement of the player.
### Return value

true if position tracking is enabled; otherwise, false.
## void setTrackingRotationEnabled ( int enabled )

Sets the value indicating if head rotation tracking is enabled.
### Arguments

- *int* **enabled** - true to enable rotation tracking; false to disable it.

## int isTrackingRotationEnabled ( )

Returns a value indicating if rotational tracking of the head is enabled � that is, whether the head transformation follows the physical rotation of the player's head.
### Return value

true if rotation tracking is enabled; otherwise, false.
## int isButtonPressed ( int button )

Returns a value indicating if the specified button is pressed. Check this value to perform continuous actions.
### Arguments

- *int* **button** - Button.

### Return value

true if the button is pressed; otherwise, false.
## int isButtonDown ( int button )

Returns a value indicating if the specified button was pressed during the current frame.
### Arguments

- *int* **button** - Button.

### Return value

true if the button was pressed; otherwise, false.
## int isButtonUp ( int button )

Returns a value indicating if the specified button was released during the current frame.
### Arguments

- *int* **button** - Button.

### Return value

true if the button was released; otherwise, false.
## InputEventVRButton getButtonEvent ( int button )

Returns the HMD button event currently being processed for the given button. One event is taken from the queue per frame.
### Arguments

- *int* **button** - Button.

### Return value
