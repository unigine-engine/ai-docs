# Developing UNIGINE-Project in Docker Container


To implement container-based development workflow for UNIGINE-based projects (i.e. to use UnigineEditor to create and edit worlds and run your application) you need to launch **UNIGINE SDK Browser** inside a *Docker* container. [Configure](../../deployment/docker/index.md) the *Docker* container first, or if it is already configured, follow these steps:


1. [Download and install](../../deployment/docker/sdk_in_docker.md#sdk_downloading) **UNIGINE SDK Browser** (version 2.0.13+)
2. [Launch](../../deployment/docker/sdk_in_docker.md#sdk_launch) **SDK Browser** in the container.


## SDK Browser Downloading and Installation


1. **[Download SDK Browser](https://developer.unigine.com/en/downloads/sdk_browser_v2_start_here) (for Linux)** and save it as `sdk_browser2_latest.run` to the target folder (`unigine-in-docker`).
2. Run the following commands from the `unigine-in-docker` folder to unpack and install **SDK Browser**: ```text $ cd ~/unigine-in-docker $ chmod +x sdk_browser2_latest.run $ ./sdk_browser2_latest.run $ chmod +x UNIGINE_SDK_Browser2/browser2.run ``` > **Notice:** During the installation you should read and accept the license terms.


## SDK Browser Launch in the Container


1. Enable connections with the X-server: ```text $ xhost +local:* ```
2. Launch **SDK Browser**: ```text $ docker run -it --rm --network host \ --runtime=nvidia --gpus 0 -e NVIDIA_VISIBLE_DEVICES=0 \ -e DISPLAY=${DISPLAY} \ --device /dev/snd \ -e NVIDIA_DRIVER_CAPABILITIES=display,compute \ -v /tmp/.X11-unix:/tmp/.X11-unix \ -v `pwd`/UNIGINE_SDK_Browser2:/opt/browser2 \ -v `pwd`/tmp/config:/root/.config/ \ -v `pwd`/unigine/config_browser:/root/.config/unigine \ -v `pwd`/unigine/config_editor:/root/.config/Unigine \ -v `pwd`/unigine/local/share:/root/.local/share/unigine/browser \ -v `pwd`/unigine/projects:/root/Documents/ \ -v /etc/localtime:/etc/localtime:ro \ -w /opt/browser2/ \ unigine/run-unigine-in-docker:latest \ ./browser2.run ``` ![](docker_5_2.png)


Congratulations! You have successfully launched *SDK Browser* in *Docker*! Now you can develop your project in UnigineEditor or run an Engine instance (your application).


> **Notice:** Functionality of the UnigineEditor and *SDK Browser* opened in the container has some limitations: you can't open the source code in the IDE, open local directory, and follow global links.
