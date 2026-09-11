# Unigine::InputVRDevice Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The base class for VR devices. It provides access to properties and settings that all VR devices have. For example, you can get a device name, check if it has a battery, or whether it will drift in a specific direction, and so on.


Also, the class functionality allows getting the model of the VR device. For example, you can use it for controller rendering:


1. Get the controller to render by using the corresponding methods of the *[Input](../../../api/library/controls/class.input_usc.md)* class. For example, to get the left controller, call *[getVRControllerLeft()](../../../api/library/controls/class.input_usc.md)*.
2. Check it exists.
3. Get the number of its models via *[getNumModels()](#getNumModels_int).*
4. Load its [meshes](#getModelMesh_int_Mesh) and [textures](#getModelTexture_int_Texture) individually, one by one, or get the [entire mesh](#getCombinedModelMesh_Mesh) at once. Note that there may be a delay during the loading process.
5. Render the loaded meshes with textures.


## InputVRDevice Class

### Members

## int isAvailable () const

Returns the current value indicating if the VR device is available.
### Return value

Current the device is available
## int getNumber () const

Returns the current index of the VR device.
### Return value

Current device index.
## const char * getName () const

Returns the current name of the VR device.
### Return value

Current device name.
## int getDeviceType () const

Returns the current type of the input device (wheel, throttle, etc.).
### Return value

Current input device type.
## int getType () const

Returns the current type of the VR device (HMD, controller, base station, etc.).
### Return value

Current VR device type.
## const char * getDeviceModelName () const

Returns the current name of the model of the VR device.
### Return value

Current model name.
## int isBatteryCharging () const

Returns the current value indicating if the device's battery is currently charging.
### Return value

Current the device's battery is currently charging
## int isBatteryPluggedIn () const

Returns the current value indicating if the device is connected to external power. *OpenVR* runtimes report no separate plugged-in state, so the charging state is used as the signal there.
### Return value

Current the device is connected to external power
## int isBatteryValid () const

Returns the current value indicating if the device actually provides battery status information, so that the battery-related values (charge level, charging state) can be trusted. *OpenXR* runtimes always report true.
### Return value

Current the device provides battery status information
## float getBatteryValue () const

Returns the current battery level.
### Return value

Current battery level, in percent.
## String getModelNumber () const

Returns the current model number for the VR device.
### Return value

Current model number.
## String getSerialNumber () const

Returns the current serial number for the VR device.
### Return value

Current serial number.
## String getManufacturerName () const

Returns the current name of the VR device's vendor.
### Return value

Current vendor name.
## long getHardwareRevision () const

Returns the current hardware revision of the VR device.
### Return value

Current hardware revision.
## long getFirmwareVersion () const

Returns the current firmware revision of the VR device.
### Return value

Current firmware revision.
## int getNumModels () const

Returns the current number of VR device's models.
### Return value

Current number of models.
## Mesh getCombinedModelMesh () const

Returns the current entire mesh of the combined model of the VR device.
> **Notice:** You cannot animate this mesh. However, if you get a mesh of each model individually, it will be automatically animated.


### Return value

Current mesh of the combined model.
## Texture getCombinedModelTexture () const

Returns the current texture of the combined model of the VR device.
### Return value

Current texture of the combined model.
## const char * getCombinedModelName () const

Returns the current name of the combined model of the VR device.
### Return value

Current name of the combined model.
---

## int hasYawDrift ( )

Returns a value indicating if the VR device will drift in a specific direction.
### Return value

true if the device has yaw drift; otherwise, false.
## int hasBattery ( )

Returns a value indicating if the VR device has a battery.
### Return value

true if the device has the battery; otherwise, false.
## Mat4 getWorldTransform ( int type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP )

Retuns the world transformation of the VR device for the specified transformation type.
### Arguments

- *int* **type** - Transformation type.

### Return value

World transformation matrix.
## mat4 getTransform ( int type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP )

Returns the local transformation of the VR device for the specified transformation type.
### Arguments

- *int* **type** - Transformation type.

### Return value

Local transformation matrix.
## vec3 getLinearVelocity ( int type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP )

Returns the linear velocity of the VR device for the specified transformation type.
### Arguments

- *int* **type** - Transformation type.

### Return value

Linear velocity.
## vec3 getAngularVelocity ( int type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP )

Returns the angular velocity of the VR device for the specified transformation type.
### Arguments

- *int* **type** - Transformation type.

### Return value

Angular velocity.
## vec3 getAngularAcceleration ( int type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP )

Returns the angular acceleration of the VR device for the specified transformation type.
### Arguments

- *int* **type** - Transformation type.

### Return value

Angular acceleration.
## int isTransformValid ( int type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP )

Returns a value indicating if transformation of the VR device for the specified transformation type is valid.
### Arguments

- *int* **type** - Transformation type.

### Return value

true if transformation is valid; otherwise, false.
## int isVelocityValid ( int type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP )

Returns a value indicating if the velocity of the VR device for the specified transformation type is valid.
### Arguments

- *int* **type** - Transformation type.

### Return value

true if velocity is valid; otherwise, false.
## int isTransformTypeSupported ( int type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP )

Returns a value indicating if the VR device supports the specified transformation type.
### Arguments

- *int* **type** - Transformation type.

### Return value

true if transformation type is supported; otherwise, false.
## mat4 getModelTransform ( int num )

Returns the local transformation of the given model.
### Arguments

- *int* **num** - Model index.

### Return value

Local transformation matrix of the model.
## Mat4 getModelWorldTransform ( int num )

Returns the world transformation of the given model.
### Arguments

- *int* **num** - Model index.

### Return value

World transformation matrix of the model.
## Mesh getModelMesh ( int num )

Returns the mesh of the given model.
### Arguments

- *int* **num** - Model index.

### Return value

Model mesh.
## Texture getModelTexture ( int num )

Returns the texture of the given model.
### Arguments

- *int* **num** - Model index.

### Return value

Model texture.
## string getModelName ( int num )

Returns the name of the given model.
### Arguments

- *int* **num** - Model index.

### Return value

Model name.
