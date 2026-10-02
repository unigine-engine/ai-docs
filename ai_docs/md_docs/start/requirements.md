# System Requirements


UNIGINE Engine runs on a broad range of hardware, from entry-level laptops to multi-GPU workstations. To be sure your configuration is suitable, check it against the requirements listed on this page.


## Hardware and OS


### Recommended


For developing in UnigineEditor and running projects of medium size and complexity.


|  | Windows | Linux |
|---|---|---|
| OS | Windows 11 Windows 10, version 22H2 (build 19045) | Linux with **kernel 4.18** or later and **GLIBC 2.28** or later, running **Xorg** or **XWayland**. Distributions: Debian 10+, Ubuntu 20.04 LTS+, Linux Mint 20+, Pop!_OS 20.04+, RHEL / Rocky Linux / AlmaLinux 8+, Fedora 30+, openSUSE Leap 15.3+, SLES 15 SP3+, current Arch Linux and Manjaro. |
| CPU | **6+ cores**, 3+ GHz - Intel Core i5/i7+ or AMD Ryzen 5/7+ |  |
| CPU architecture | x64 with **SSE4.2** |  |
| RAM | 16+ GB - dual-channel, with the **XMP** or **EXPO** profile enabled |  |
| GPU | **8+ GB VRAM** - NVIDIA GeForce RTX 3060, AMD Radeon RX 6600 XT or better |  |
| Graphics API | **DirectX 12** or **Vulkan 1.3** | **Vulkan 1.3** |
| Storage | 256+ GB free space on an SSD, depending on project content |  |


### Minimum


The minimum configuration - enough to run a final build with simplified graphics.


