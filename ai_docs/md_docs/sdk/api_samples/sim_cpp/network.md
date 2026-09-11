# Networking

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


## DataBridge

This sample demonstrates how to set up the interaction of a UNIGINE application with a Python script via [DataBridge Plugin](../../../code/plugins/databridge/index.md).


When the Python script is running, DataBridge arranges the exchange of information between the application and the script, and the car drives along the route without driving through the walls.


To run the script, follow the instructions in `cpp_sim_samples/source/networking/car_controller_python_databridge/python/readme.md`.


> **Notice:** DataBridge Plugin requires **Python 3.12+** for correct operation and entity management.


The *Web Dash* button opens the web page illustrating how to obtain and change the DataBridge parameters via HTTP requests.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/networking/databridge*
## HTTP Get Player Position (Rest API)

This sample demonstrates a lightweight embedded asynchronous *HTTP* server that returns current world coordinates of the player in response to external *REST API* requests. The server handles *GET* requests to the **/player_pos** endpoint and responds with the current world coordinates of the active player in plain text format. The server runs directly inside the simulation and starts automatically with the sample. Server host and port are configurable via component parameters.


For demonstration, open the *URL* displayed on the plate in the scene.


This sample can serve as a foundation for live telemetry, integration with third-party monitoring systems, or any use case where external tools need access to runtime data from the simulation environment.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/networking/http_get_player_position*
## HTTP Get Screenshot (Rest API)

This sample demonstrates an embedded asynchronous *HTTP* server that captures application window content and streams it as *PNG* images via *REST API*.


The server responds to *GET* requests at the **/unigine.png** endpoint by converting the latest rendered frame to PNG format in memory and sending it directly to clients. The server runs asynchronously, and all resource access is properly synchronized to ensure thread safety.


For demonstration, open the *URL* displayed on the plate under the *Material Ball* in the scene to receive a real-time screenshot of the application. Server host and port are configured via component parameters.


This sample demonstrates how to access visual data from a real-time application for remote monitoring, or integration with web-based interfaces.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/networking/http_get_screenshot*
## HTTP Set Player Position (Rest API)

This sample demonstrates a lightweight embedded asynchronous HTTP server that handles **GET** requests to control player position through external applications. The server processes requests to the **/set_camera** endpoint with **x** and **y** parameters from the request, updating the player's world-space position accordingly while preserving the **z-axis** value.


The interface displays the connection URL on a text plate - open this URL in a web browser to trigger position changes. The server runs directly inside the simulation and starts automatically with the sample. Server host and port are configured via component parameters.


This sample can serve as a foundation for interactive control, integration with third-party systems, or any use case where external tools need to influence simulation state at runtime.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/networking/http_set_player_position*
## Secure Message Exchange (SSL Socket)

![](../../../samples/img/cpp_sim_samples_secure_message_exchange_ssl_socket.jpg)

This sample illustrates the implementation of message exchange with a server through an SSL connection. It contains two windows: one representing the server, and the other one - the client.


To exchange messages, you need to run the server first (click the *Run* button in the **Server** window), then connect the client (use the *Connect* button in the **Client** window). After that, you can type messages in the message areas and click *Send* to exchange them.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/networking/secure_message_exchange_ssl_socket*
