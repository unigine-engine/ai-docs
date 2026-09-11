# Unigine::Plugins::Kinect Class (CS)

> **Notice:** This class is a singleton.


This set of functions is available when the [Kinect2 plugin](../../../code/plugins/kinect2/index_cs.md) is loaded. This plugin is used for receiving already detected data from a Kinect2 sensor.


> **Notice:** Kinect SDK 2.0+ must be installed on your computer.


If the plugin is loaded together with the engine, the `HAS_KINECT` definition is set. This definition can be used, for example, to avoid errors if the plugin is not loaded: the code in which the plugin functions are executed can be wrapped around as follows:


```csharp
#ifdef HAS_KINECT
	// kinect functions
#endif

```


The Unigine Kinect plugin works in the following way: when *[Kinect.IsBodyTracked(body)](#isBodyTracked_int_bool)* returns **0**, *[Kinect.GetBonePosition(body, bone)](#getBonePosition_int_int_vec3)* will return **vec3_zero**. Kinect has its own framerate, so the body tracking information is not available each engine frame. Wrist tracking can be achieved via:


```csharp
vec3 wrist;

int Update() {
    if(Kinect.IsBodyTracked(0)) {
        wrist = Kinect.GetBonePosition(0,KINECT.WRIST_LEFT);
    }
    Visualizer.RenderSphere(0.05f,translate(wrist),vec4_one);
    return 1;
}

```


### See Also


- Article on [Kinect2 Plugin](../../../code/plugins/kinect2/index_cs.md)
- UnigineScript samples:

  -
  -
  -


## Kinect Class

### Enums

## FACE_PROPERTY

| Name | Description |
|---|---|
| **HAPPY** = 0 | The user's face is happy (for example, the user is smiling). |
| **ENGAGED** = 1 | The user's face is engaged. |
| **GLASSES** = 2 | There are glasses on the face. |
| **EYE_LEFT_CLOSED** = 3 | The user's left eye is closed. |
| **EYE_RIGHT_CLOSED** = 4 | The user's right eye is closed. |
| **MOUTH_OPEN** = 5 | The user's mouth is open. |
| **MOUTH_MOVED** = 6 | The user's mouth moved. |
| **LOOKING_AWAY** = 7 | The user is looking away. |

## FACE_POINT

| Name | Description |
|---|---|
| **EYE_LEFT** = 0 | The left eye. |
| **EYE_RIGHT** = 1 | The right eye. |
| **NOSE** = 2 | The nose. |
| **MOUTH_CORNER_LEFT** = 3 | The left corner of the mouse. |
| **MOUTH_CORNER_RIGHT** = 4 | The right corner of the mouse. |

## FACE_DETECTION_RESULT

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | A flag indicating that the face is in the unknown state. |
| **NO** = 1 | A flag indicating that the face property (state) is not tracked. |
| **MAYBE** = 2 | A flag indicating that the face property (state) is partially tracked. |
| **YES** = 3 | A flag indicating that the face property (state) is tracked. |

## BONE

| Name | Description |
|---|---|
| **HEAD** = 3 | The head. |
| **NECK** = 2 | The neck. |
| **SPINE_SHOULDER** = 20 | The spine at the shoulder. |
| **SPINE_MID** = 1 | Middle of the spine. |
| **SPINE_BASE** = 0 | Base of the spine. |
| **SHOULDER_LEFT** = 4 | The left shoulder. |
| **ELBOW_LEFT** = 5 | The left elbow. |
| **WRIST_LEFT** = 6 | The left wrist. |
| **HAND_LEFT** = 7 | The left hand. |
| **HAND_TIP_LEFT** = 21 | The tip of the left hand. |
| **THUMB_LEFT** = 22 | The left thumb. |
| **SHOULDER_RIGHT** = 8 | The right shoulder. |
| **ELBOW_RIGHT** = 9 | The right elbow. |
| **WRIST_RIGHT** = 10 | The right wrist. |
| **HAND_RIGHT** = 11 | The right hand. |
| **HAND_TIP_RIGHT** = 23 | The tip of the right hand. |
| **THUMB_RIGHT** = 24 | The right thumb. |
| **HIP_LEFT** = 12 | The left hip (except the thumb). |
| **KNEE_LEFT** = 13 | The left knee. |
| **ANKLE_LEFT** = 14 | The left ankle. |
| **FOOT_LEFT** = 15 | The left foot. |
| **HIP_RIGHT** = 16 | The right hip (except the thumb). |
| **KNEE_RIGHT** = 17 | The right knee. |
| **ANKLE_RIGHT** = 18 | The right ankle. |
| **FOOT_RIGHT** = 19 | The right foot. |

## HAND_STATE

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | A flag indicating that the state of the hand is unknown. |
| **NOT_TRACKED** = 1 | A flag indicating that the state of the hand is not tracked. |
| **OPEN** = 2 | A flag indicating that the hand is open. |
| **CLOSED** = 3 | A flag indicating that the hand is closed (clenched in a fist). |
| **LASSO** = 4 | A flag indicating that the hand is in the lasso state (a closed hand with the middle and index fingers both up). |

## TRACKING_CONFIDENCE

| Name | Description |
|---|---|
| **LOW** = 0 | A flag indicating that a hand is tracked with the low level of confidence (perhaps a hand is tracked correctly). |
| **HIGH** = 1 | A flag indicating that a hand is tracked with the high level of confidence (a hand is fully tracked). |

## TRACKING_STATE

| Name | Description |
|---|---|
| **NOT_TRACKED** = 0 | A flag indicating that a body and bones aren't tracked. |
| **INFERRED** = 1 | A flag indicating that a body and bones are inferred (Kinect inferring their positions). |
| **TRACKED** = 2 | A flag indicating that a body and bones are being tracked. |

## NUM

| Name | Description |
|---|---|
| **BODIES** = 6 | Number of tracked bodies. The maximum value is **6**. |
| **BONES** = 25 | Number of tracked bones. The maximum value is **25**. |
| **FACE_POINTS** = 5 | Number of tracked face points (left and right eyes, nose, left and right mouth corners). The maximum value is **5**. |
| **FACE_PROPERTIES** = 8 | Number of tracked face states (for example, happy, engaged, wearing glasses and so on). The maximum value is **8**. |

## STREAM

| Name | Description |
|---|---|
| **COLOR** = 1 | A color stream. If this constant isn't specified on [sensor initialization](#init_uint_int), there will be no access to the color stream. |
| **INFRARED** = 2 | An infrared stream. If this constant isn't specified on [sensor initialization](#init_uint_int), there will be no access to the infrared stream. |
| **DEPTH** = 8 | A depth stream. If this constant isn't specified on [sensor initialization](#init_uint_int), there will be no access to the depth stream. |
| **BODY** = 32 | A body. If this constant isn't specified on [sensor initialization](#init_uint_int), bodies won't be tracked. |
| **ALL** = 43 | The [*COLOR*](#STREAM_COLOR), [*INFRARED*](#STREAM_INFRARED), [*DEPTH*](#STREAM_DEPTH), [*BODY*](#STREAM_BODY) constants combined by using **logical OR**. |

### Members

---

## Kinect.TRACKING_STATE GetBodyLeanState ( int body )

Returns a value indicating whether the body with the given number was tracked as lean or not.
### Arguments

- *int* **body** - Body index in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

One of the [TRACKING_STATE_*](#TRACKING_STATE_NOT_TRACKED) constants specifying the tracking state. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), [*TRACKING_STATE_NOT_TRACKED*](#TRACKING_STATE_NOT_TRACKED) will be returned.
## quat GetBoneOrientation ( int body , Kinect.BONE bone )

Returns orientation of the given bone of the given body relative to the parent bone.
### Arguments

- *int* **body** - Body number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].
- *[Kinect.BONE](../../../api/library/plugins/engine.kinect_cs.md#BONE)* **bone** - Bone number in range [0;[NUM_BONES](#NUM_BONES) - 1 ].

### Return value

Bone orientation relative to the parent bone. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), zero quat will be returned.
## vec3 GetBonePosition ( int body , Kinect.BONE bone )

Returns position of the given bone of the given body relative to the sensor.
### Arguments

- *int* **body** - Body number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].
- *[Kinect.BONE](../../../api/library/plugins/engine.kinect_cs.md#BONE)* **bone** - Bone number in range [0;[NUM_BONES](#NUM_BONES) - 1 ].

### Return value

Bone position relative to the sensor. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), zero vector will be returned.
## Kinect.TRACKING_STATE GetBoneState ( int body , Kinect.BONE bone )

Returns the current tracking state of the given bone of the given body.
### Arguments

- *int* **body** - Body number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].
- *[Kinect.BONE](../../../api/library/plugins/engine.kinect_cs.md#BONE)* **bone** - Bone number in range [0;[NUM_BONES](#NUM_BONES) - 1 ].

### Return value

One of the [TRACKING_STATE_*](#TRACKING_STATE_NOT_TRACKED) constants specifying the tracking state. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), [*TRACKING_STATE_NOT_TRACKED*](#TRACKING_STATE_NOT_TRACKED) will be returned.
## Image GetColorBuffer ( )


Returns an image representing the current color buffer in the RGBA8 format.


> **Notice:** The image in the color buffer is deleted each frame. However, the data isn't sent to the buffer each frame, so the function may return **NULL**.


### Return value

An image representing the current color buffer. If the [*STREAM_COLOR*](#STREAM_COLOR) is not specified on sensor [initialization](#init_uint_int), **NULL** will be returned.
## Image GetDepthBuffer ( )


Returns an image representing the current depth buffer in the R16 format.


> **Notice:** The image in the depth buffer is deleted each frame. However, the data isn't sent to the buffer each frame, so the function may return **NULL**.


### Return value

An image representing the current depth buffer. If the [*STREAM_DEPTH*](#STREAM_DEPTH) is not specified on sensor [initialization](#init_uint_int), **NULL** will be returned.
## ivec4 GetFaceBoundsInColorSpace ( int face )

Returns bounds of the given face relative to the size of the color buffer.
### Arguments

- *int* **face** - Face number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

Face bounds in the format *(Left,Top,Right,Bottom)*. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), zero vector will be returned.
## ivec4 GetFaceBoundsInInfraredSpace ( int face )

Returns bounds of the given face relative to the size of the infrared buffer.
### Arguments

- *int* **face** - Face number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

Face bounds in the format *(Left,Top,Right,Bottom)*. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), zero vector will be returned.
## quat GetFaceOrientation ( int face )

Returns orientation of the given face relative to the sensor.
### Arguments

- *int* **face** - Face number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

Face orientation. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), zero quat will be returned.
## vec3 GetFacePointInColorSpace ( int face , Kinect.FACE_POINT point )


Returns coordinates of the given point on the given face relative to the size of the color buffer.


> **Notice:** Only *X* and *Y* components of the returned vector are used, *Z* component should be ignored.


### Arguments

- *int* **face** - Face number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].
- *[Kinect.FACE_POINT](../../../api/library/plugins/engine.kinect_cs.md#FACE_POINT)* **point** - Face point number in range [0;[NUM_FACE_POINTS](#NUM_FACE_POINTS) - 1 ].

### Return value

Face point coordinates. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), zero vector will be returned.
## vec3 GetFacePointInInfraredSpace ( int face , Kinect.FACE_POINT point )


