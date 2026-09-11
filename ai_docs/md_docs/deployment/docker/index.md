# Docker Container Configuration


This article describes the **[Docker](https://www.docker.com/)** container configuration process for [RHEL](#running_rhel)- and [Debian](#running_debian)-based Linux distributions. *Docker* allows you to develop and run your UNIGINE-based application in isolated environments inside a container. To complete all steps described in this guide, your system must run Linux and be equipped with an **NVIDIA** graphic card.


To work with other distributions, such as Amazon, openSUSE, Debian, or CentOS, refer to the [NVIDIA Container Toolkit documentation](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker).


## System Requirements


To ensure correct audio playback, close all applications that are using sound devices. The **[ALSA](https://www.alsa-project.org/wiki/Download)** driver must be installed on the system to play the sound correctly.


> **Notice:** The *Docker* daemon binds to a Unix socket rather than a TCP port. By default, the Unix socket is owned by the **root** user, and other users can access it only via **sudo** ([read more](https://docs.docker.com/engine/install/ubuntu/)). The *Docker* daemon always runs as the root user.
>
>
> If you don't want to prefix Docker commands with **sudo**, create a Unix group called `docker` and add users to it ([read more](https://docs.docker.com/engine/install/linux-postinstall/)). When the *Docker* daemon starts, it creates a Unix socket accessible to members of the `docker` group.


## Docker Configuration for RHEL Linux


To run your UNIGINE-based application inside a container, we recommend one of the following:


- Use a pre-built Vulkan image from NVIDIA based on Rocky Linux 8.
- Download a UNIGINE image based on Rocky Linux 8 + Vulkan.
- Build a Docker image according to the instructions below.


> **Notice:** It is impossible to run a UNIGINE application on the **Red OS UBI 8** system, since the stripped-down UBI image does not support Vulkan (vulkan-loader, mesa-vulkan-drivers) and is not designed for the GPU stack. To resolve this limitation, use a full-fledged **Red OS** / **RHEL** system or a RHEL-compatible distribution such as **Rocky Linux 8** / **AlmaLinux 8**.


To configure **Docker**, perform the following steps:


1. Install the NVIDIA driver on the host computer. The NVIDIA driver is installed **only on the host**, not inside the container. GPU access and information can be verified using the **`nvidia-smi`** command.
2. [Install the NVIDIA Container Toolkit](#nvidia_installation_rhel).
3. [Assemble the *Docker* container image](#image_preparation_rhel).
4. [Run the *Docker* container in test mode](#test_launch_rhel).


### NVIDIA Container Toolkit Installation


1. Install the **NVIDIA Container Toolkit**: ```bash sudo dnf install -y nvidia-container-toolkit ``` > **Notice:** If you require a different version of the NVIDIA Container Toolkit, follow the [official installation instructions](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#with-dnf-rhel-centos-fedora-amazon-linux).
2. Configure the container runtime using the **`nvidia-ctk`** command, which modifies the `/etc/docker/daemon.json` file on the host: ```bash sudo nvidia-ctk runtime configure --runtime=docker ```
3. Restart the Docker Daemon: ```bash sudo systemctl restart docker ```
4. Verify that Docker detects the NVIDIA runtime: ```bash docker info | grep -i runtime ``` ```text Runtimes: runc nvidia ``` If the Docker doesn't detect the runtime, register it manually: ```bash sudo nvidia-ctk runtime configure --runtime=docker sudo systemctl restart docker ```
5. To run graphical applications inside the Docker container, allow access to X11 forwarding: ```bash xhost +local:docker ```


### Preparing the Container Image


If you do not want to use a container image from *Docker Hub* and prefer to **assemble your own image** with vulkan-loader and X11 support, follow the instructions in the spoiler below:


<details>
<summary>Manual Image Preparation and Assembly | Close</summary>

1. Create a folder to work with the container: ```bash $ mkdir ~/unigine-in-docker ```
2. Create a `Dockerfile` text file inside the `unigine-in-docker` folder: ```bash $ cd ~/unigine-in-docker $ touch Dockerfile ```
3. Add the following lines to the `Dockerfile` file and save it: > **Notice:** The Dockerfile below contains a complete list of dependencies required to work with the UNIGINE Engine and Editor, as well as to run C++ and C# applications. You may select only the dependencies you need and omit any unnecessary ones. The Dockerfile is based on an [NVIDIA Docker](https://hub.docker.com/r/nvidia/cuda/tags). ```bash FROM rockylinux:8 # You can use nvidia/cuda:12.3.2-runtime-rockylinux8 if CUDA support is required # Install Vulkan-loader and X11 libraries RUN dnf -y update # 1. Runtime dependencies (required to run a UNIGINE-based application) RUN dnf -y install \ vulkan-loader \ vulkan-tools \ libX11 \ libXcursor \ libXrandr \ libXinerama \ libXdamage \ libXfixes # 2. Editor Qt6 dependencies (required for UNIGINE Editor, BuildTool, runtime generation, and cache) RUN dnf install -y epel-release RUN dnf install -y \ mesa-libEGL \ mesa-libGL \ libglvnd-opengl \ libxkbcommon \ libxkbcommon-x11 \ xcb-util \ xcb-util-keysyms \ xcb-util-wm \ xcb-util-cursor \ fontconfig \ freetype # 3. C++ development (required to build C++ applications in Docker) RUN dnf -y install \ gcc \ gcc-c++ \ glibc-devel \ libstdc++-devel \ make \ cmake \ gdb \ git # 4. C# development install .NET 8 (required to build C# applications in Docker) RUN wget -O dotnet.tar.gz https://builds.dotnet.microsoft.com/dotnet/Sdk/8.0.417/dotnet-sdk-8.0.417-linux-x64.tar.gz && \ mkdir /usr/local/etc/dotnet-sdk-8.0 && \ tar -xzf dotnet.tar.gz -C /usr/local/etc/dotnet-sdk-8.0 && \ rm -rf /usr/bin/dotnet && \ ln -s /usr/local/etc/dotnet-sdk-8.0/dotnet /usr/bin/dotnet && \ rm -rf dotnet.tar.gz # sound RUN dnf install -y alsa-lib alsa-utils RUN ldconfig && dnf clean all ```
4. Assemble the Docker image (inside the `unigine-in-docker` folder): ```bash Docker build �tag your_image_name . ```

</details>


### Docker Test Run


1. Run the Docker image: ```bash docker run --rm \ --gpus all \ --device /dev/snd  --group-add audio \ -e DISPLAY=$DISPLAY \ -e NVIDIA_DRIVER_CAPABILITIES=graphics,compute,utility \ -e VK_ICD_FILENAMES=/usr/share/vulkan/icd.d/nvidia_icd.json \ -v /usr/share/vulkan/icd.d/nvidia_icd.json:/usr/share/vulkan/icd.d/nvidia_icd.json:ro \ -v /tmp/.X11-unix:/tmp/.X11-unix \ your_image_name ``` > **Notice:** The path to the `nvidia_icd.json` file on the host may differ (for example, `/usr/lib/x86_64-linux-gnu/vulkan/icd.d/nvidia_icd.json`).
2. To verify the selected GPU drivers, run: **`vulkaninfo`**. This command displays the detailed GPU device information. To display only the GPU model name, use: **`vulkaninfo | grep GPU`**.


## Docker Configuration for Debian-based Linux


To run your UNIGINE-based application inside a container, we recommend one of the following:


- Use a pre-built Vulkan image from NVIDIA based on Ubuntu 20.04.
- Download a UNIGINE image based on Ubuntu 20.04 + Vulkan.
- Build a Docker image according to the instructions below.


To configure **Docker**, perform the following steps:


1. Install the NVIDIA driver on the host computer. The NVIDIA driver is installed **only on the host**, not inside the container. GPU access and information can be verified using the **`nvidia-smi`** command.
2. [Install the NVIDIA Container Toolkit](#nvidia_installation_rhel).
3. [Assemble the *Docker* container image](#image_preparation_rhel).
4. [Run the *Docker* container in test mode](#test_launch_rhel).


### NVIDIA Container Toolkit Installation


1. Install the **NVIDIA Container Toolkit**: ```bash sudo apt-get install -y nvidia-container-toolkit ``` > **Notice:** If you need a different version of the NVIDIA Container Toolkit, follow the [official installation instructions](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#with-apt-ubuntu-debian).
2. Configure the container runtime using **`nvidia-ctk`** command, which modifies the `/etc/docker/daemon.json` file on the host: ```bash sudo nvidia-ctk runtime configure --runtime=docker ```
3. Restart the Docker Daemon: ```bash sudo systemctl restart docker ```
4. Verify that Docker detects the NVIDIA runtime: ```bash docker info | grep -i runtime ``` ```text Runtimes: runc nvidia ``` If Docker does not detect the runtime, register it manually: ```bash sudo nvidia-ctk runtime configure --runtime=docker sudo systemctl restart docker ```
5. To run graphical applications inside a Docker container, allow the container access to X11 forwarding: ```bash xhost +local:docker ```


### Preparing Container Image


There is a ready-to-use container image that we have prepared for you on the *Docker Hub* - check out the link **[run-unigine-in-docker](https://hub.docker.com/r/unigine/run-unigine-in-docker)** and use the following command:


```bash
docker pull unigine/run-unigine-in-docker
```


If you do not want to use a container image from *Docker Hub* and prefer to **assemble your own image** with vulkan-loader and X11 support, follow the instructions in the spoiler below:


<details>
<summary>Manual Image Preparation and Assembly | Close</summary>

1. Create a folder to work with the container: ```bash $ mkdir ~/unigine-in-docker ```
2. Create a `Dockerfile` text file inside the `unigine-in-docker` folder: ```bash $ cd ~/unigine-in-docker $ touch Dockerfile ```
3. Add the following lines to the `Dockerfile` file and save it: > **Notice:** The Dockerfile below contains a complete list of dependencies required to work with the UNIGINE Engine and Editor, as well as to run C++ and C# applications. You may select only the dependencies you need and omit any unnecessary ones. The Dockerfile is based on an [NVIDIA Docker with Vulkan 1.3](https://hub.docker.com/r/nvidia/vulkan/tags). ```bash FROM nvidia/vulkan:1.3-470 ENV DEBIAN_FRONTEND=noninteractive # (optional) Remove problematic CUDA/NVIDIA APT lists to prevent apt-get update GPG errors RUN rm -f /etc/apt/sources.list.d/cuda*.list \ /etc/apt/sources.list.d/nvidia*.list \ /etc/apt/sources.list.d/*cuda*.sources \ /etc/apt/sources.list.d/*nvidia*.sources || true # 1. Runtime dependencies (required to run a UNIGINE-based application) RUN apt-get update && apt-get install -y --no-install-recommends \ ca-certificates \ libx11-dev \ libxrandr-dev \ libxinerama-dev \ libxcursor-dev \ libxi-dev \ libxext-dev \ libxrender-dev \ libxfixes-dev \ xauth \ && rm -rf /var/lib/apt/lists/* # Fresh cmake (newer than the repository version) RUN apt-get update && apt-get install -y --no-install-recommends \ python3 python3-pip \ && pip3 install --no-cache-dir -U cmake \ && cmake --version \ && rm -rf /var/lib/apt/lists/* # 2. Editor Qt6 dependencies (required for UNIGINE Editor, BuildTool, runtime generation, and cache) RUN apt-get update && apt-get install -y --no-install-recommends \ libfontconfig1 \ libfreetype6 \ libxkbcommon-x11-0 \ libxkbcommon0 \ libdbus-1-3 \ libglib2.0-0 \ libegl1 \ libgl1 \ libopengl0 \ libxcb1 \ libxcb-icccm4 \ libxcb-image0 \ libxcb-keysyms1 \ libxcb-randr0 \ libxcb-render0 \ libxcb-render-util0 \ libxcb-shape0 \ libxcb-sync1 \ libxcb-xfixes0 \ libxcb-xinerama0 \ libxcb-xkb1 \ libxcb-cursor0 \ xdg-utils \ && rm -rf /var/lib/apt/lists/* # 3. C++ development (required to build C++ applications in Docker) RUN apt-get update && apt-get install -y --no-install-recommends \ build-essential \ ninja-build \ pkg-config \ git \ gdb \ && rm -rf /var/lib/apt/lists/* # 4. C# development install .NET 8 (required to build C# applications in Docker) RUN wget -O dotnet.tar.gz https://builds.dotnet.microsoft.com/dotnet/Sdk/8.0.417/dotnet-sdk-8.0.417-linux-x64.tar.gz && \ mkdir /usr/local/etc/dotnet-sdk-8.0 && \ tar -xzf dotnet.tar.gz -C /usr/local/etc/dotnet-sdk-8.0 && \ rm -rf /usr/bin/dotnet && \ ln -s /usr/local/etc/dotnet-sdk-8.0/dotnet /usr/bin/dotnet && \ rm -rf dotnet.tar.gz # for SDK Browser 2.x \ libxcb-shape0 \ libxcb-xkb1 \ libxcb-icccm4 \ libxcb-image0 \ libxcb-keysyms1 \ libxcb-render-util0 \ libxkbcommon-x11-0 \ linux-headers-5.4.0-135-generic \ lxterminal \ # sound \ libasound2 alsa-utils # entrypoint: create XDG_RUNTIME_DIR if it doesn�t exist RUN cat > /usr/local/bin/with-xdg-runtime <<'EOF' #!/usr/bin/env bash set -e if [ -z "${XDG_RUNTIME_DIR:-}" ]; then export XDG_RUNTIME_DIR=/tmp/xdg-runtime fi mkdir -p "$XDG_RUNTIME_DIR" chmod 700 "$XDG_RUNTIME_DIR" || true exec "$@" EOF RUN chmod +x /usr/local/bin/with-xdg-runtime ENTRYPOINT ["/usr/local/bin/with-xdg-runtime"] CMD ["/bin/bash"] ```
4. Assemble the Docker image (inside the `unigine-in-docker` folder): ```bash Docker build �tag your_image_name . ```

</details>


### Docker Test Run


1. Run the Docker image: ```bash docker run --rm \ --gpus all \ --device /dev/snd  --group-add audio \ -e DISPLAY=$DISPLAY \ -e NVIDIA_DRIVER_CAPABILITIES=graphics,compute,utility \ -e VK_ICD_FILENAMES=/usr/share/vulkan/icd.d/nvidia_icd.json \ -v /usr/share/vulkan/icd.d/nvidia_icd.json:/usr/share/vulkan/icd.d/nvidia_icd.json:ro \ -v /tmp/.X11-unix:/tmp/.X11-unix \ your_image_name ``` > **Notice:** The path to the `nvidia_icd.json` file on the host may differ (for example, `/usr/lib/x86_64-linux-gnu/vulkan/icd.d/nvidia_icd.json`).
2. Check selected GPU drivers with the following command: **`vulkaninfo`**. You will see the full information about your GPU. Or use the command **`vulkaninfo | grep GPU`** to display the model name of the GPU used.


## Using Docker Container


After you have successfully built and run GPU-accelerated **Docker** container, you can do the following:


1. [Develop your project using UnigineEditor or run an application (Engine instance) via **SDK Browser** (version 2.0.13+)](../../deployment/docker/sdk_in_docker.md).
2. [Run a **UNIGINE-based application**](../../deployment/docker/app_in_docker.md).
