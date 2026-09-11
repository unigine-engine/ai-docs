# RTSPStreamer Plugin (CS)


The UNIGINE *RTSPStreamer* plugin publishes the image rendered from a UNIGINE *Player* camera as a live H.264 RTSP stream. Each selected viewport is rendered into a GPU texture, converted from RGBA to NV12, encoded with NVIDIA NVENC, and delivered over the network by the built-in live555 RTSP server.


[![](index.jpg)](index.jpg)


The plugin is designed for scenarios where rendered camera views need to be consumed by external RTSP-compatible tools or systems, such as VLC, mpv, ffmpeg, GStreamer, video processing pipelines, monitoring software, or remote operator interfaces.


Multiple streams can run simultaneously. Each stream has its own camera, resolution, target FPS, bitrate, render-target slot count, and encoder settings. This makes it possible to publish several independent views from the same UNIGINE application.


Encoding is performed on NVIDIA GPUs using NVENC. The rendered image remains on the GPU throughout the pipeline, including color conversion from RGBA to NV12, which avoids CPU readback and reduces system memory traffic. The plugin uses BT.709 limited-range color conversion, suitable for HD video playback in common clients.


For live streaming, the plugin uses low-latency H.264 settings: B-frames are disabled, adaptive quantization is enabled, and a key frame can be forced when a new client connects, allowing playback to start without waiting for the next scheduled IDR frame.


The RTSP server can allow TCP, UDP, or both transport modes. It can also be disabled entirely when RTSP output is not required and encoded H.264 frames are needed only through application callbacks.


The plugin also includes:


- Editor component for setting up streams directly on *Player* nodes
- Runtime debug overlays + possibility to use user widgets
- Profiling kill-switch for disabling measurement overhead in production


### See Also


- [RTSPStreamer Plugin API](../../../api/library/plugins/rtspstreamer/index.md)


## Typical Use Cases


![](use_cases.jpg)


The plugin can be useful in a wide range of simulation, visualization, and monitoring workflows:


- Remote observation of a UNIGINE application from standard video clients
- Streaming camera feeds into video analytics or recording pipelines
- Publishing multiple simulation viewpoints to operator stations
- Integrating UNIGINE-rendered imagery into external broadcast or control systems
- Exporting encoded frames directly through callbacks for custom network or storage backends


Since the output is a standard RTSP stream with H.264 video, it can be consumed by common tools without writing a custom client.


## Requirements


The plugin requires:


- **NVIDIA GPU** with NVENC support
- **NVIDIA driver** compatible with **CUDA 12** or newer


No additional CUDA installation is required: the CUDA runtime is linked statically into the plugin, while CUDA Driver API, NVENC, and NVML are loaded dynamically from the installed NVIDIA driver.


The supported rendering backends are **Vulkan** and **Direct3D 12**.


## Server Configuration


The RTSP server is configured through `data/plugins/Unigine/RTSPStreamer/server_config.json`, which is read on the plugin initialization.


Example configuration:


```xml
{
    "start_server": true,
    "port": 8554,
    "transport": "any"
}

```


| start_server | Controls whether the RTSP server socket is opened. When set to false, streams and encoders are still created, but encoded frames are available only through callbacks. |
|---|---|
| port | Defines the RTSP server port. By default, the plugin uses port 8554. |
| transport | Can be set to any, tcp, or udp. If a client requests a transport mode that is not allowed, the server responds with *461 Unsupported Transport*. |


If the configuration file is missing, incomplete, or contains invalid values, the plugin writes a warning to the log and falls back to default settings.


## How the Streaming Pipeline Works


![](workflow.jpg)


For each stream, the plugin renders the selected ***[Player](../../../objects/players/index.md)*** camera into a texture. The image is then converted from RGBA to NV12 on the GPU. NV12 is a YUV 4:2:0 format widely used by video encoders and players. The converted frame is then passed to NVIDIA NVENC, which encodes it into H.264 using a dedicated hardware encoder on the GPU.


The CPU-side part of the process runs in a separate worker thread: it prepares frames, submits them to NVENC, receives encoded data, and sends it to the RTSP server and/or user callbacks. The actual video compression is handled by NVENC, so encoding does not directly block the main rendering pipeline.


All active streams share the available NVENC encoder engines. If several streams use the same encoder engine, frames are processed in turn. Higher resolution, more streams, higher bitrate, and heavier encoder settings **can increase encoding time**.


