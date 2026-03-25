# Running UNIGINE-Based Application in Docker Container


You can run a **UNIGINE-based application** (whether it is a third-party solution or the one you've developed yourself) inside a **Docker** container you have already [configured](../../deployment/docker/index.md).


First, prepare the application that you want to run:


1. Download it from an external resource or, if it is your application, create a final [Release build](../../editor2/projects/build_project.md).
2. Move the application with all its content and additional libraries (if any) to the *Docker*-related folder (`unigine-in-docker`): ```text $ mv cpp_samples/  ~/unigine-in-docker/ $ mv csharp_component_samples/ ~/unigine-in-docker/ ```


Running C# and C++ UNIGINE-based applications slightly differs, so here as an example we use the **C++ Samples** and **C# Component Samples** demos included in **UNIGINE SDK**.


## Running C++ Application


1. Enable connections with the X-server: ```text $ xhost +local:* ```
2. Launch the **C++ application**: ```text $ cd ~/unigine-in-docker/ $ docker run -it --rm \ --runtime=nvidia --gpus 0 \ -e NVIDIA_VISIBLE_DEVICES=0 \ -e DISPLAY=${DISPLAY} \ --device /dev/snd \ -e NVIDIA_DRIVER_CAPABILITIES=display,compute \ -v /tmp/.X11-unix:/tmp/.X11-unix \ -v `pwd`/cpp_samples:/opt/project \ -v /etc/localtime:/etc/localtime:ro \ -w /opt/project/bin/ \ unigine/run-unigine-in-docker:latest \ ./cpp_samples_x64 ``` ![](cpp_example.png)


## Running C# Application


1. Enable connections with the X-server: ```text $ xhost +local:* ```
2. Launch the **C# application**: ```text $ cd ~/unigine-in-docker/ $ docker run -it --rm \ --runtime=nvidia --gpus 0 \ -e NVIDIA_VISIBLE_DEVICES=0 \ -e DISPLAY=${DISPLAY} \ --device /dev/snd \ -e NVIDIA_DRIVER_CAPABILITIES=display,compute \ -v /tmp/.X11-unix:/tmp/.X11-unix \ -v `pwd`/csharp_component_samples:/opt/project \ -v /etc/localtime:/etc/localtime:ro \ -w /opt/project/bin/ \ unigine/run-unigine-in-docker:latest \ dotnet csharp_component_samples_x64.dll -console_command "world_load csharp_samples" ``` ![](csharp_example.png)


Congratulations! You have successfully run a **UNIGINE-based application** in a *Docker* container!
