# FMOD Plugin


The **FMOD** plugin provides integration with [FMOD](https://www.fmod.com/) library developed by Firelight Technologies. FMOD is a powerful solution that includes all the tools you need to add sound and music to video games and applications.


> **Notice:** FMOD Plugin is compatible with the FMOD version **2.03.08** (earlier FMOD versions are not supported in this version of UNIGINE SDK).
> Supported OS: **Windows x64** and **Linux**.


### See also


- *[FMOD plugin](../../../api/library/plugins/fmod/index.md)* classes
- C++ samples:

  -
  -
- C# Component samples:

  -
  -


## Installing FMOD


To be able to use this plugin:


- Download the [FMOD Engine installer](https://www.fmod.com/download) available on the official website (in the *FMOD Studio Suite* section). ![](fmod_download.png)
- Install the engine.
- Go to the FMOD installation folder and copy the following **DLL**'s to the `bin` folder of your project:

  - **fmod.dll**, **fmodL.dll** from */api/core/lib/x64/*
  - **fmodstudio.dll**, **fmodstudioL.dll** from */api/studio/lib/x64/*


## Launching FMOD Plugin


To use *FMOD Plugin*, specify the `extern_plugin` command line option on the application start-up:


```bash
main_x64 -extern_plugin "UnigineFMOD"
```
