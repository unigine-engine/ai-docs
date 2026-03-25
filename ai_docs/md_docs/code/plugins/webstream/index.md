# WebStream Plugin

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


> **Warning:** The functionality described in this article is experimental.

     Sorry, your browser does not support embedded videos.
The **WebStream** plugin allows broadcasting audio data and video frames rendered by a UNIGINE-based application to an unlimited number of devices via *WebRTC (Web Real-Time Communication)*.


![](web_streaming_plugin.png)


In general, the process is as follows:


1. You run the UNIGINE application on a remote computer, a desktop inside your organization, [a container](../../../deployment/index.md), or a virtual machine provided by a cloud hosting service.
2. UNIGINE uses the resources available to that computer (like CPU, GPU, memory, etc.) to run the application logic and render frames.
3. The rendered output is continuously encoded into a media stream and passed through a lightweight stack of web services.
4. Users view this stream in standard web browsers running on other computers and mobile devices and control the experience from their browsers, sending keyboard, mouse, and touch events, as well as custom events emitted from the client's web page, back to UNIGINE.


## Launching Plugin


To use the *WebStream* plugin with your project, do the following:


1. Add it via UNIGINE SDK Browser on the project creation: click *[Plugins](../../../sdk/projects/index_cpp.md#general_settings)*, check the *WebStream plugin* option, and click **Add**. > **Notice:** For the existing project, choose *[Other Actions -> Configure Project](../../../sdk/projects/index_cpp.md#update_config)*, add the plugin as described above, and click **Update Configuration**.
2. Launch the plugin: specify the `extern_plugin` command line option on the application start-up. ```text main_x64 -extern_plugin "UnigineWebStream" ``` Otherwise, you can load the plugin at runtime using the following console command: ```text plugin_load UnigineWebStream ```
3. In addition, you can enable the ***Offscreen*** mode by specifying the `-video_offscreen` command-line option. It will allow you to run the application in the headless mode without displaying a visible window. ```text main_x64 -extern_plugin "UnigineWebStream" -video_offscreen 1 ``` > **Notice:** - If you skip this parameter, the application window will be rendered alongside the video and input streams. However, in this case, inputs from remote clients may be processed incorrectly. > - For cases where [user input](../../../code/plugins/webstream/server.md#input_enabled) is not allowed in a remote client application, there is no need to enable *[Offscreen](#launch)* mode.


## Viewing Output


To render the output from the main viewport in a web browser, use the http address data specified in the [web configuration file](#web_config) in the address bar:


| Engine image: | Streamed image: |
|---|---|
| [![](engine_image.jpg)](engine_image.jpg) | [![](streaming_image.jpg)](streaming_image.jpg) |


The output is configured via the web browser UI. The description of parameters is available [here](../../../code/plugins/webstream/server.md#webstream_frontend_parameters).


## Web Configuration File


The configuration file `web_config.json` is located in the `%PROJECT_NAME%/data/plugins/Unigine/WebStream` directory. This file contains the following parameters:


| **Parameter** | **Description** |
|---|---|
| `signaling_server_adress` | The address of the signaling server to connect to. The connection is established via the WebSocket protocol, therefore the address must be specified in the **ws://** format. |
| `ice_servers` | A list of STUN/TURN servers used to establish a P2P connection when operating over the internet. These servers are typically not used in a local network. |
