# Unigine::Plugins::RTSPStreamer::RTSPStreamer Class (CPP)

**Header:** #include <plugins/Unigine/RTSPStreamer/UnigineRTSPStreamer.h>


This class allows an application to create streams from *Player* cameras, retrieve stream URLs, subscribe to encoded H.264 frames, control debug overlays, add GUI widgets to the streamed image, and change the stream camera at runtime.


## Creating a Stream


Example:


```cpp
#include <plugins/Unigine/RTSPStreamer/UnigineRTSPStreamer.h>

using namespace Unigine;
using namespace Unigine::Plugins;

// access the plugin interface
RTSPStreamer *streamer = RTSPStreamer::get();

// Before creating streams, check that the plugin is available and initialized
if (streamer && streamer->isInitialized())
{
	// creating a stream
	RTSPStreamer::StreamDescription desc;
	desc.width = 1920;
	desc.height = 1080;
	desc.target_fps = 60.0f;
	desc.bitrate_kbps = 0;
	desc.encoder.preset = RTSPStreamer::EncoderPreset::LowLatency;

	PlayerDummyPtr camera = PlayerDummy::create();

	RTSPStreamer::StreamHandle handle = streamer->addStream("camera1", camera, desc);

	if (handle.value != RTSPStreamer::StreamHandle::InvalidHandle)
	{
		Log::message("Stream URL: %s\n", streamer->getStreamUrl(handle));
	}

	// Later:
	streamer->removeStream(handle);
}

```


The stream name becomes part of the RTSP URL: *rtsp://<host>:8554/camera1*


## RTSPStreamer Class

### Enums

## H264Profile

| Name | Description |
|---|---|
| **Auto** = 0 | Lets the encoder select the H.264 profile automatically based on the stream parameters and selected preset. |
| **Baseline** = 1 | Uses the H.264 Baseline profile. Provides maximum compatibility with older or simpler decoders, but offers lower compression efficiency than Main or High. |
| **Main** = 2 | Uses the H.264 Main profile. Provides a balance between decoder compatibility and compression efficiency. |
| **High** = 3 | Uses the H.264 High profile. Provides better compression efficiency when supported by the target decoder. |

## H264Level

| Name | Description |
|---|---|
| **Auto** = 0 | Lets the encoder or client select the H.264 level automatically based on the stream parameters. |
| **L3_0** = 1 | Sets H.264 level 3.0 explicitly. |
| **L3_1** = 2 | Sets H.264 level 3.1 explicitly. |
| **L3_2** = 3 | Sets H.264 level 3.2 explicitly. |
| **L4_0** = 4 | Sets H.264 level 4.0 explicitly. |
| **L4_1** = 5 | Sets H.264 level 4.1 explicitly. |
| **L4_2** = 6 | Sets H.264 level 4.2 explicitly. |
| **L5_0** = 7 | Sets H.264 level 5.0 explicitly. |
| **L5_1** = 8 | Sets H.264 level 5.1 explicitly. |
| **L5_2** = 9 | Sets H.264 level 5.2 explicitly. |
| **L6_0** = 10 | Sets H.264 level 6.0 explicitly. |
| **L6_1** = 11 | Sets H.264 level 6.1 explicitly. |
| **L6_2** = 12 | Sets H.264 level 6.2 explicitly. |

## EncoderPreset

| Name | Description |
|---|---|
| **UltraLowLatency** = 0 | Optimizes encoding for minimum latency. Recommended for live streaming and interactive applications. |
| **LowLatency** = 1 | Keeps latency low while allowing slightly better visual quality than UltraLowLatency. |
| **Quality** = 2 | Prioritizes visual quality over minimum latency. |

### Structs

## struct StreamHandle

Stream handle. If equals to 0, this means that the stream handle is invalid and the stream was not created or is no longer available.
### Fields

- *int* **value** - Stream handle.

## struct FrameCallbackHandle