The ***[target_fps](../../../api/library/plugins/rtspstreamer/class.rtspstreamer_cs.md#StreamDescription)*** value only defines the intended stream frame rate and is used by the encoder configuration and timing logic.


## Editor Component: RTSPStreamSetup


For editor-based workflows, the plugin includes the ***RTSPStreamSetup*** component (`data/plugins/Unigine/RTSPStreamer/components/RTSPStreamSetup.prop`).


The component is assigned to a ***Player*** node. During world initialization, it creates a stream from that camera. During shutdown, it removes the stream automatically.


The component exposes stream parameters such as name, resolution, target FPS, bitrate, render-target slot count, debug overlay visibility, encoder preset, H.264 profile, and H.264 level.


This allows artists and technical users to configure RTSP output directly in the editor without writing code.


![](component.png)

*RTSPStreamSetup component*


| Parameter | Description |
|---|---|
| Name | Stream URL path component. Must be unique and no longer than 100 characters. |
| Width | Output frame width in pixels. Must be even and within the [2, 16000] range. |
| Height | Output frame height in pixels. Must be even and within the [2, 16000] range. |
| Target FPS | Target encoding frame rate. 0 means 60 FPS by default. This value controls encoding rate only and does not limit the engine rendering FPS. |
| Bitrate (kbps) | Average video bitrate in kilobits per second. 0 enables automatic bitrate selection based on resolution and FPS. |
| Slot count | Number of render-target slots used as an internal frame buffer for the stream. This value defines how many rendered frames can be held before they are passed to the encoder. If rendering is significantly faster than encoding, increasing this value can reduce frame drops caused by unavailable slots. Higher values may increase buffering and latency. |
| Show debug info | Enables or disables the [debug information overlay](#debug) in the streamed image. |
| Preset | H.264 [encoder preset](../../../api/library/plugins/rtspstreamer/class.rtspstreamer_cs.md#EncoderPreset). |
| Profile | [H.264 profile](../../../api/library/plugins/rtspstreamer/class.rtspstreamer_cs.md#H264Profile). |
| Level | [H.264 level](../../../api/library/plugins/rtspstreamer/class.rtspstreamer_cs.md#H264Level). Available values: Auto, [3.0, 6.2]. |


## Debug Overlay and Runtime Metrics


The plugin includes a debug overlay that can be rendered directly into the outgoing video stream. It can display the stream URL, number of clients, encoder parameters, GPU information, camera name, engine FPS, frame counters, and timing information.


The overlay can be controlled per stream through the [API](../../../api/library/plugins/rtspstreamer/class.rtspstreamer_cs.md#setShowDebugInfo_StreamHandle_bool_void):


```csharp
Unigine.Plugins.RTSPStreamer.SetShowDebugInfo(stream, true);

```


It can also be toggled globally for all active streams using the console command `rtsp_streamer_show_debug_info 0|1`.


### Profiling Kill-Switch


In addition to the video overlay, the plugin provides a local debug window named ***RTSP Streamer*** controlled by a global profiling switch `rtsp_streamer_profiling 0|1`. This window displays common server information and detailed metrics for the selected stream, including frame size, render wait time, color conversion time, NVENC encoding time, push time, queue depth, and delivered NAL units.


Profiling is disabled by default. When disabled, the plugin does not perform CUDA event timing, CPU timing measurements, or NVML sampling. This avoids measurement overhead in production runs.


When profiling is enabled, timing data becomes available in the debug window scope.


![](overlay.jpg)


**Common**


| Parameter | Description |
|---|---|
| URL | Current RTSP server URL. |
| Overflow events | Number of server-side overflow events. |
| Clients total / TCP / UDP | Total number of connected clients and their transport distribution. |
| GPU | NVIDIA GPU used by the streamer. |
| Encoder engines | Number of available hardware encoder engines reported by NVML. |
| Encoder utilization | Current encoder utilization reported by NVML, if available. |
| Profiling | Global profiling switch state. |
| Streams | Number of active streams. |
| Engine FPS | Current engine frame rate. |
| Rendered this frame | Number of stream frames rendered during the current engine frame. |
| Drops: slot pool full | Number of dropped frames caused by unavailable render-target slots. |
| Drops: pacing | Number of dropped frames caused by target FPS pacing. |


**Selected Stream**


| Parameter | Description |
|---|---|
| Mount | RTSP mount name of the selected stream. |
| Resolution | Output resolution of the selected stream. |
| URL | Full RTSP URL of the selected stream. |
| Frame size | Size of the last encoded frame, in KB. |
| Wait (fence) | Time spent waiting for the rendered frame to become available on the GPU, measured in milliseconds using a CUDA event. |
| Convert (RGBA → NV12) | Time spent on GPU color conversion from RGBA to NV12, in milliseconds. |
| Encode (NVENC) | Time spent encoding the frame with NVENC, in milliseconds. |
| Push (to server) | Time spent delivering the encoded frame to live555 and/or frame callbacks, in milliseconds. |
| Total per frame | Total per-frame processing time in the encoder worker thread, in milliseconds. |
| Queue depth | Current depth of the live555 NAL-unit queue. |
| Pushed NALs | Number of NAL units pushed to the live555 queue. |
| Delivered NALs | Number of NAL units delivered from the live555 queue to clients. |
| Total delivered NALs | Total number of NAL units delivered by live555 to RTSP clients for the selected stream. This counter helps verify that encoded video data is being passed from the server queue to connected clients. |


## Connecting from RTSP Clients


After a stream is created, the plugin prints its URL to the log. Clients can connect using common RTSP-compatible tools:


```bash
ffplay rtsp://192.168.0.10:8554/camera1
mpv    rtsp://192.168.0.10:8554/camera1
vlc    rtsp://192.168.0.10:8554/camera1

```


When the server is configured to allow only TCP transport, ffplay can be launched as follows:


```bash
ffplay -rtsp_transport tcp rtsp://192.168.0.10:8554/camera1

```


The server listens on *0.0.0.0*. The LAN IP in the printed URL is provided as a convenience for clients on the local network.


## Limitations


- The current implementation supports H.264 encoding through NVIDIA NVENC only. A compatible NVIDIA GPU and driver are required.
- Frame dimensions must be even because the encoder input format is NV12 4:2:0.
- Encoded frame callbacks are executed from the encoder thread, so thread-safety must be handled by the application.
- NVML-based encoder utilization sampling is optional. If it is not available on a particular system, the overlay reports it as unsupported, while the rest of the streaming functionality remains available.
