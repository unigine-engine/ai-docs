# Sounds

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/cpp-api-samples](https://github.com/unigine-engine/cpp-api-samples)**.


This section contains expamples displaying how to implement the application logic.


## 3D Sound

This example demonstrates how to create a sound source (*[SoundSource](../../../api/library/sounds/class.soundsource_cpp.md)*) and configure its basic parameters: volume, pitch, looping mode, and playback type. The sound source features configurable spatial audio properties with adjustable minimum and maximum distance falloff, visualized in the scene.


UNIGINE allows you to work with sound sources just like with other nodes: they can be easily moved, rotated, or scaled. Additionally, they have specific characteristics detailed in the [related article](../../../api/library/sounds/class.soundsource_cpp.md).


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/sounds/3d_sound*
## Ambient Sound

This sample shows the implementation of a component that controls the playback of ambient sound (*[AmbientSource](../../../api/library/sounds/class.ambientsource_cpp.md)*) with interactive GUI controls using the *[AmbientSource](../../../api/library/sounds/class.ambientsource_cpp.md)* class. The component creates an ambient sound source that plays continuously in the background and provides real-time parameter adjustment through a dedicated interface.


The streaming mode can be toggled dynamically via the *Stream* checkbox, recreating the sound source to switch between preloaded audio (lower latency) and streamed audio (lower memory usage). This approach is ideal for background music, environmental sounds, and other continuous audio elements that enhance scene immersion.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/sounds/ambient_sound*
## FMOD Core

Before running this sample, follow the steps provided in the setup section or in the FMOD Integration Guide linked below.


This sample loads the *FMOD* plugin and initializes the *Core* system to demonstrate playback of both 2D and 3D sound instances, supporting up to 1024 simultaneous sound channels. You can switch between the 2D and 3D scenes to observe and interact with different sound behaviors.


Two sound modes are presented:


- **2D Music Playback**: Standard audio playback with support for volume adjustment and a distortion DSP effect
- **3D Music Playback**: Sound is emitted from a red sphere in 3D space, demonstrating positional audio in the environment. Move the camera to experience changes in sound direction and attenuation in real time.


**Use Cases:**


- Integrating FMOD Core into runtime environments for games or simulations
- Prototyping spatial sound design and 3D audio placement.


**Sample Requirements**


1. Download and install **FMOD Engine (version 2.03.08)** for your OS available on the official website (**[https://www.fmod.com/download](https://www.fmod.com/download)**).


2. Go to the FMOD installation folder and copy the following files to the `bin` folder of your project:


**for Windows:**


- `fmod.dll, fmodL.dll` from `/api/core/lib/x64/`
- `fsbank.dll, libfsbvorbis64.dll, opus.dll` from `/api/fbank/lib/x64/`.
- `fmodstudio.dll, fmodstudioL.dll` from `/api/studio/lib/x64/`


**for Linux**


- `libfmod.so.13, libfmodL.so.13` from `/api/core/lib/x64/`
- `libfsbank.so.13, libfsbankL.so.13, libfsbvorbis.so, libopus.so` from `/api/fbank/lib/x64/`
- `libfmodstudio.so.13, libfmodstudioL.so.13` from `/api/studio/lib/x64/`


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/sounds/fmod_core*
## FMOD Studio

Before running this sample, follow the steps provided in the setup section or in the FMOD Integration Guide linked below.


This sample demonstrates how to control, simulate, and visualize real-time audio events using the *FMOD Studio* plugin.


The setup includes a stationary object (car) and a moving object representing a source of Doppler-shifted sound, which can be toggled and adjusted via the *Doppler* tab of the GUI Parameters section. Additional sound settings such as wind, rain, the car engine RPM sound, and overall environmental volume can also be fine-tuned in real time under the *Ambience, Engine*, and *VCA* tabs.


**Use Cases:**


- Prototyping audio-driven game mechanics (e.g., vehicle audio, spatial ambiences, Doppler effects)
- Demonstrating dynamic audio parameters and movement-based effects like Doppler shifts.


**Sample Requirements**


1. Download and install **FMOD Engine (version 2.03.08)** for your OS available on the official website (**[https://www.fmod.com/download](https://www.fmod.com/download)**).


2. Go to the FMOD installation folder and copy the following files to the `bin` folder of your project:


**for Windows:**


- `fmod.dll, fmodL.dll` from `/api/core/lib/x64/`
- `fsbank.dll, libfsbvorbis64.dll, opus.dll` from `/api/fbank/lib/x64/`.
- `fmodstudio.dll, fmodstudioL.dll` from `/api/studio/lib/x64/`


**for Linux**


- `libfmod.so.13, libfmodL.so.13` from `/api/core/lib/x64/`
- `libfsbank.so.13, libfsbankL.so.13, libfsbvorbis.so, libopus.so` from `/api/fbank/lib/x64/`
- `libfmodstudio.so.13, libfmodstudioL.so.13` from `/api/studio/lib/x64/`


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/sounds/fmod_studio*
## Reverberation Zone

This sample demonstrates a *[Reverberation Zone](../../../objects/sounds/sound_reverb.md)* controller that uses the SoundReverb component to create configurable acoustic areas. These zones affect sound sources within their boundaries, simulating realistic environmental reverberation that adds depth and authenticity to audio experiences.


Adjust the *Gain* slider in the Parameters section to control various reverb properties, including density, decay time, and reflection gain.


Visual boundaries clearly delineate the affected areas, enabling precise spatial control over acoustic effects throughout the scene.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/sounds/reverberation_zone*