Callback handle that identifies a subscription to encoded frame data. It is returned by [addStreamFrameEncodedCallback()](#addStreamFrameEncodedCallback_StreamHandle_FrameEncodedCallback_FrameCallbackHandle) and is required when removing the callback.
### Fields

- *int* **value** - Callback handle. If equals to 0, this means that the handle is invalid.

## struct EncoderSettings

Defines H.264 encoder settings for a stream.
### Fields

- *[H264Profile](/api/library/plugins/rtspstreamer/class.rtspstreamer#H264Profile)* **profile** - [H.264 profile](#H264Profile).
- *[H264Level](/api/library/plugins/rtspstreamer/class.rtspstreamer#H264Level)* **level** - [H.264 level](#H264Level).
- *[EncoderPreset](/api/library/plugins/rtspstreamer/class.rtspstreamer#EncoderPreset)* **preset** - [Encoder preset](#EncoderPreset).

## struct StreamDescription

Defines stream parameters used when creating a new stream.
### Fields

- *int* **width** - Output frame width in pixels. The value must be even because the stream is converted to NV12 4:2:0 before encoding. Supported range: [2, 16000].
- *int* **height** - Output frame height in pixels. The value must be even because the stream is converted to NV12 4:2:0 before encoding. Supported range: [2, 16000].
- *float* **target_fps** - Target encoding frame rate. This value controls how often frames are encoded and sent to the stream. If set to 0, the plugin uses 60 FPS by default. It does not limit the engine rendering FPS.
- *int* **bitrate_kbps** - Average video bitrate in kilobits per second. Defines how much data the encoder uses for the stream. Higher values usually improve image quality but increase network traffic. If set to 0, the plugin selects the bitrate automatically based on the stream resolution and target FPS.
- *int* **slot_count** - Number of render-target slots used by the stream. A value of 1 provides minimum latency because only one frame slot is used. Values greater than 1 allow the renderer to queue frames ahead, which can help smooth processing but may increase latency.
- *EncoderSettings* **encoder** - H.264 encoder settings for the stream. Includes the encoder profile, level, and preset. These settings control compatibility, stream complexity limits, compression behavior, quality, and latency tradeoffs.

### Members

## bool isInitialized () const

Returns the current flag indicating whether the plugin has been initialized successfully and is ready to create streams.
### Return value

**true** if the plugin initialization is completed successfully is enabled ; otherwise **false**.
---

## RTSPStreamer::StreamHandle addStream ( const char * name , const Ptr < Player > & player , const RTSPStreamer::StreamDescription & desc )


Creates a new stream from a specific camera according to the specified description. Stream creation may fail if the name is empty, already used, or longer than 100 characters; if the resolution is odd or outside the supported range; if target FPS is outside the supported range; or if NVENC is not available.


The stream URL has the following format: *rtsp://<host>:<port>/<name>*.


### Arguments

- *const char ** **name** - Stream name. It must be unique, non-empty, and no longer than 100 characters.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Player](../../../../api/library/players/class.player_cpp.md)> &* **player** - Player camera used for streaming.
- *const [RTSPStreamer::StreamDescription](../../../../api/library/plugins/rtspstreamer/class.rtspstreamer_cpp.md#StreamDescription) &* **desc** - Stream description.

### Return value

Valid StreamHandle if the stream was created successfully, or an invalid handle if stream creation fails.
## void removeStream ( const RTSPStreamer::StreamHandle & stream )

Removes the specified stream. This unregisters the stream from the RTSP server, stops encoding, and releases associated resources. Invalid or unknown handles are ignored.
### Arguments

- *const [RTSPStreamer::StreamHandle](../../../../api/library/plugins/rtspstreamer/class.rtspstreamer_cpp.md#StreamHandle) &* **stream** - Handle to the stream.

## const char * getStreamUrl ( const RTSPStreamer::StreamHandle & stream ) const

Returns the full RTSP URL of the specified stream. Returns *nullptr* if the stream does not exist or if the plugin is running in callback-only mode with the RTSP server disabled.
### Arguments

- *const [RTSPStreamer::StreamHandle](../../../../api/library/plugins/rtspstreamer/class.rtspstreamer_cpp.md#StreamHandle) &* **stream** - Handle to the stream.

### Return value

Full stream URL in the format: *rtsp://<host>:<port>/<name>*.
## RTSPStreamer::FrameCallbackHandle addStreamFrameEncodedCallback ( const RTSPStreamer::StreamHandle & stream , CallbackBase3 <const char *, unsigned int, unsigned long long> * callback )

Subscribes to encoded H.264 frames produced by the specified stream. The callback receives H.264 Annex-B frame data. The plugin takes ownership of the callback object if the subscription is successful. If the subscription fails, the plugin deletes the callback object. This callback mechanism also works when the RTSP server is disabled.


> **Notice:** - The callback is called from the encoder thread, not from the main thread. The application must synchronize access to shared data.
> - The *data* pointer is valid only during the callback call and must be copied if it needs to be stored.


```cpp
RTSPStreamer::FrameCallbackHandle callback_handle = streamer->addStreamFrameEncodedCallback(stream, callback);

```


### Arguments

- *const [RTSPStreamer::StreamHandle](../../../../api/library/plugins/rtspstreamer/class.rtspstreamer_cpp.md#StreamHandle) &* **stream** - Handle to the stream.
- *[CallbackBase3](../../../../api/library/common/callbacks/class.callbackbase3_cpp.md)<const char *, unsigned int, unsigned long long> ** **callback** - Callback function that receives encoded H.264 frame data in Annex-B format. The callback provides a pointer to the encoded data buffer, the buffer size in bytes, and the frame presentation timestamp.

### Return value

FrameCallbackHandle that can be used to [remove the callback](#removeStreamFrameEncodedCallback_StreamHandle_FrameCallbackHandle_void) later.
## void removeStreamFrameEncodedCallback ( const RTSPStreamer::StreamHandle & stream , const RTSPStreamer::FrameCallbackHandle & callback_handle )

Removes a previously [registered encoded-frame callback](#addStreamFrameEncodedCallback_StreamHandle_FrameEncodedCallback_FrameCallbackHandle) from the specified stream.
### Arguments

- *const [RTSPStreamer::StreamHandle](../../../../api/library/plugins/rtspstreamer/class.rtspstreamer_cpp.md#StreamHandle) &* **stream** - Handle to the stream.
- *const [RTSPStreamer::FrameCallbackHandle](../../../../api/library/plugins/rtspstreamer/class.rtspstreamer_cpp.md#FrameCallbackHandle) &* **callback_handle** - FrameCallbackHandle for removing the callback.

## void setShowDebugInfo ( const RTSPStreamer::StreamHandle & stream , bool show )

Enables or disables the debug overlay for the specified stream. The overlay is rendered into the streamed image and can include the stream URL, client count, encoder settings, hardware information, camera name, FPS, frame number, and timing information.


```cpp
Unigine::Plugins::RTSPStreamer::get()->setShowDebugInfo(stream, true);

```


### Arguments

- *const [RTSPStreamer::StreamHandle](../../../../api/library/plugins/rtspstreamer/class.rtspstreamer_cpp.md#StreamHandle) &* **stream** - Handle to the stream.
- *bool* **show** - true to enable the debug overlay for the specified stream, false to disable it.

## bool isShowDebugInfo ( const RTSPStreamer::StreamHandle & stream ) const

Returns the value indicating if the debug overlay is enabled for the specified stream. The overlay is rendered into the streamed image and can include the stream URL, client count, encoder settings, hardware information, camera name, FPS, frame number, and timing information.
### Arguments

- *const [RTSPStreamer::StreamHandle](../../../../api/library/plugins/rtspstreamer/class.rtspstreamer_cpp.md#StreamHandle) &* **stream** - Handle to the stream.

### Return value

true if the debug overlay is enabled for the specified stream, otherwise false.
## void addWidget ( const RTSPStreamer::StreamHandle & stream , const Ptr < Widget > & widget , int flags = -1 )

Adds a GUI widget to the specified stream. The widget is rendered into the encoded video frame as an overlay.
### Arguments

- *const [RTSPStreamer::StreamHandle](../../../../api/library/plugins/rtspstreamer/class.rtspstreamer_cpp.md#StreamHandle) &* **stream** - Handle to the stream.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../../api/library/gui/class.widget_cpp.md)> &* **widget** - GUI widget.
- *int* **flags** - Alignment flags, one of the [Gui::ALIGN_*](../../../../api/library/gui/class.gui_cpp.md#ALIGN_CENTER) values.

## void removeWidget ( const RTSPStreamer::StreamHandle & stream , const Ptr < Widget > & widget )

Removes a GUI widget from the specified stream.
### Arguments

- *const [RTSPStreamer::StreamHandle](../../../../api/library/plugins/rtspstreamer/class.rtspstreamer_cpp.md#StreamHandle) &* **stream** - Handle to the stream.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../../api/library/gui/class.widget_cpp.md)> &* **widget** - GUI widget.

## void setStreamPlayer ( const RTSPStreamer::StreamHandle & stream , const Ptr < Player > & player )

Changes the camera used by the specified stream. Passing *nullptr* pauses the stream without destroying it. Setting a valid Player again resumes streaming from the new camera.
### Arguments

- *const [RTSPStreamer::StreamHandle](../../../../api/library/plugins/rtspstreamer/class.rtspstreamer_cpp.md#StreamHandle) &* **stream** - Handle to the stream.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Player](../../../../api/library/players/class.player_cpp.md)> &* **player** - Player camera used for streaming. Passing *nullptr* pauses the stream without destroying it. Setting a valid Player again resumes streaming from the new camera.
