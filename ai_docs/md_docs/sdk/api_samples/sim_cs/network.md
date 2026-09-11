# Networking

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


## DataBridge

This sample demonstrates how to set up the interaction of a UNIGINE application with a Python script via [DataBridge Plugin](../../../code/plugins/databridge/index.md).


When the Python script is running, DataBridge arranges the exchange of information between the application and the script, and the car drives along the route without driving through the walls.


To run the script, follow the instructions in `csharp_sim_samples/source/databridge_python/readme.md`.


> **Notice:** DataBridge Plugin requires **Python 3.12+** for correct operation and entity management.


The Web Dash button opens the web page illustrating how to obtain and change the DataBridge parameters via HTTP requests.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_sim_samples/networking/databridge*
## HTTP Get Player Position (Rest API)

This sample demonstrates a lightweight embedded asynchronous *HTTP* server that returns current world coordinates of the player in response to external *REST API* requests. The server handles *GET* requests to the **/player_pos** endpoint and responds with the current world coordinates of the active player in plain text format. The server runs directly inside the simulation and starts automatically with the sample. Server host and port are configurable via component parameters.


For demonstration, open the *URL* displayed on the plate in the scene.


This sample can serve as a foundation for live telemetry, integration with third-party monitoring systems, or any use case where external tools need access to runtime data from the simulation environment.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_sim_samples/networking/http_get_player_position*
## HTTP Get Screenshot (Rest API)

This sample demonstrates an embedded asynchronous *HTTP* server that captures application window content and streams it as *PNG* images via *REST API*.


The server responds to *GET* requests at the **/unigine.png** endpoint by converting the latest rendered frame to PNG format in memory and sending it directly to clients. The server runs asynchronously, and all resource access is properly synchronized to ensure thread safety.


For demonstration, open the *URL* displayed on the plate under the *Material Ball* in the scene to receive a real-time screenshot of the application. Server host and port are configured via component parameters.


This sample demonstrates how to access visual data from a real-time application for remote monitoring, or integration with web-based interfaces.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_sim_samples/networking/http_get_screenshot*
## HTTP Set Player Position (Rest API)

This sample demonstrates a lightweight embedded asynchronous HTTP server that handles **GET** requests to control player position through external applications. The server processes requests to the **/set_camera** endpoint with **x** and **y** parameters from the request, updating the world-space position of the active player accordingly (preserving the original **z** coordinate).


For demonstration, open the URL displayed on the plate in the scene to trigger position changes. The server runs directly inside the simulation and starts automatically with the sample. Server host and port are configured via component parameters.


This sample can serve as a foundation for interactive control, integration with third-party systems, or any use case where external tools need to influence simulation state at runtime.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_sim_samples/networking/http_set_player_position*