|  | Windows | Linux |
|---|---|---|
| OS | Windows 10, version 21H1 or later Earlier Windows 10 builds require a specific update for DirectX 12: version 20H2 - build 19042.804+ ([KB4601319](https://support.microsoft.com/en-us/topic/february-9-2021-kb4601319-os-builds-19041-804-and-19042-804-87fc8417-4a81-0ebb-5baa-40cfab2fbfde)) version 2004 - build 19041.804+ ([KB4601319](https://support.microsoft.com/en-us/topic/february-9-2021-kb4601319-os-builds-19041-804-and-19042-804-87fc8417-4a81-0ebb-5baa-40cfab2fbfde)) version 1909 - build 18363.1377+ ([KB4601315](https://support.microsoft.com/en-us/topic/february-9-2021-kb4601315-os-build-18363-1377-bdd71d2f-6729-e22a-3150-64324e4ab954)) | Linux with **kernel 4.18** or later and **GLIBC 2.28** or later, running **Xorg** or **XWayland** - see [Recommended](#development_specs) for the distribution list. |
| CPU | **4�6 cores**, 2.5+ GHz - Intel Core i3/i5+ or AMD Ryzen 3/5+ |  |
| CPU architecture | x64 with **SSE4.2** |  |
| RAM | 4+ GB |  |
| GPU | **2+ GB VRAM** - NVIDIA GeForce GTX 1650 or AMD Radeon RX 5500 |  |
| Graphics API | **DirectX 12** or **Vulkan 1.3** | **Vulkan 1.3** |
| Storage | 50+ GB free space on an SSD |  |


### High-End


For large-scale worlds and databases, simulators, and VR at high resolution and refresh rate.


|  | Windows | Linux |
|---|---|---|
| OS | Windows 11 | Linux with **kernel 4.18** or later and **GLIBC 2.28** or later, running **Xorg** or **XWayland** - see [Recommended](#development_specs) for the distribution list. |
| CPU | **12+ cores**, 3.5+ GHz - Intel Core i7/i9+ or AMD Ryzen 7/9+; Intel Xeon W or AMD Ryzen Threadripper PRO[*](#highend_cpu_note) |  |
| CPU architecture | x64 with **SSE4.2** |  |
| RAM | 64+ GB - dual-channel or more, with the **XMP** or **EXPO** profile enabled |  |
| GPU | **16+ GB VRAM** - NVIDIA GeForce RTX 4080+ or NVIDIA RTX PRO 4500+ |  |
| Graphics API | **DirectX 12** or **Vulkan 1.3** | **Vulkan 1.3** |
| Storage | 1+ TB free space on an NVMe SSD, depending on project content |  |


* Real-time rendering is bound by single-thread performance, so above 12 cores clock speed matters more than core count. **Xeon W** and **Threadripper PRO** give an advantage in other tasks: asset baking, project builds, preparing large data sets including terrain generation, and running several Engine instances on one machine - a multi-GPU setup driving several displays, for example.


See [Supported GPUs](#gpu) for the full list and known limitations.


## Development Software


Writing code for a UNIGINE project requires a minimum set of software; which set applies depends on the programming language you use. None of it is needed to start building scenes in UnigineEditor - it is ready to use as soon as the SDK is installed.


The listed IDEs are the ones used at UNIGINE; the list is not restrictive. The build is performed by the compiler and the build system, so any other modern IDE can be used instead, including AI-assisted editors and agentic coding tools.


### C++ Projects


|  | Windows | Linux |
|---|---|---|
| Runtime | [Microsoft Visual C++ Redistributable v14](https://aka.ms/vs/17/release/vc_redist.x64.exe) (for Visual Studio 2017�2026), x64 - required to run the Engine; **SDK Browser 2** offers to install it | Nothing beyond the [OS requirements](#hardware) |
| IDE | Visual Studio 2017+, Visual Studio Code or Qt Creator | Visual Studio Code or Qt Creator |
| Compiler | MSVC v141+ (ships with Visual Studio, also available separately) | GCC 8.3+ |
| Windows SDK | 8.1 or later; **10.0.19041.0** or newer recommended - the version the Engine itself is built and tested with | Not applicable |
| Build system | [CMake](https://cmake.org/download/) 3.21+ |  |
| Python | **Optional, rarely needed.** [Python](https://www.python.org/downloads/) 3.12+ is used by the ready-made `.py` project launchers, to fetch the [sample projects from GitHub](https://github.com/unigine-engine), and by the DataBridge Python API. The launchers additionally need **PyYAML** and **tkinter** (`python3-tk` on Linux). |  |


### C# Projects


|  | Windows | Linux |
|---|---|---|
| Runtime | [Microsoft Visual C++ Redistributable v14](https://aka.ms/vs/17/release/vc_redist.x64.exe) (for Visual Studio 2017�2026), x64 - required to run the Engine; **SDK Browser 2** offers to install it | Nothing beyond the [OS requirements](#hardware) |
| IDE | Visual Studio 2022 **17.8+**, Visual Studio Code or Rider | Visual Studio Code or Rider |
| C# SDK | [.NET SDK](https://dotnet.microsoft.com/en-us/download/dotnet/8.0) 8.0+ |  |
| Python | **Optional, rarely needed.** [Python](https://www.python.org/downloads/) 3.12+ is used by the ready-made `.py` project launchers, to fetch the [sample projects from GitHub](https://github.com/unigine-engine), and by the DataBridge Python API. The launchers additionally need **PyYAML** and **tkinter** (`python3-tk` on Linux). |  |


> **Notice:** **Windows**: the **SDK Browser 2** Installer offers to install **.NET 8.0+ SDK** and **Visual Studio Code** - the minimum needed for C# development.


### UnigineEditor Plugins


[UnigineEditor plugins](../editor2/extensions/index.md) are written in C++ only - C# API for editor extensions is not available. Everything from [C++ Projects](#cpp-tools) applies here as well, plus Qt.


|  | Windows | Linux |
|---|---|---|
| Language | Everything from [C++ Projects](#cpp-tools) |  |
| Framework | [Qt Framework](https://download.qt.io/archive/qt/) 6.5.3 - install exactly this version, newer releases are rejected by the build |  |


## Supported GPUs


The Engine runs on any graphics card that supports **DirectX 12** or **Vulkan 1.3**, whether it is listed here or not (with [Intel](#intel) as the exception). The lists below are provided for convenience, with every entry marked as one of:


- **(Recommended)** - current hardware, which we develop and test on. Choose from this group when purchasing new hardware.
- **No marker** - supported and working, but one or two generations older. Not recommended for new purchases.
- **(Legacy)** - **not recommended for use**. The vendor no longer ships new drivers for these cards, so problems that appear will not be fixed on the driver side, and we cannot guarantee reliable operation.


We strongly recommend using a single graphics card per machine, and always running the latest driver available for it:


|  | Windows | Linux |
|---|---|---|
| NVIDIA | Game Ready or Studio driver; RTX Enterprise for PRO cards | The official NVIDIA driver. Its **open kernel modules** are the default since R560 and the only option for Blackwell; the community **Nouveau**/**NVK** stack is not supported |
| AMD | Radeon Adrenalin; Radeon PRO Software for workstation cards | The **amdgpu** kernel driver with **Mesa** (RADV) for Vulkan |
| Intel (limited) | Intel Arc Graphics driver | Not supported - see [Intel](#intel) |


### NVIDIA


Supported NVIDIA GPUs:


**Desktop**


- **GeForce RTX 50 series** (Recommended): 5090, 5080, 5070 Ti, 5070, 5060 Ti, 5060, 5050
- **GeForce RTX 40 series** (Recommended): 4090, 4090 D, 4080 Super, 4080, 4070 Ti Super, 4070 Ti, 4070 Super, 4070, 4060 Ti, 4060
- **GeForce RTX 30 series** (Recommended): 3090 Ti, 3090, 3080 Ti, 3080, 3070 Ti, 3070, 3060 Ti, 3060, 3050
- **GeForce RTX 20 series**: Titan RTX, 2080 Ti, 2080 Super, 2080, 2070 Super, 2070, 2060 Super, 2060
- **GeForce GTX 16 series**: 1660 SUPER, 1660 Ti, 1660, 1650
- **Volta series** (Legacy): TITAN V
- **GeForce GTX 10 series** (Legacy): 1080 Ti, 1080, 1070 Ti, 1070, 1060
- **GeForce GTX 900 series** (Legacy): Titan X, 980 Ti, 980, 970, 960


**Mobile**


- **GeForce RTX 50 series** (Recommended): 5090, 5080, 5070 Ti, 5070, 5060, 5050
- **GeForce RTX 40 series** (Recommended): 4090, 4080, 4070, 4060, 4050
- **GeForce RTX 30 series** (Recommended): 3080 Ti, 3080, 3080 Max-Q, 3070 Ti, 3070, 3070 Max-Q, 3060, 3060 Max-Q, 3050 Ti, 3050
- **GeForce RTX 20 series**: 2080, 2080 Super, 2080 Max-Q, 2080 Super Max-Q, 2070, 2070 Super, 2070 Max-Q, 2070 Super Max-Q, 2060, 2060 Super, 2060 Max-Q, 2050
- **GeForce GTX 16 series**: 1660 Ti, 1660, 1660 Super, 1660 Ti Max-Q, 1650, 1650 Super, 1650 Max-Q, 1630
- **GeForce GTX 10 series** (Legacy): 1080, 1080 Max-Q, 1070, 1070 Max-Q, 1060, 1060 Max-Q, 1050 Ti, 1050 Ti Max-Q, 1050
- **GeForce GTX 900M series** (Legacy): 980, 980M, 970M


**PRO - Desktop**


- **Blackwell series** (Recommended): RTX PRO 6000, 5500, 5000, 4500, 4000, 2000
- **Ada Lovelace series** (Recommended): RTX 6000, 5000, 4500, 4000, 2000
- **Ampere series** (Recommended): RTX A6000, A5500, A5000, A4500, A4000, A2000, A1000, A400
- **Turing series**: Quadro RTX 8000, 6000, 5000, 4000, T1000, RTX T10-8
- **Volta series** (Legacy): Quadro GV100
- **Pascal series** (Legacy): Quadro GP100, P6000, P5000, P4000, P2000, P2200, P1000
- **Maxwell series** (Legacy): Quadro M6000, M5000, M4000, M2000, M1000M
- **Tesla series** (Legacy): DGX-2, DGX-1V, HGX-1, DGX Station, V100 PCIe, V100 PCIe 32GB, V100 SMX2, V100 SMX2 32GB, P40, DGX-1 (Pascal), P100 SMX2, P100 PCIe, P4, M40, M60, M6, M4, M10, V100, P100


**PRO - Mobile**


- **Blackwell series** (Recommended): RTX PRO 5000, 4000, 3000, 2000, 1000, 500
- **Ada Lovelace series** (Recommended): RTX 5000, 4000, 3500, 3000, 2000, 1000, 500
- **Ampere series** (Recommended): RTX A5500, A5000, A4500, A4000, A3000, A2000, A1000, A500
- **Turing series**: Quadro RTX 5000, RTX 4000, RTX 3000, T2000, T1200, T1000, T600, T500


> **Notice:** GPUs marked **Legacy** no longer receive new NVIDIA drivers. The 580 driver branch (October 2025) ended support for the **Maxwell** (GeForce GTX 900 series), **Pascal** (GeForce GTX 10 series) and **Volta** (TITAN V) architectures; they now get critical security fixes only. Such GPUs remain operational, but driver-side fixes and optimizations will no longer be released for them, and we cannot guarantee reliable operation. See NVIDIA's [list of legacy products](https://nvidia.custhelp.com/app/answers/detail/a_id/3473/~/eol-windows-driver-support-for-legacy-products) for Windows, and the [legacy driver timeframes](https://nvidia.custhelp.com/app/answers/detail/a_id/3142/~/support-timeframes-for-unix-legacy-gpu-releases) for Linux.


### AMD


Supported AMD Radeon GPUs:


**Desktop**


- **RX 9000 series** (Recommended): RX 9070 XT, RX 9070, RX 9070 GRE, RX 9060 XT, RX 9060
- **RX 7000 series** (Recommended): RX 7900 XTX, RX 7900 XT, RX 7800 XT, RX 7700 XT, RX 7700, RX 7600 XT, RX 7600
- **RX 6000 series**: RX 6950 XT, RX 6900 XT, RX 6800 XT, RX 6800, RX 6750 XT, RX 6700 XT, RX 6700, RX 6650 XT, RX 6600 XT, RX 6600, RX 6500 XT, RX 6400
- **RX 5000 series**: RX 5700 XT, RX 5700, RX 5600 XT, RX 5500 XT, RX 5500
- **RX Vega series** (Legacy): RX Vega 64, RX Vega 56, Radeon VII
- **RX 500 series** (Legacy): RX 590, RX 580, RX 570, RX 560, RX 550
- **RX 400 series** (Legacy): RX 480, RX 470, RX 460
- **RX 300 series** (Legacy): R9 Fury X, R9 Nano, R9 Fury, R9 390X, R9 390, R9 380X, R9 380, R9 370X, R9 370, R7 370
- **RX 200 series** (Legacy): R9 295 X2, R9 290X, R9 290, R9 285, R9 280X, R9 280, R9 270X, R9 270, R7 265, R7 260X, R7 260


**Mobile**


- **RX 7000 series** (Recommended): RX 7900M, RX 7800M, RX 7700S, RX 7600M XT, RX 7600M, RX 7600S
- **RX 6000 series**: RX 6850M XT, RX 6800M, RX 6700M, RX 6650M XT, RX 6800S, RX 6650M, RX 6600M, RX 6700S, RX 6600S, RX 6550M, RX 6500M, RX 6550S, RX 6450M, RX 6300M
- **RX 5000M series**: RX 5700M, RX 5600M, RX 5500M, RX 5300M
- **RX M600 series** (Legacy): 640, 630, 625, 620, 610
- **RX M500 series** (Legacy): RX 560X
- **RX M400 series** (Legacy): R9 M485X, RX 480M, RX 470M, R9 M470X
- **RX M300 series** (Legacy): R9 M395X, R9 M395, R9 M390X, R9 M390, R9 M385X, R9 M385, R9 M380, R9 M375X, R9 M375, R9 M370X
- **RX M200 series** (Legacy): R9 M295X, R9 M290X, R9 M280X, R9 M275X, R9 M270X, R9 M265X, R7 M265, R7 M260X, R7 M260


**PRO - Desktop**


- **Radeon AI PRO R9000 series** (Recommended): R9700, R9700S
- **Radeon PRO W7000 series** (Recommended): W7900, W7800, W7700, W7600, W7500
- **Radeon PRO W6000 series**: W6800, W6600, W6400
- **Radeon PRO W5000 series**: W5700, W5500
- **Radeon PRO V series**: PRO V710, PRO V620
- **Radeon PRO VII** (Legacy): Radeon PRO VII
- **Radeon PRO WX x200 series** (Legacy): WX 8200, WX 3200
- **Radeon PRO WX x100 series** (Legacy): WX 9100, WX 7100, WX 5100, WX 4100, WX 3100, WX 2100
- **Radeon PRO Series** (Legacy): PRO V340, Pro SSG, Vega Frontier Edition, Pro Duo (Fiji), Pro Duo (Polaris)


**PRO - Mobile**


- **Radeon PRO W6000 series**: W6600M
- **Radeon PRO W5000 series**: W5500M
- **Radeon PRO WX x200 series** (Legacy): WX 3200 Mobile
- **Radeon PRO WX x100 series** (Legacy): WX 7130, WX 7100, WX 4170, WX 4150, WX 4130, WX 3100, WX 2100


**APU**


- **Radeon 8000S** (Recommended): 8060S, 8050S, 8040S
- **Radeon 800M** (Recommended): 890M, 880M, 860M, 840M, 820M
- **Radeon 700M** (Recommended): 780M, 760M, 740M
- **Radeon 600M**: 680M, 660M
- **Radeon Vega** (Legacy): Vega 11, Vega 10, Vega 9, Vega 8, Vega 7, Vega 6, Vega 5


> **Notice:** In November 2025 AMD moved the **RX 5000** and **RX 6000** series (RDNA 1 and RDNA 2) to a driver branch separate from RDNA 3 and RDNA 4. They keep receiving game and stability updates, but less frequently. **Polaris** and **Vega** get bug fixes only, with no new features. For GPUs on AMD's [list of legacy products](https://www.amd.com/en/resources/support-articles/faqs/GPU-630.html) we cannot guarantee reliable operation.


### Intel


**Limited support** for Intel GPUs:


> **Warning:** - Many Intel Vulkan drivers currently lack support for multithreaded data transfer between CPU and GPU, which is required for the engine to function correctly. As a result, the **engine may not work properly on these systems when using Vulkan**. This is a driver limitation and it will be resolved once Intel updates their Vulkan drivers and adds the required support.
> - *Landscape Terrain* uses complex shaders that rely on double-precision floating-point calculations. Many **Intel GPUs (particularly on Windows) do not support double-precision math** in shaders under DirectX 12. As a result, terrain rendering may behave incorrectly or not function as expected on these systems.


**Intel Discrete GPU:**


- **Intel Arc B-Series**: B580, B570
- **Intel Arc A-Series** (Desktop): A770, A750, A580, A380, A310
- **Intel Arc A-Series** (Mobile): A770M, A730M, A570M, A550M, A530M, A370M, A350M
- **Intel Arc Pro B-Series**: B60, B50
- **Intel Arc Pro A-Series**: A60, A50, A40, A60M, A30M


**Intel CPU with Integrated Graphics:**


- **Intel Core Ultra Series 3** - *Intel Arc Graphics B390, B370* or *Intel Graphics* (Xe3)
- **Intel Core Ultra Series 2** - *Intel Arc Graphics 140V, 130V, 140T* or *Intel Graphics* (Xe2)
- **Intel Core Ultra Series 1** - *Intel Arc Graphics* or *Intel Graphics* (Xe-LPG)
- **Intel Core 12th�14th gen** (Legacy) - *Iris Xe Graphics*, *UHD Graphics 770, 730*
- **Intel Core 11th gen** (Legacy) - *Iris Xe Graphics*, *UHD Graphics 750*


**Intel Data Center GPU:**


- **Intel Data Center GPU Flex Series**: 170V, 170, 140


> **Notice:** The operating configuration for Intel GPUs is **DirectX + Windows**; we cannot guarantee reliable operation for other configurations. Entries marked (Legacy) are 11th�14th Gen processor graphics, which Intel has moved to a [legacy driver branch](https://www.intel.com/content/www/us/en/support/articles/000101986/graphics.html).


## Supported Devices


### Displays and Output


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


### Input


**Keyboard, mouse and touch**


- PC keyboard
- PC mouse
- Multi-touch screen


**Game controllers**


- Xbox 360 and Xbox One controllers, and XInput-compatible gamepads
- DualShock 3 / DualShock 4 / DualSense controllers, including the touchpad (multi-finger, with pressure), the light bar, the accelerometer and the gyroscope
- Analog triggers and dual-frequency vibration


**Joysticks and specialized controllers**


- Sim racing steering wheels and throttles
- Flight sticks
- Arcade sticks
- Dance pads, guitars and drum kits


**VR controllers and trackers**


- Controllers of the [supported headsets](#output) - 6DoF position and rotation, axes, buttons and haptic feedback
- Standalone trackers, for tracking bodies and props
- Base stations


**External tracking systems** - available via plugins:


- [ART](../code/plugins/arttrack/index.md) (Advanced Realtime Tracking) optical tracking systems
- [VRPN](../code/plugins/vrpn/index_cpp.md)-compatible trackers, buttons and analog devices
- [Ultraleap](../code/plugins/ultraleap/index_cpp.md) hand tracking


Devices with **force feedback** are supported - steering wheels and flight sticks in particular. Eleven effect types are available: constant and ramp forces; sine, square, triangle and sawtooth (up and down) waveforms; and spring, friction, damper and inertia conditions. An application can query each effect before using it.


### Audio


All sound devices supported by *[OpenAL](https://github.com/kcat/openal-soft)* library (virtually any standard sound device).
