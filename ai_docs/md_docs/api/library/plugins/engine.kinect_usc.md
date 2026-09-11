# Unigine::Plugins::Kinect Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This set of functions is available when the [Kinect2 plugin](../../../code/plugins/kinect2/index_usc.md) is loaded. This plugin is used for receiving already detected data from a Kinect2 sensor.


> **Notice:** Kinect SDK 2.0+ must be installed on your computer.


If the plugin is loaded together with the engine, the `HAS_KINECT` definition is set. This definition can be used, for example, to avoid errors if the plugin is not loaded: the code in which the plugin functions are executed can be wrapped around as follows:


```cpp
#ifdef HAS_KINECT
	// engine.kinect functions
#endif

```


The UNIGINE Kinect plugin works in the following way: when *[engine.kinect.isBodyTracked(body)](#isBodyTracked_int_bool)* returns **0**, *[engine.kinect.getBonePosition(body, bone)](#getBonePosition_int_int_vec3)* will return **vec3_zero**. Kinect has its own framerate, so the body tracking information is not available each engine frame. Wrist tracking can be achieved via:


```cpp
vec3 wrist;

int update() {
    if(engine.kinect.isBodyTracked(0)) {
        wrist = engine.kinect.getBonePosition(0,KINECT_BONE_WRIST_LEFT);
    }
    engine.visualizer.renderSphere(0.05f,translate(wrist),vec4_one);
    return 1;
}

```


### See Also


- Article on [Kinect2 Plugin](../../../code/plugins/kinect2/index_usc.md)
- UnigineScript samples:

  -
  -
  -


## Kinect Class

---

## int engine.kinect. getBodyLeanState ( int body )

Returns a value indicating whether the body with the given number was tracked as lean or not.
### Arguments

- *int* **body** - Body index in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

One of the [TRACKING_STATE_*](#TRACKING_STATE_NOT_TRACKED) constants specifying the tracking state. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), [*TRACKING_STATE_NOT_TRACKED*](#TRACKING_STATE_NOT_TRACKED) will be returned.
## quat engine.kinect. getBoneOrientation ( int body , int bone )

Returns orientation of the given bone of the given body relative to the parent bone.
### Arguments

- *int* **body** - Body number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].
- *int* **bone** - Bone number in range [0;[NUM_BONES](#NUM_BONES) - 1 ].

### Return value

Bone orientation relative to the parent bone. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), zero quat will be returned.
## vec3 engine.kinect. getBonePosition ( int body , int bone )

Returns position of the given bone of the given body relative to the sensor.
### Arguments

- *int* **body** - Body number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].
- *int* **bone** - Bone number in range [0;[NUM_BONES](#NUM_BONES) - 1 ].

### Return value

Bone position relative to the sensor. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), zero vector will be returned.
## int engine.kinect. getBoneState ( int body , int bone )

Returns the current tracking state of the given bone of the given body.
### Arguments

- *int* **body** - Body number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].
- *int* **bone** - Bone number in range [0;[NUM_BONES](#NUM_BONES) - 1 ].

### Return value

One of the [TRACKING_STATE_*](#TRACKING_STATE_NOT_TRACKED) constants specifying the tracking state. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), [*TRACKING_STATE_NOT_TRACKED*](#TRACKING_STATE_NOT_TRACKED) will be returned.
## Image engine.kinect. getColorBuffer ( )


Returns an image representing the current color buffer in the RGBA8 format.


> **Notice:** The image in the color buffer is deleted each frame. However, the data isn't sent to the buffer each frame, so the function may return **NULL**.


### Return value

An image representing the current color buffer. If the [*STREAM_COLOR*](#STREAM_COLOR) is not specified on sensor [initialization](#init_uint_int), **NULL** will be returned.
## Image engine.kinect. getDepthBuffer ( )


Returns an image representing the current depth buffer in the R16 format.


> **Notice:** The image in the depth buffer is deleted each frame. However, the data isn't sent to the buffer each frame, so the function may return **NULL**.


### Return value

An image representing the current depth buffer. If the [*STREAM_DEPTH*](#STREAM_DEPTH) is not specified on sensor [initialization](#init_uint_int), **NULL** will be returned.
## ivec4 engine.kinect. getFaceBoundsInColorSpace ( int face )

Returns bounds of the given face relative to the size of the color buffer.
### Arguments

- *int* **face** - Face number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

Face bounds in the format *(Left,Top,Right,Bottom)*. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), zero vector will be returned.
## ivec4 engine.kinect. getFaceBoundsInInfraredSpace ( int face )

Returns bounds of the given face relative to the size of the infrared buffer.
### Arguments

- *int* **face** - Face number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

Face bounds in the format *(Left,Top,Right,Bottom)*. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), zero vector will be returned.
## quat engine.kinect. getFaceOrientation ( int face )

Returns orientation of the given face relative to the sensor.
### Arguments

- *int* **face** - Face number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

Face orientation. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), zero quat will be returned.
## vec3 engine.kinect. getFacePointInColorSpace ( int face , int point )


Returns coordinates of the given point on the given face relative to the size of the color buffer.


> **Notice:** Only *X* and *Y* components of the returned vector are used, *Z* component should be ignored.


### Arguments

- *int* **face** - Face number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].
- *int* **point** - Face point number in range [0;[NUM_FACE_POINTS](#NUM_FACE_POINTS) - 1 ].

### Return value

Face point coordinates. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), zero vector will be returned.
## vec3 engine.kinect. getFacePointInInfraredSpace ( int face , int point )


Returns coordinates of the given point on the given face relative to the size of the infrared buffer.


> **Notice:** Only *X* and *Y* components of the returned vector are used, *Z* component should be ignored.


### Arguments

- *int* **face** - Face number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].
- *int* **point** - Face point number in range [0;[NUM_FACE_POINTS](#NUM_FACE_POINTS) - 1 ].

### Return value

Face point coordinates. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), zero vector will be returned.
## int engine.kinect. getFaceProperty ( int face , int property )

Returns a value indicating how accurate the property of the given face was tracked.
### Arguments

- *int* **face** - Face number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].
- *int* **property** - Face property number in range [0;[NUM_FACE_PROPERTIES](#NUM_FACE_PROPERTIES) - 1 ].

### Return value

One of the [*KINECT_FACE_DETECTION_RESULT_**](#FACE_DETECTION_RESULT_UNKNOWN) constants. If The [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), [*KINECT_FACE_DETECTION_RESULT_UNKNOWN*](#FACE_DETECTION_RESULT_UNKNOWN) will be returned.
## Image engine.kinect. getInfraredBuffer ( )


Returns an image representing the current infrared buffer in the R16 format.


> **Notice:** The image in the infrared buffer is deleted each frame. However, the data isn't sent to the buffer each frame, so the function may return **NULL**.


### Return value

An image representing the current infrared buffer. If the [*STREAM_INFRARED*](#STREAM_INFRARED) is not specified on sensor [initialization](#init_uint_int), **NULL** will be returned.
## int engine.kinect. getLeftHandConfidence ( int body )

Returns the confidence level for the tracked left hand of the given body.
### Arguments

- *int* **body** - Body number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

One of the [*TRACKING_CONFIDENCE_**](#TRACKING_CONFIDENCE_LOW). If The [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), [*TRACKING_CONFIDENCE_LOW*](#TRACKING_CONFIDENCE_LOW) will be returned.
## int engine.kinect. getLeftHandState ( int body )

Returns the current state of the left hand of the given body.
### Arguments

- *int* **body** - Body number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

One of the [*HAND_STATE_**](#HAND_STATE_UNKNOWN). If The [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), [*HAND_STATE_UNKNOWN*](#HAND_STATE_UNKNOWN) will be returned.
## int engine.kinect. getRightHandConfidence ( int body )

Returns the confidence level for the tracked right hand of the given body.
### Arguments

- *int* **body** - Body number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

One of the [*TRACKING_CONFIDENCE_**](#TRACKING_CONFIDENCE_LOW). If The [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), [*TRACKING_CONFIDENCE_LOW*](#TRACKING_CONFIDENCE_LOW) will be returned.
## int engine.kinect. getRightHandState ( int body )

Returns the current state of the right hand of the given body.
### Arguments

- *int* **body** - Body number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

One of the [*HAND_STATE_**](#HAND_STATE_UNKNOWN). If The [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), [*HAND_STATE_UNKNOWN*](#HAND_STATE_UNKNOWN) will be returned.
## int engine.kinect. init ( unsigned int stream_flags )

Kinect2 sensor initialization. The [*STREAM_**](#STREAM_COLOR) constants specify which data streams should be initialized.
### Arguments

- *unsigned int* **stream_flags** - A bit mask represented by one of or combination of the [*STREAM_**](#STREAM_COLOR) constants.

### Return value

1 if the sensor was initialized successfully; otherwise, 0.
### Examples


For example, there will be access to the color and depth buffers if you initialize the sensor as follows:


```cpp
engine.kinect.init(KINECT_STREAM_COLOR | KINECT_STREAM_DEPTH);
```


## bool engine.kinect. isBodyTracked ( int body )

Returns a value indicating if the body with the given number was tracked by the sensor.
### Arguments

- *int* **body** - Body number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

true if the body was tracked; otherwise, false. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), fals will be returned.
## bool engine.kinect. isFaceTracked ( int face )

Returns a value indicating whether the face with the given number was tracked or not.
### Arguments

- *int* **face** - Face number in range [0;[NUM_BODIES](#NUM_BODIES) - 1 ].

### Return value

true if the given face is tracked; otherwise, false. If the [*STREAM_BODY*](#STREAM_BODY) is not specified on sensor [initialization](#init_uint_int), false will be returned.
## void engine.kinect. shutdown ( )

Kinect2 sensor shutdown.
