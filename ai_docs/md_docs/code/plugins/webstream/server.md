# Sample Server for WebStream Plugin

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


This server is provided as a test implementation. If required, you can develop your own signaling server using any suitable architecture. The server can also be used as a reference example: you can review the implemented logic and, if necessary, integrate it into your own web application.


The signaling server repository is available at [https://github.com/unigine-engine/unigine-webstream-signaling-server](https://github.com/unigine-engine/unigine-webstream-signaling-server). The server is distributed publicly, and users can download it from this repository.


## Setting Up the Server


1. The server is implemented using *Node.js*; therefore, *Node.js* must be installed before running it. The installer can be downloaded from [https://nodejs.org/en/download](https://nodejs.org/en/download), after which the installation wizard should be completed. For Linux systems, installation scripts for downloading and installing *Node.js* via the terminal are available on the same page.
2. After installing *Node.js*, clone the signaling server repository from GitHub ([https://github.com/unigine-engine/unigine-webstream-signaling-server](https://github.com/unigine-engine/unigine-webstream-signaling-server)).
3. The `signaling_server` directory contains the `setup` scripts for Windows and Linux. Run the required script to install all dependencies required for the server. ![Dependencies installed by the Windows setup script](setup_server.jpg) *Dependencies installed by the Windows setup script*


## Running the Web Interface


After the setup is completed, you can start the server using the `start` script.


After startup, the server outputs the message:


```text
Server running: http://localhost:8888

```


Opening this address in a browser displays the server web interface. The same address must be specified in the [`web_config.json` file](../../../code/plugins/webstream/index.md#web_config), after which the [runtime can be launched](../../../code/plugins/webstream/index.md#view).


## Streaming Settings


The web client provides a set of parameters for configuring video streaming. These parameters are used to select the codec, transport protocol, video stream characteristics, etc.


The *Settings* tab provides the interface for configuring the following parameters:


![](frontend_settings.jpg)


| Parameter | Description |
|---|---|
| Keyboard Input | Specifies whether keyboard input events should be transmitted from the client to the server. When enabled, keyboard events are sent to the runtime for processing. |
| Mouse Input | Specifies whether mouse input events should be transmitted from the client to the server. When enabled, mouse events are sent to the runtime for processing. > **Notice:** Mouse input is only available, when the *[Offscreen](../../../code/plugins/webstream/index.md#offscreen)* mode is enabled. |
| Max FPS | Specifies the frame rate of the video stream. |
| Min Bitrate (kbps) | Specifies the minimum target bitrate of the video stream. |
| Max Bitrate (kbps) | Specifies the maximum target bitrate of the video stream |
| Resolution | Specifies the target resolution of the video stream. The specified resolution is used when capturing and transmitting video frames. |
| Video Source | Defines the video source used for streaming. Allows selecting a specific player from the players available in the world. |
| Degradation Preference | Defines the preferred video quality degradation strategy under limited bandwidth conditions. It is used to choose between preserving image quality and maintaining playback smoothness. |


The *Information* tab provides the streaming statistics along with the following connection settings:


![](frontend_info.jpg)


| Parameter | Description |
|---|---|
| Preferred Transport | Allows selecting the preferred transport protocol used for media data transmission. If multiple options are available, the system will attempt to use the selected protocol. |
| Preferred Codec | Allows selecting the preferred video codec from the list of supported codecs. The selected codec will be used during video stream initialization if available. |