Returns coordinates of the given point on the given face relative to the size of the infrared buffer.


> **Notice:** Only *X* and *Y* components of the returned vector are used, *Z* component should be ignored.


### Arguments

- *int* **face** - Face number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].
- *[Kinect.FACE_POINT](../../../api/library/plugins/engine.kinect_cs.md#FACE_POINT)* **point** - Face point number in range [0;[NUM_FACE_POINTS](#NUM_FACE_POINTS) - 1 ].

### Return value

Face point coordinates. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), zero vector will be returned.
## Kinect.FACE_DETECTION_RESULT GetFaceProperty ( int face , Kinect.FACE_PROPERTY property )

Returns a value indicating how accurate the property of the given face was tracked.
### Arguments

- *int* **face** - Face number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].
- *[Kinect.FACE_PROPERTY](../../../api/library/plugins/engine.kinect_cs.md#FACE_PROPERTY)* **property** - Face property number in range [0;[NUM_FACE_PROPERTIES](#NUM_FACE_PROPERTIES) - 1 ].

### Return value

One of the [*KINECT_FACE_DETECTION_RESULT_**](#FACE_DETECTION_RESULT_UNKNOWN) constants. If The [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), [*KINECT_FACE_DETECTION_RESULT_UNKNOWN*](#FACE_DETECTION_RESULT_UNKNOWN) will be returned.
## Image GetInfraredBuffer ( )


Returns an image representing the current infrared buffer in the R16 format.


> **Notice:** The image in the infrared buffer is deleted each frame. However, the data isn't sent to the buffer each frame, so the function may return **NULL**.


### Return value

An image representing the current infrared buffer. If the [*STREAM_INFRARED*](#STREAM_INFRARED) is not specified on sensor [initialization](#init_uint_int), **NULL** will be returned.
## Kinect.TRACKING_CONFIDENCE GetLeftHandConfidence ( int body )

Returns the confidence level for the tracked left hand of the given body.
### Arguments

- *int* **body** - Body number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

One of the [*TRACKING_CONFIDENCE_**](#TRACKING_CONFIDENCE_LOW). If The [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), [*TRACKING_CONFIDENCE_LOW*](#TRACKING_CONFIDENCE_LOW) will be returned.
## Kinect.HAND_STATE GetLeftHandState ( int body )

Returns the current state of the left hand of the given body.
### Arguments

- *int* **body** - Body number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

One of the [*HAND_STATE_**](#HAND_STATE_UNKNOWN). If The [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), [*HAND_STATE_UNKNOWN*](#HAND_STATE_UNKNOWN) will be returned.
## Kinect.TRACKING_CONFIDENCE GetRightHandConfidence ( int body )

Returns the confidence level for the tracked right hand of the given body.
### Arguments

- *int* **body** - Body number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

One of the [*TRACKING_CONFIDENCE_**](#TRACKING_CONFIDENCE_LOW). If The [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), [*TRACKING_CONFIDENCE_LOW*](#TRACKING_CONFIDENCE_LOW) will be returned.
## Kinect.HAND_STATE GetRightHandState ( int body )

Returns the current state of the right hand of the given body.
### Arguments

- *int* **body** - Body number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

One of the [*HAND_STATE_**](#HAND_STATE_UNKNOWN). If The [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), [*HAND_STATE_UNKNOWN*](#HAND_STATE_UNKNOWN) will be returned.
## int Init ( uint stream_flags )

Kinect2 sensor initialization. The [*STREAM_**](#STREAM_COLOR) constants specify which data streams should be initialized.
### Arguments

- *uint* **stream_flags** - A bit mask represented by one of or combination of the [*STREAM_**](#STREAM_COLOR) constants.

### Return value

1 if the sensor was initialized successfully; otherwise, 0.
### Examples


For example, there will be access to the color and depth buffers if you initialize the sensor as follows:


```cpp
engine.kinect.init(KINECT_STREAM_COLOR | KINECT_STREAM_DEPTH);
```


## bool isBodyTracked ( int body )

Returns a value indicating if the body with the given number was tracked by the sensor.
### Arguments

- *int* **body** - Body number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

true if the body was tracked; otherwise, false. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), fals will be returned.
## bool isFaceTracked ( int face )

Returns a value indicating whether the face with the given number was tracked or not.
### Arguments

- *int* **face** - Face number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

true if the given face is tracked; otherwise, false. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), false will be returned.
## void Shutdown ( )

Kinect2 sensor shutdown.
