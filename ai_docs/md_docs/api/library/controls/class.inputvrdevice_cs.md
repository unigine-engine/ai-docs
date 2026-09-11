# Unigine::InputVRDevice Class (CS)


The base class for VR devices. It provides access to properties and settings that all VR devices have. For example, you can get a device name, check if it has a battery, or whether it will drift in a specific direction, and so on.


Also, the class functionality allows getting the model of the VR device. For example, you can use it for controller rendering:


1. Get the controller to render by using the corresponding methods of the *[Input](../../../api/library/controls/class.input_cs.md)* class. For example, to get the left controller, call *[getVRControllerLeft()](../../../api/library/controls/class.input_cs.md)*.
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
| **AIM** = 0 | (OpenXR only) A pose that allows applications to point in the world using the input source, according to the platform�s conventions for aiming with that kind of source. The aim pose is defined as follows: - For tracked hands: The ray that follows platform conventions for how the user aims at objects in the world with their entire hand, with +Y up, +X to the right, and -Z forward. The ray chosen will be runtime-dependent, often a ray emerging from the hand at a target pointed by moving the forearm. - For handheld motion controllers: The ray that follows platform conventions for how the user targets objects in the world with the motion controller, with +Y up, +X to the right, and -Z forward. This is usually for applications that are rendering a model matching the physical controller, as an application rendering a virtual object in the user�s hand likely prefers to point based on the geometry of that virtual object. The ray chosen will be runtime-dependent, although this will often emerge from the frontmost tip of a motion controller. |
| **GRIP** = 1 | A pose that allows applications to reliably render a virtual object held in the user�s hand, whether it is tracked directly or by a motion controller. The grip pose is defined as follows: - The grip position: - For tracked hands: The user�s palm centroid when closing the fist, at the surface of the palm. - For handheld motion controllers: A fixed position within the controller that generally lines up with the palm centroid when held by a hand in a neutral position. This position should be adjusted left or right to center the position within the controller�s grip. - The grip orientation�s +X axis: When you completely open your hand to form a flat 5-finger pose, the ray that is normal to the user�s palm (away from the palm in the left hand, into the palm in the right hand). - The grip orientation�s -Z axis: When you close your hand partially (as if holding the controller), the ray that goes through the center of the tube formed by your non-thumb fingers, in the direction of little finger to thumb. - The grip orientation�s +Y axis: orthogonal to +Z and +X using the right-hand rule. |
| **MESH** = 2 | A pose ([grip_surface](https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#semantic-paths-standard-pose-identifiers)) that allows applications to reliably anchor visual content relative to the user�s physical hand, whether the user�s hand is tracked directly or its position and orientation is inferred by a physical controller. The grip_surface pose is defined as follows: - The grip_surface position: The user�s physical palm centroid, at the surface of the palm. For the avoidance of doubt, the palm does not include fingers. - The grip_surface orientation�s +X axis: When a user is holding the controller and straightens their index fingers pointing forward, the ray that is normal (perpendicular) to the user�s palm (away from the palm in the left hand, into the palm in the right hand). - The grip_surface orientation�s -Z axis: When a user is holding the controller and straightens their index finger, the ray that is parallel to their finger�s pointing direction. - The grip_surface orientation�s +Y axis: orthogonal to +Z and +X using the right-hand rule. |
| **PINCH** = 3 | [Pinch pose](https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#_pinch_pose) designed for interacting with a small object within arm�s reach using a finger and thumb with a "pinch" gesture. For example, turning a key to open a lock or moving the knob on a slider control are interactions suited to the "pinch" pose. |
| **POKE** = 4 | [Poke pose](https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#_poke_pose) designed for interactions using a fingertip to touch and push a small object. For example, pressing a push button with a fingertip, swiping to scroll a browser view, or typing on a virtual keyboard are interactions suited to the "poke" pose. |
| **GAZE** = 5 | [Gaze pose](https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#_eye_gaze_input) represents the user's gaze direction and is designed for interactions based on real time user's eye tracking. The gaze pose is typically used for interactions such as pointing, object selection, UI targeting, and attention-based interaction. It provides a natural method for determining user intent based on what they are currently looking at in the scene. The gaze pose is defined as follows: - The gaze position: The center point between the user's eyes (when eye tracking is active), or an estimated point between the eyes based on head tracking. - The gaze orientation's -Z axis: The direction in which the user is looking. When eye tracking is available, this reflects the user's actual line of sight; otherwise, it aligns with the forward direction of the head. - The gaze orientation's +Y axis: Generally upward from the user's face. - The gaze orientation's +X axis: To the right from the user's perspective, forming a right-handed coordinate system. > **Notice:** This feature is only available for OpenXR devices. |
| **NUM_TRANSFORM_TYPES** = 6 | Total number of transformation types. |

### Properties

## 🔒︎ bool IsAvailable

The value indicating if the VR device is available.
## 🔒︎ int Number

The index of the VR device.
## 🔒︎ string Name

The name of the VR device.
## 🔒︎ Input.DEVICE DeviceType

The type of the input device (wheel, throttle, etc.).
## 🔒︎ InputVRDevice.TYPE Type

The type of the VR device (HMD, controller, base station, etc.).
## 🔒︎ string DeviceModelName

The name of the model of the VR device.
## 🔒︎ bool IsBatteryCharging

The value indicating if the device's battery is currently charging.
## 🔒︎ bool IsBatteryPluggedIn

The value indicating if the device is connected to external power. *OpenVR* runtimes report no separate plugged-in state, so the charging state is used as the signal there.
## 🔒︎ bool IsBatteryValid

The value indicating if the device actually provides battery status information, so that the battery-related values (charge level, charging state) can be trusted. *OpenXR* runtimes always report true.
## 🔒︎ float BatteryValue

The battery level.
## 🔒︎ string ModelNumber

The model number for the VR device.
## 🔒︎ string SerialNumber

The serial number for the VR device.
## 🔒︎ string ManufacturerName

The name of the VR device's vendor.
## 🔒︎ ulong HardwareRevision

The hardware revision of the VR device.
## 🔒︎ ulong FirmwareVersion

The firmware revision of the VR device.
## 🔒︎ int NumModels

The number of VR device's models.
## 🔒︎ Mesh CombinedModelMesh

The entire mesh of the combined model of the VR device.
> **Notice:** You cannot animate this mesh. However, if you get a mesh of each model individually, it will be automatically animated.


## 🔒︎ Texture CombinedModelTexture

The texture of the combined model of the VR device.
## 🔒︎ string CombinedModelName

The name of the combined model of the VR device.
### Members

---

## bool HasYawDrift ( )

Returns a value indicating if the VR device will drift in a specific direction.
### Return value

true if the device has yaw drift; otherwise, false.
## bool HasBattery ( )

Returns a value indicating if the VR device has a battery.
### Return value

true if the device has the battery; otherwise, false.
## bool IsVelocityValid ( InputVRDevice.TRANSFORM_TYPE type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP )

Returns a value indicating if the velocity of the VR device for the specified transformation type is valid.
### Arguments

- *[InputVRDevice.TRANSFORM_TYPE](../../../api/library/controls/class.inputvrdevice_cs.md#TRANSFORM_TYPE)* **type** - Transformation type.

### Return value

true if velocity is valid; otherwise, false.
## bool IsTransformTypeSupported ( InputVRDevice.TRANSFORM_TYPE type = Enum.InputVRDevice.TRANSFORM_TYPE.GRIP )

Returns a value indicating if the VR device supports the specified transformation type.
### Arguments

- *[InputVRDevice.TRANSFORM_TYPE](../../../api/library/controls/class.inputvrdevice_cs.md#TRANSFORM_TYPE)* **type** - Transformation type.

### Return value

true if transformation type is supported; otherwise, false.
## mat4 GetModelTransform ( int num )

Returns the local transformation of the given model.
### Arguments

- *int* **num** - Model index.

### Return value

Local transformation matrix of the model.
## mat4 GetModelWorldTransform ( int num )

Returns the world transformation of the given model.
### Arguments

- *int* **num** - Model index.

### Return value

World transformation matrix of the model.
## Mesh GetModelMesh ( int num )

Returns the mesh of the given model.
### Arguments

- *int* **num** - Model index.

### Return value

Model mesh.
## Texture GetModelTexture ( int num )

Returns the texture of the given model.
### Arguments

- *int* **num** - Model index.

### Return value

Model texture.
## string GetModelName ( int num )

Returns the name of the given model.
### Arguments

- *int* **num** - Model index.

### Return value

Model name.
