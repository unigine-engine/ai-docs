# VideoTexture

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


The *VideoTexture* plugin implements hardware decoding of low-latency video streams from online sources in the UNIGINE application (UNIGINE Sim SDK edition).


The plugin allows streaming video from VP9-encoded online RTSP/RTP sources to a UNIGINE texture (sound data is ignored). This texture can be used in any material and applied to various objects in the scene (e.g. to output video to a background TV-panel in a virtual studio or create a multi-camera surveillance system).


This is not a generic solution for in-app video decoding and has a limited scope of applications.


The plugin package also contains a sample scene with textures to which the video can be streamed and a guide on how to start your own stream for quick testing.


![](index.png)


Requirements:


- OS: Windows 10+
- DirectX11 GAPI (NVidia RTX 2080+)
- Source Code: C++
- VP9-encoded online RTSP/RTP sources


## Running the Sample


To run the sample:


- Download the *UnigineVideoTexture* plugin from [Add-On Store](https://store.unigine.com/).
- Add the downloaded add-on (UPACKAGE file) to your project by dragging it into the project `data/` folder in the Asset Browser. In the *Import Package* window that opens, click the *Import Package* button and wait until the add-on contents are imported.
- Open the `%PROJECT_NAME%/source/plugins/Unigine/VideoTexture/stream_cfg.json` file and change URL addresses to your own. If you don�t have any streaming source to use in the sample, run a sample stream as described in the `%PROJECT_NAME%/docs/UnigineVideoTexture/example_streaming_server_mediamtx/readme.md` file.
- Run the sample using the corresponding `*.bat` file available in the sample folder:

  - `%PROJECT_NAME%\source\plugins\Unigine\VideoTexture\run_sample.bat` � for the float precision C++ project
  - `%PROJECT_NAME%\source\plugins\Unigine\VideoTexture\run_sample_double.bat` � for the double precision C++ project


## Using Plugin in Your Application


To use the plugin in your own application:


- Import the package to your project.
- Check the plugin API is available in `%PROJECT_NAME%\source\plugins\Unigine\VideoTexture\Interface.h`.
- Use the sample implementation available in the `%PROJECT_NAME%\source\plugins\Unigine\VideoTexture\sample\VideoTextureSample.cpp` file for reference.
