# Unigine::InputVRDevice Class (CPP)

**Header:** #include <UnigineInput.h>


The base class for VR devices. It provides access to properties and settings that all VR devices have. For example, you can get a device name, check if it has a battery, or whether it will drift in a specific direction, and so on.


Also, the class functionality allows getting the model of the VR device. For example, you can use it for controller rendering:


1. Get the controller to render by using the corresponding methods of the *[Input](../../../api/library/controls/class.input_cpp.md)* class. For example, to get the left controller, call *[getVRControllerLeft()](../../../api/library/controls/class.input_cpp.md)*.
2. Check it exists.
3. Get the number of its models via *[getNumModels()](#getNumModels_int).*
4. Load its [meshes](#getModelMesh_int_Mesh) and [textures](#getModelTexture_int_Texture) individually, one by one, or get the [entire mesh](#getCombinedModelMesh_Mesh) at once. Note that there may be a delay during the loading process.
5. Render the loaded meshes with textures.


## InputVRDevice Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **INPUT_VR_UNKNOWN** = 0 | Unknown VR device. |
| **INPUT_VR_DEVICE** = 1 | VR device. |
| **INPUT_VR_HEAD** = 2 | Head-mounted display. |
| **INPUT_VR_CONTROLLER** = 3 | Controller. |
| **INPUT_VR_TRACKER** = 4 | Tracker. |
| **INPUT_VR_BASE_STATION** = 5 | Base station. |
| **NUM_TYPES** = 6 | Total number of types of the VR devices. |

## TRANSFORM_TYPE

| Name | Description |
|---|---|
| **TRANSFORM_TYPE_AIM** = 0 | (OpenXR only) A pose that allows applications to point in the world using the input source, according to the platform�s conventions for aiming with that kind of source. The aim pose is defined as follows: - For tracked hands: The ray that follows platform conventions for how the user aims at objects in the world with their entire hand, with +Y up, +X to the right, and -Z forward. The ray chosen will be runtime-dependent, often a ray emerging from the hand at a target pointed by moving the forearm. - For handheld motion controllers: The ray that follows platform conventions for how the user targets objects in the world with the motion controller, with +Y up, +X to the right, and -Z forward. This is usually for applications that are rendering a model matching the physical controller, as an application rendering a virtual object in the user�s hand likely prefers to point based on the geometry of that virtual object. The ray chosen will be runtime-dependent, although this will often emerge from the frontmost tip of a motion controller. |
| **TRANSFORM_TYPE_GRIP** = 1 | A pose that allows applications to reliably render a virtual object held in the user�s hand, whether it is tracked directly or by a motion controller. The grip pose is defined as follows: - The grip position: - For tracked hands: The user�s palm centroid when closing the fist, at the surface of the palm. - For handheld motion controllers: A fixed position within the controller that generally lines up with the palm centroid when held by a hand in a neutral position. This position should be adjusted left or right to center the position within the controller�s grip. - The grip orientation�s +X axis: When you completely open your hand to form a flat 5-finger pose, the ray that is normal to the user�s palm (away from the palm in the left hand, into the palm in the right hand). - The grip orientation�s -Z axis: When you close your hand partially (as if holding the controller), the ray that goes through the center of the tube formed by your non-thumb fingers, in the direction of little finger to thumb. - The grip orientation�s +Y axis: orthogonal to +Z and +X using the right-hand rule. |
| **TRANSFORM_TYPE_MESH** = 2 | A pose ([grip_surface](https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#semantic-paths-standard-pose-identifiers)) that allows applications to reliably anchor visual content relative to the user�s physical hand, whether the user�s hand is tracked directly or its position and orientation is inferred by a physical controller. The grip_surface pose is defined as follows: - The grip_surface position: The user�s physical palm centroid, at the surface of the palm. For the avoidance of doubt, the palm does not include fingers. - The grip_surface orientation�s +X axis: When a user is holding the controller and straightens their index fingers pointing forward, the ray that is normal (perpendicular) to the user�s palm (away from the palm in the left hand, into the palm in the right hand). - The grip_surface orientation�s -Z axis: When a user is holding the controller and straightens their index finger, the ray that is parallel to their finger�s pointing direction. - The grip_surface orientation�s +Y axis: orthogonal to +Z and +X using the right-hand rule. |
| **TRANSFORM_TYPE_PINCH** = 3 | [Pinch pose](https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#_pinch_pose) designed for interacting with a small object within arm�s reach using a finger and thumb with a "pinch" gesture. For example, turning a key to open a lock or moving the knob on a slider control are interactions suited to the "pinch" pose. |
| **TRANSFORM_TYPE_POKE** = 4 | [Poke pose](https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#_poke_pose) designed for interactions using a fingertip to touch and push a small object. For example, pressing a push button with a fingertip, swiping to scroll a browser view, or typing on a virtual keyboard are interactions suited to the "poke" pose. |
| **TRANSFORM_TYPE_GAZE** = 5 | [Gaze pose](https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#_eye_gaze_input) represents the user's gaze direction and is designed for interactions based on real time user's eye tracking. The gaze pose is typically used for interactions such as pointing, object selection, UI targeting, and attention-based interaction. It provides a natural method for determining user intent based on what they are currently looking at in the scene. The gaze pose is defined as follows: - The gaze position: The center point between the user's eyes (when eye tracking is active), or an estimated point between the eyes based on head tracking. - The gaze orientation's -Z axis: The direction in which the user is looking. When eye tracking is available, this reflects the user's actual line of sight; otherwise, it aligns with the forward direction of the head. - The gaze orientation's +Y axis: Generally upward from the user's face. - The gaze orientation's +X axis: To the right from the user's perspective, forming a right-handed coordinate system. > **Notice:** This feature is only available for OpenXR devices. |
| **NUM_TRANSFORM_TYPES** = 6 | Total number of transformation types. |

### Members

## bool isAvailable () const

Returns the current value indicating if the VR device is available.
### Return value

**true** if the device is available; otherwise **false**.
## int getNumber () const

Returns the current index of the VR device.
### Return value

Current device index.
## const char * getName () const

Returns the current name of the VR device.
### Return value

Current device name.
## Input::DEVICE getDeviceType () const

Returns the current type of the input device (wheel, throttle, etc.).
### Return value

Current input device type.
## InputVRDevice::TYPE getType () const

Returns the current type of the VR device (HMD, controller, base station, etc.).
### Return value

Current VR device type.
## const char * getDeviceModelName () const

Returns the current name of the model of the VR device.
### Return value

Current model name.
## bool isBatteryCharging () const

Returns the current value indicating if the device's battery is currently charging.
### Return value

**true** if the device's battery is currently charging; otherwise **false**.
## bool isBatteryPluggedIn () const

Returns the current value indicating if the device is connected to external power. *OpenVR* runtimes report no separate plugged-in state, so the charging state is used as the signal there.
### Return value

**true** if the device is connected to external power; otherwise **false**.
## bool isBatteryValid () const

Returns the current value indicating if the device actually provides battery status information, so that the battery-related values (charge level, charging state) can be trusted. *OpenXR* runtimes always report true.
### Return value

**true** if the device provides battery status information; otherwise **false**.
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
## unsigned long long getHardwareRevision () const

Returns the current hardware revision of the VR device.
### Return value

Current hardware revision.
## unsigned long long getFirmwareVersion () const

Returns the current firmware revision of the VR device.
### Return value

Current firmware revision.
## int getNumModels () const

Returns the current number of VR device's models.
### Return value

Current number of models.
## Ptr < Mesh > getCombinedModelMesh () const

Returns the current entire mesh of the combined model of the VR device.
> **Notice:** You cannot animate this mesh. However, if you get a mesh of each model individually, it will be automatically animated.


### Return value

Current mesh of the combined model.
## Ptr < Texture > getCombinedModelTexture () const

Returns the current texture of the combined model of the VR device.
### Return value

Current texture of the combined model.
## const char * getCombinedModelName () const

Returns the current name of the combined model of the VR device.
### Return value

Current name of the combined model.
---

## bool hasYawDrift ( ) const

Returns a value indicating if the VR device will drift in a specific direction.
### Return value

true if the device has yaw drift; otherwise, false.
## bool hasBattery ( ) const

Returns a value indicating if the VR device has a battery.
### Return value

true if the device has the battery; otherwise, false.
## Math:: Mat4 getWorldTransform ( InputVRDevice::TRANSFORM_TYPE type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP ) const

Retuns the world transformation of the VR device for the specified transformation type.
### Arguments

- *[InputVRDevice::TRANSFORM_TYPE](../../../api/library/controls/class.inputvrdevice_cpp.md#TRANSFORM_TYPE)* **type** - Transformation type.

### Return value

World transformation matrix.
## Math:: mat4 getTransform ( InputVRDevice::TRANSFORM_TYPE type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP ) const

Returns the local transformation of the VR device for the specified transformation type.
### Arguments

- *[InputVRDevice::TRANSFORM_TYPE](../../../api/library/controls/class.inputvrdevice_cpp.md#TRANSFORM_TYPE)* **type** - Transformation type.

### Return value

Local transformation matrix.
## Math:: vec3 getLinearVelocity ( InputVRDevice::TRANSFORM_TYPE type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP ) const

Returns the linear velocity of the VR device for the specified transformation type.
### Arguments

- *[InputVRDevice::TRANSFORM_TYPE](../../../api/library/controls/class.inputvrdevice_cpp.md#TRANSFORM_TYPE)* **type** - Transformation type.

### Return value

Linear velocity.
## Math:: vec3 getAngularVelocity ( InputVRDevice::TRANSFORM_TYPE type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP ) const

Returns the angular velocity of the VR device for the specified transformation type.
### Arguments

- *[InputVRDevice::TRANSFORM_TYPE](../../../api/library/controls/class.inputvrdevice_cpp.md#TRANSFORM_TYPE)* **type** - Transformation type.

### Return value

Angular velocity.
## Math:: vec3 getAngularAcceleration ( InputVRDevice::TRANSFORM_TYPE type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP ) const

Returns the angular acceleration of the VR device for the specified transformation type.
### Arguments

- *[InputVRDevice::TRANSFORM_TYPE](../../../api/library/controls/class.inputvrdevice_cpp.md#TRANSFORM_TYPE)* **type** - Transformation type.

### Return value

Angular acceleration.
## bool isTransformValid ( InputVRDevice::TRANSFORM_TYPE type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP ) const

Returns a value indicating if transformation of the VR device for the specified transformation type is valid.
### Arguments

- *[InputVRDevice::TRANSFORM_TYPE](../../../api/library/controls/class.inputvrdevice_cpp.md#TRANSFORM_TYPE)* **type** - Transformation type.

### Return value

true if transformation is valid; otherwise, false.
## bool isVelocityValid ( InputVRDevice::TRANSFORM_TYPE type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP ) const

Returns a value indicating if the velocity of the VR device for the specified transformation type is valid.
### Arguments

- *[InputVRDevice::TRANSFORM_TYPE](../../../api/library/controls/class.inputvrdevice_cpp.md#TRANSFORM_TYPE)* **type** - Transformation type.

### Return value

true if velocity is valid; otherwise, false.
## bool isTransformTypeSupported ( InputVRDevice::TRANSFORM_TYPE type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP ) const

Returns a value indicating if the VR device supports the specified transformation type.
### Arguments

- *[InputVRDevice::TRANSFORM_TYPE](../../../api/library/controls/class.inputvrdevice_cpp.md#TRANSFORM_TYPE)* **type** - Transformation type.

### Return value

true if transformation type is supported; otherwise, false.
## Math:: mat4 getModelTransform ( int num ) const

Returns the local transformation of the given model.
### Arguments

- *int* **num** - Model index.

### Return value

Local transformation matrix of the model.
## Math:: Mat4 getModelWorldTransform ( int num ) const

Returns the world transformation of the given model.
### Arguments

- *int* **num** - Model index.

### Return value

World transformation matrix of the model.
## Ptr < Mesh > getModelMesh ( int num )

Returns the mesh of the given model.
### Arguments

- *int* **num** - Model index.

### Return value

Model mesh.
## Ptr < Texture > getModelTexture ( int num )

Returns the texture of the given model.
### Arguments

- *int* **num** - Model index.

### Return value

Model texture.
## const char * getModelName ( int num )

Returns the name of the given model.
### Arguments

- *int* **num** - Model index.

### Return value

Model name.
