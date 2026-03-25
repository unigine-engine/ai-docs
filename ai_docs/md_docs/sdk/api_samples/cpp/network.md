# Network

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/cpp-api-samples](https://github.com/unigine-engine/cpp-api-samples)**.


## HTTP Image request

This sample shows how to implement an asynchronous *HTTP* request to a *REST API* to download image files and apply them to scene objects at runtime.


Two requests are performed to retrieve sample image data:


1. **eu.httpbin.org/image/png** - to download a *PNG* image
2. **eu.httpbin.org/image/jpeg** - to download a *JPEG* image


Only *PNG* and *JPEG* formats are supported for runtime loading into *[Image](../../../api/library/common/class.image_cpp.md)* Class instance from raw data.


The **[github.com/yhirose/cpp-httplib](https://github.com/yhirose/cpp-httplib)** library is used to perform the *HTTP* requests.


Once an image is retrieved, it is loaded from raw byte data using the *[Image::load()](../../../api/library/common/class.image_cpp.md#load_cstr_int_int)* method. If successful, the image is assigned to the albedo texture slot of the target material using *[Material::setTextureImage()](../../../api/library/rendering/class.material_cpp.md#setTextureImage_int_Image_int)*. The texture is applied at runtime to the specified surface of an object in the scene. If loading fails, the downloaded data is written to a file for further inspection.


This sample showcases a practical approach to fetching external media assets, validating them, and using them in your scenes or application logic.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/network/http_image_request*
## HTTP Request Handling

![](../../../samples/img/cpp_samples_http_request_handling.jpg)

This sample demonstrates how to implement asynchronous *HTTP GET* requests to external *REST API* and display the retrieved data in the user interface.


For demonstration, the sample performs two consecutive requests to external weather *API* and displays the results in real time.


1. **Geocoding** - resolving a location by name using *geocoding-api.open-meteo.com*.
2. **Current weather conditions** - retrieving live meteorological data for the selected location using *api.open-meteo.com*.


The **[github.com/yhirose/cpp-httplib](https://github.com/yhirose/cpp-httplib)** library is used to perform *HTTP* requests asynchronously. Check the console to view more details from server.


The *JSON* response is processed using the *[Json](../../../api/library/common/class.json_cpp.md)* Class and displayed in the sample *UI*. Additional response details can be viewed in the console output.


You can interactively test the workflow by entering a city name in the *UI*, viewing a list of possible matches, and selecting a specific location. This triggers a request for up-to-date weather data, which is then parsed and displayed in the *UI*.


Asynchronous processing ensures that network operations do not block or degrade the simulation performance.


This sample can serve as a foundation for integrating any external data providers.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/network/http_request_handling*
## TCP Sockets

This sample demonstrates how to establish and manage *TCP* socket connections between a server and multiple clients each represented by a UNIGINE-application. Clients can connect to the server, exchange text messages via the Console (**send_msg** command), and receive camera transform updates from the server.


**You need to have two instances of this 'C++ Samples' app running for this sample to work.**


Each instance can operate in one of two modes: *Server* or *Client*. To select the mode click on the corresponding button below. There you can also specify the desired *host and port*.


The server uses a non-blocking socket to accept client connections and creates a dedicated background thread for each connection. The communication protocol is based on custom messages (e.g., text or camera transforms) packed and unpacked using *[Blob](../../../api/library/common/class.blob_cpp.md)* streams. On the client side, a socket is created and connected to the server. Incoming and outgoing messages are sent/received using two threadsafe queues. To send text messages to the peer use the sample-specific console command `send_msg` (e.g. `send_msg hello world`)


Incoming messages are parsed using message headers. Both client and server use message buffering, timeouts, and validation checks to maintain connection stability and prevent invalid data processing.


The sample provides options to configure the server address and port, switch between modes, and monitor active connections.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/network/tcp_sockets*
## UDP Sockets

This sample shows how to use the sockets API to send and receive UDP messages between two peers in the network.


**You need to have two instances of this 'C++ Samples' app running for this sample to work.**


Each instance can operate in one of two modes: *Sender* or *Receiver*. To select the mode click on the corresponding button below. There you can also specify the *Receiver's hostname and port*.


In *Sender* mode the app packs the player's camera transform into a datagram and sends it to the Receiver on every engine update.


While in this mode you can also send text messages to the peer by using this sample-specific console command `send_msg` (e.g. `send_msg hello world`).


In *Receiver* mode the app receives and interprets incoming messages from the peer: the text messages are written to console, and the camera transforms are applied to the player.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/network/udp_sockets*
