# System Requirements


## Software


To develop and run applications using UNIGINE 2 SDK, any of the following operating systems should be used:


- Windows (10/11) x64, the minimum required: Version 2004, Codename 20H1, Name: May 2020 Update, Build 19041.804
- Linux (kernel 4.19+) x64


### Additional Software for Development


To develop your project, see the requirements below.


##### Windows


- **Runtime** > **Notice:** The Redistributable packages are bundled with the SDK.

  - **Microsoft Visual C++ Redistributable** for *Visual Studio 2015, 2017, 2019*, and *2022*: [x64](https://aka.ms/vs/17/release/vc_redist.x64.exe) - required to run the Engine.
- **Development**

  - **C++ Development Requirements:**

    - **IDE**: Any preferred IDE. Recommended: **Microsoft Visual Studio 2015+**, **Visual Studio Code** or **Qt Creator** (mostly used for Qt framework development, but also suitable for regular C++ projects)
    - **Toolset / Build Tools**:

      - **MSVC v140+** (available with Visual Studio, but can be [downloaded separately](https://www.microsoft.com/en-us/download/details.aspx?id=48159)).
      - **CMake 3.21+** (can be [downloaded for free](http://www.cmake.org/)).
      - **Python 3.10** (can be [downloaded for free](http://www.python.org/)) - used by launchers.
  - **C# Development Requirements:** > **Notice:** The **SDK Browser 2** Installer will automatically prompt to install **.NET 8.0 SDK** and **Visual Studio Code**, which are the minimum required tools for C# development.

    - **IDE**: Any preferred IDE. Recommended: **Microsoft Visual Studio 2022**, **Visual Studio Code** or **Rider**
    - **Toolset / Build Tools**:

      - **.NET SDK 8.0** (can be [downloaded for free](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)).
      - **Python 3.10** (can be [downloaded for free](http://www.python.org/)) - used by launchers.


##### Linux


- **Runtime:**

  - **GLIBC 2.28** - required to run the Engine.
- **Development:**

  - **C++ Development Requirements:**

    - **IDE**: Any preferred IDE. Recommended: **Visual Studio Code** or **Qt Creator** (mostly used for Qt framework development, but also suitable for regular C++ projects)
    - **Toolset / Build Tools**:

      - **GCC 8.3+** - a C++ compiler.
      - **CMake 3.21+** (can be [downloaded for free](http://www.cmake.org/)).
      - **Python 3.10** (can be [downloaded for free](http://www.python.org/)) - used by launchers.
  - **C# Development Requirements:**

    - **IDE**: Any preferred IDE. Recommended: **Visual Studio Code** or **Rider**
    - **Toolset / Build Tools**:

      - **.NET SDK 8.0** (can be [downloaded for free](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)).
      - **Python 3.10** (can be [downloaded for free](http://www.python.org/)) - used by launchers.


To develop [plugins for UnigineEditor](../editor2/extensions/index.md), you'll need the following as well:


- **Qt Framework version 6.5.3** ([download](https://download.qt.io/archive/qt/) the required version and install it).


## Hardware Specifications


### Minimum Requirements


Minimum implies that the engine will start and run a project with simplified visuals. However for developing and running **complex projects**, we advise to consider the [recommended configuration](#development_specs) below.


| CPU: | x64 processors with SSE4.2 support starting with quad-core Intel or AMD with 2.5+ GHz frequency. |
|---|---|
| RAM: | 4 GB or more. |
| Storage: | At least 50 GB free space. It is recommended to use an **SSD storage** device for best performance. |
| GPU: | [Graphics cards](#gpu) with support for DirectX 12 or Vulkan. |
| VRAM: | 2 GB or more. |


### Recommended Configuration


This section represents an average configuration that is deemed acceptable at UNIGINE for convenient development of medium-size projects.


| CPU: | Intel i5/i7/i9 with **6+ cores** or AMD Ryzen 5/7 series, 3+ GHz |
|---|---|
| RAM: | 32 GB or more |
| Storage: | 256 GB or more (depending on the content) It is recommended to use an **SSD storage** device for best performance. |
| GPU: | At least, NVIDIA GeForce RTX 3060 or similar |
| VRAM: | 8 GB or more |


## GPU


We strongly recommend using one graphic card in PC.


> **Notice:** - Even if UNIGINE cannot recognize a graphics card, it still can detect the card's capabilities and use available features.
> - For optimal experience it is **strongly recommended to use up-to-date video drivers**.


### NVIDIA


Supported NVIDIA GPUs:


**Desktop**


- **GeForce RTX 50 series** (Recommended): 5090, 5080, 5070 Ti, 5070, 5060 Ti, 5060, 5050
- **GeForce RTX 40 series** (Recommended): 4090, 4090 D, 4080, 4070 Ti Super, 4070 Ti, 4070 Ti Super, 4070 Ti, 4070 Super, 4070, 4060 Ti, 4060
- **GeForce RTX 30 series** (Recommended): 3090 Ti, 3090, 3080 Ti, 3080, 3070 Ti, 3070, 3060 Ti, 3060, 3050
- **GeForce RTX 20 series** (Recommended): Titan RTX, 2080 Ti, 2080 Super, 2080, 2070 Super, 2070, 2060 Super, 2060
- **GeForce GTX 16 series** (Recommended): 1660 SUPER, 1660 Ti, 1660, 1650
- **Volta series** (Recommended): TITAN V
- **GeForce GTX 10 series**: 1080 Ti, 1080, 1070 Ti, 1070; Limited: 1060
- **GeForce GTX 900 series** (Limited): Titan X, 980 Ti, 980, 970, 960


**Mobile / Laptop**


- **GeForce RTX 50 series** (Recommended): 5090, 5080, 5080 Ti, 5070, 5070 Ti, 5060, 5050
- **GeForce RTX 40 series** (Recommended): 4090, 4080, 4080 Super, 4070 Ti, 4070 Ti Super, 4070 Super, 4070, 4060 Ti, 4060, 4050
- **GeForce RTX 30 series** (Recommended): 3090, 3090 Ti, 3080, 3080 Ti, 3080 Max-Q, 3070 Ti, 3070, 3070 Max-Q, 3060 Ti, 3060, 3060 Max-Q, 3050, 3050 Ti
- **GeForce RTX 20 series** (Recommended): 2080, 2080 Super, 2080 Max-Q, 2080 Super Max-Q, 2070, 2070 Super, 2070 Max-Q, 2070 Super Max-Q, 2060, 2060 Super, 2060 Max-Q, 2050
- **GeForce GTX 16 series** (Recommended): 1660 Ti, 1660, 1660 Super, 1660 Ti Max-Q, 1650, 1650 Super, 1650 Max-Q, 1630
- **GeForce GTX 10 series**: 1080, 1080 Max-Q, 1070, 1070 Max-Q, 1060; Limited: 1060 Max-Q, 1050 Ti, 1050 Ti Max-Q, 1050
- **GeForce GTX 900M series** (Limited): 980, 980M, 970M


**PRO**


- **Maxwell series**: Quadro M6000, M5000, M4000, M2000, M1000M
- **Pascal series**: Quadro GP100, P6000, P5000, P4000, P2000, P2200, P1000
- **Volta series**: Quadro GV100
- **Turing series**: Quadro RTX 8000, 6000, 5000, 4000, T1000
- **Ampere series**: RTX A6000, A5500, A5000, A4500, A4000, A2000
- **Ada Lovelace series**: RTX 6000, 5000, 4500, 4000, 2000, A1000
- **Blackwell series**: RTX PRO 6000, 5000, 4500, 2000
- **Tesla series**: RTX T10-8, DGX-2, DGX-1V, HGX-1, DGX Station, V100 PCIe, V100 PCIe 32GB, V100 SMX2, V100 SMX2 32GB, P40, DGX-1 (Pascal), P100 SMX2, P100 PCIe, P4, M40, M60, M6, M4, M10, V100, P100


If your NVIDIA GPU is in the [list of legacy products](http://nvidia.custhelp.com/app/answers/detail/a_id/3473/~/eol-windows-driver-support-for-legacy-products), we cannot guarantee its reliable operation.


### AMD


Supported AMD Radeon GPUs (OEM versions not listed):


**Desktop**


- **RX 9000 series** (Recommended): RX 9070 XT, RX 9070, RX 9060 XT, RX 9060
- **RX 7000 series** (Recommended): RX 7900 XTX, RX 7900 XT, RX 7800 XT, RX 7700 XT, RX7700, RX 7600 XT, RX 7600
- **RX 6000 series** (Recommended): RX 6950 XT, RX 6900 XT, RX 6800 XT, RX 6800, RX 6750 XT, RX 6700 XT, RX 6700, RX 6650 XT, RX 6600 XT, RX 6600, RX 6500 XT, RX 6400
- **RX 5000 series** (Recommended): RX 5700 XT, RX 5700, RX 5600 XT, RX 5500 XT, RX 5500
- **RX Vega series** (Recommended): RX Vega 64, RX Vega 56, Radeon VII
- **RX 500 series** (Limited): RX 590, RX 580, RX 570, RX 560, RX 550
- **RX 400 series** (Limited): RX 480, RX 470, RX 460
- **RX 300 series** (Limited): R9 Fury X, R9 Nano, R9 Fury, R9 390X, R9 390, R9 380X, R9 380, R9 370X, R9 370, R7 370
- **RX 200 series** (Limited): R9 295 X2, R9 290X, R9 290, R9 285, R9 280X, R9 280, R9 270X, R9 270, R7 265, R7 260X, R7 260


**Mobile**


- **RX 7000 series** (Recommended): RX 7900M, RX 7800M, RX 7700S, RX 7600M XT, RX 7600M, RX 7600S
- **RX 6000 series** (Recommended): RX 6850M XT, RX 6800M, RX 6700M, RX 6650M XT, RX 6800S, RX 6650M, RX 6600M, RX 6700S, RX 6600S, RX 6550M, RX 6500M, RX 6550S, RX 6450M, RX 6300M
- **RX 5000M series**:RX 5700M, RX 5600M, RX 5500M, RX 5300M
- **RX M600 series**: 640; Limited: 630, 625, 620, 610
- **RX M500 series** (Limited): RX 560X
- **RX M400 series** (Limited): R9 M485X, RX 480M, RX 470M, R9 M470X
- **RX M300 series** (Limited): R9 M395X, R9 M395, R9 M390X, R9 M390, R9 M385X, R9 M385, R9 M380, R9 M375X, R9 M375, R9 M370X
- **RX M200 series** (Limited): R9 M295X, R9 M290X, R9 M280X, R9 M275X, R9 M270X, R9 M265X, R7 M265, R7 M260X, R7 M260


**Radeon Pro (Workstation and Mobile)**


- **Pro R9000 series**: R9700
- **Pro W7000 series**: W7900, W7800, W7700, W7600, W7500
- **Pro W6000 series**: W6800, W6600, W6400, W6600M
- **Radeon PRO VII Series**: Radeon PRO VII
- **W5000 series**: W5700, W5500, W5500M
- **WX x200 series**: WX 8200, WX 3200, WX 3200 Mobile
- **WX x100 series**: WX 9100, WX 7100, WX 5100, WX 4100, WX 3100, WX 2100
- **WX x100 series (Mobile)**: WX 7130, WX 7100, WX 4170, WX 4150, WX 4130, WX 3100, WX 2100
- **Pro V series**: PRO V710, PRO V620, PRO V340
- **Pro Series**Pro SSG, Vega Frontier Edition, Pro Duo (Fiji), Pro Duo (Polaris)


**APU**


- **Radeon Vega**: Vega 11, Vega 10, Vega 9, Vega 8, Vega 7, Vega 6, Vega 5
- **Radeon 700M**: 780M, 760M, 740M
- **Radeon 600M**: 680M, 660M


If your AMD GPU is in the [list of legacy products](https://www.amd.com/en/resources/support-articles/faqs/GPU-630.html), we cannot guarantee its reliable operation.


### Intel


> **Warning:** - Many Intel Vulkan drivers currently lack support for multithreaded data transfer between CPU and GPU, which is required for the engine to function correctly. As a result, the **engine may not work properly on these systems when using Vulkan**. This is a driver limitation and it will be resolved once Intel updates their Vulkan drivers and adds the required support.
> - *Landscape Terrain* uses complex shaders that rely on double-precision floating-point calculations. Many **Intel GPUs (particularly on Windows) do not support double-precision math** in shaders under DirectX 12. As a result, terrain rendering may behave incorrectly or not function as expected on these systems.


**Intel CPU with Integrated Graphics:**


- **Intel Core Ultra Series 2** with *Intel Graphics* / *Intel Arc graphics*
- **Intel Core Ultra Series 1** with *Intel Graphics* / *Intel Arc graphics*
- **Intel Core 14th gen** with UHD 770 / UHD 730
- **Intel Core 13th gen** with UHD 770 / UHD 730
- **Intel Core 12th gen** with UHD 770 / UHD 730
- **Intel Core 11th gen** with UHD 750


> **Warning:** When using Intel CPUs 11th-14th Gen with integrated graphics, the Engine **supports DirectX 12 only**.


**Intel Discrete GPU:**


- **Intel Arc A-Series**: A770, A750, A750E, A770M, A580E, A580, A730M, A570M, A550M, A530M, A380E, A380, A370E, A370M, A310E, A310, A350E, A350M
- **Intel Arc B-Series**: B580, B570
- **Intel Arc Pro A-Series**: A60, A60M, A30M, A50, A40
- **Intel Arc Pro B-Series**: B60, B50


**Intel Data Center GPU:**


- **Intel Data Center GPU Max Series**: 1550, 1100
- **Intel Data Center GPU Flex Series**: 170V, 170, 140


> **Notice:** The operating configuration for Intel GPUs is DirectX + Windows; we cannot guarantee reliable operation for other configurations.


If your Intel GPU is in the [list of legacy products](https://www.intel.com/content/www/us/en/support/articles/000005526/graphics.html), we cannot guarantee its reliable operation.


## Output Devices


- Standard monitors
- VR headsets:

  - Oculus Rift / Rift S / Quest / Quest 2 / Quest 3 / Quest 3S (with Oculus Link cable / Oculus Link wireless)
  - HTC Vive / Vive Pro / Focus / Cosmos / Flow / XR Elite
  - Varjo VR-2 / VR-2 Pro (with eye tracking) / VR-3 / XR-3 (with extended mixed reality support) / XR-4
  - Windows Mixed Reality (WMR)-compatible
  - OpenVR-compatible
  - OpenXR-compatible
- Stereo system (anaglyph, side-by-side, interlaced, separate images)
- Multi-monitor systems (monitor walls, projectors, NVIDIA Surround, etc.)
- Multi-channel (network cluster)


## Input Devices


- PC keyboard
- PC mouse
- PC joystick
- Sim racing steering wheel
- XBox-compatible gamepad controller
- DualSense/DualShock controller
- Multi-touch screen


## Sound Cards


All sound devices supported by *[OpenAL](https://github.com/kcat/openal-soft)* library (virtually any standard sound device).
