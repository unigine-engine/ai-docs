# Unigine::Socket Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Stream


This class provides basic functionality for network interaction using stream sockets.


### Usage Example


In this example we create UDP sockets: server and five clients.


- The server sends broadcast packets containing the ID of the receiving client.
- Each client processes only the messages, that were addressed to it.
- In the world's *update()* method the server sends messages addressed to clients **2** and **5**.


In the `<your_unigine_project>.cpp` file we do the following:


- First, we describe our client and server and declare server and array of clients.
- In the world's *init()* method we initialize our clients.
- In the world's *update()* we check which keys were pressed and send messages to corresponding clients: Here we also call *update()* method for all clients to process server's messages.

  - **Client 2** - on ENTER key
  - **Client 5** - on WASD keys


```cpp
// <your_unigine_project>.cpp

/* ... */
// UDP port to be used
int UDP_PORT = 8889;

// UDP receive buffer size
int RECV_SIZE = 7;

// UDP send buffer size
int SEND_SIZE = 7;

/// Class representing the Server Socket
class ServerSocket {
	Socket socket;

	/// Server constructor
	ServerSocket() {
		// creating a UDP socket
		socket = new Socket(SOCKET_TYPE_DGRAM);

		// opening a socket on the specified port with a specified broadcast address
		socket.open("127.255.255.255", UDP_PORT);

		// setting the size of the sending buffer
		socket.send(SEND_SIZE);

		// setting the socket as a broadcasting one
		socket.broadcast();

		// setting the socket as a non-blocking one
		socket.nonblock();
	}

	/// Server destructor
	~ServerSocket()
	{
		// closing the socket
		socket.close();

		// deleting the socket
		delete socket;
	}

	/// method sending a message to a certain client
	void send_message(int client_num, string msg)
	{
		// preparing a message to be received by a client with a given client_id
		Blob blob =  new Blob();
		blob.clear();
		blob.writeInt(client_num);
		int buf[SEND_SIZE];
		for(int i=0; i < strlen(msg); i++)
			buf[i] = msg[i];
		blob.write(buf, strlen(msg));

		// getting message size
		int size = blob.getSize();

		// setting current position to start
		blob.seekSet(0);

		// sending the message
		socket.writeStream(blob, size);

        delete blob;
	}
};

/// Class representing the Client Socket
class ClientSocket {
	Socket socket;
	int id = 0;

	/// Client constructor
	ClientSocket()
	{
		// creating a UDP socket
		socket = new Socket(SOCKET_TYPE_DGRAM);

		// opening a socket on the specified port
		socket.open(UDP_PORT);

		// setting the size of the receiving buffer
        socket.recv(RECV_SIZE);

		// binding the socket to an address figured out from the host used for socket initialization
		socket.bind();

		// setting the socket as a non-blocking one
		socket.nonblock();
	}

	/// Client destructor
	~ClientSocket()
	{
		// closing the socket
		socket.close();

		// deleting the socket
		delete socket;
	}

	void setID(int num)
	{
		// setting client's ID
		id = num;
	}

	/// method checking for received packes from the server
	int update()
	{
		// preparing a blob to read the message into
		Blob temp_blob = new Blob();
		temp_blob.clear();

		// reading data from the socket
		socket.readStream(temp_blob, RECV_SIZE);

		if (temp_blob.getSize() > 0){

			// setting current position to start
			temp_blob.seekSet(0);

			// getting client's ID
			int num_client = temp_blob.readInt();

			// checking if the received message is addressed to this particular client and processing it
			if (num_client == id){
               log.message("\nClient[%d] - OPERATION_CODE: %s", num_client, temp_blob.readLine());
			}
		}

		delete temp_blob;

		return 1;
	}
};

	// declaring client and server sockets
	ServerSocket server_socket;
	ClientSocket clients[5];
int init() {

	/* ... */

	// initializing server and clients
	server_socket = new ServerSocket();
	for (int i = 0; i < 5; i++)
	{
		clients[i] = new ClientSocket();
		clients[i].setID(i + 1);
	}

	return 1;
}

// start of the main loop
int update() {

	Controls controls = engine.game.getPlayer().getControls();

	// sending messages on keys pressed to clients 2 and 5
	if (controls.clearState(CONTROLS_STATE_USE) == 1 )
		server_socket.send_message(2, "SWT");
    else if (controls.clearState(CONTROLS_STATE_FORWARD) == 1)
		server_socket.send_message(5, "F");
    else if (controls.clearState(CONTROLS_STATE_BACKWARD) == 1)
		server_socket.send_message(5, "B");
    else if (controls.clearState(CONTROLS_STATE_MOVE_LEFT) == 1)
		server_socket.send_message(5, "L");
    else if (controls.clearState(CONTROLS_STATE_MOVE_RIGHT) == 1)
		server_socket.send_message(5, "R");

	// updating clients
	for (int i = 0; i < 5; i++)
		clients[i].update();

	return 1;
}

/* ... */

int shutdown() {
	// Write here code to be called on world shutdown: delete resources that were created during world script execution to avoid memory leaks.

	// performing cleanup
	for (int i = 0; i < 5; i++)
		delete clients[i];

	return 1;
}

/* ... */

```


### See Also


API examples demonstrating how to manage sockets via API.


- **C++**:

  -
  -
- **UnigineScript**:

  -
  -
  -
  -
  -


## Socket Class

---

## static Socket ( int type )

Creates a socket of the specified type. When the socket receives data, packets from all network interfaces will be received. When the socket sends data, the default IP address will be used.
### Arguments

- *int* **type** - Socket type for TCP or UDP connections.

## static Socket ( int type , int port )

Creates a socket for TCP or UDP connections and opens it on a given port. When the socket receives data, packets from all network interfaces will be received. When the socket sends data, the default IP address will be used.
### Arguments

- *int* **type** - Socket type for TCP or UDP connections.
- *int* **port** - Port, on which the socket will be opened.

## static Socket ( int type , string host , int port )

Creates a socket for TCP or UDP connections and opens it on a given host and a given port. The host specifies the address, from and to which data will be sent.
### Arguments

- *int* **type** - Socket type for TCP or UDP connections.
- *string* **host** - Host, on which the socket will be opened.
- *int* **port** - Port, on which the socket will be opened.

## int getFD ( )

Returns the socket file descriptor.
### Return value

Socket file descriptor.
## getHost ( )

Returns the host name on which the socket is opened.
### Return value

Host name.
## int getPort ( )

Returns the port number on which the socket is opened.
### Return value

Port number.
## bool accept ( )

Accepts a connection on the socket.
### Arguments

### Return value

**true** if the connection is accepted; otherwise, **false**.
## bool bind ( )

Binds the socket to an address figured out from the host used for socket initialization.
### Return value

true if the address is bound; otherwise, false.
## bool block ( )

Sets up a blocking socket.
### Return value

true if the socket is blocking; otherwise, false.
## bool broadcast ( )

Sets up a broadcast socket. To create a broadcast socket, you need to create it with a broadcast host address first and then use this function.
### Return value

true if the socket is set up successfully; otherwise, false is returned.
## bool connect ( )

Initiates a connection on the socket. If the socket has been switched to the [non-blocking mode](#nonblock_int), this method will wait for a connection for up to 10 seconds. If the socket is blocking (either by default, or [set](#block_int) intentionally), the timeout period is defined either by OS. This method blocks the thread in which it is called, regardless of whether the socket is set as blocking or non-blocking.
### Return value

true if the connection is initialized; otherwise, false.
## bool connect ( size_t timeout_ms )

Initiates the connection on a socket. This method will wait for a connection up to the time set as the argument. This method blocks the thread in which it is called, regardless of whether the socket is set as blocking or non-blocking.
### Arguments

- *size_t* **timeout_ms** - Timeout during which the thread is blocked by this method, in ms.

### Return value

true if the connection is initialized; otherwise, false.
## bool listen ( int num )

Makes the socket listen to connections.
### Arguments

- *int* **num** - Maximum number of pending connections.

### Return value

true if the socket has started listening; otherwise, false.
## bool listenMulticastGroup ( )

Joins the socket to a multicast group. Available for [UDP sockets](#SOCKET_TYPE_DGRAM) only.
> **Notice:** The socket class doesn't allow creating a multicast server.


```cpp
int PORT = 8888;
Socket socket = new Socket(SOCKET_TYPE_DGRAM, PORT);
socket.listenMulticastGroup();

```


### Return value

true if the sockect has been joined successfully; otherwise, false.
## bool nodelay ( )

Enables Nagle's algorithm.
### Return value

true if the algorithm has been enabled successfully; otherwise, false.
## bool nonblock ( )

Makes the socket a non-blocking one.
### Return value

true if the socket has become non-blocking; otherwise, false.
## bool open ( int port , string host )

Opens the socket on a given port. When the socket receives data, packets from all network interfaces will be received. When the socket sends data, the default IP address will be used.
### Arguments

- *int* **port** - Port number, on which the socket will be opened.
- *string* **host** - Host, on which the socket will be opened.

### Return value

true if the socket is opened successfully; otherwise, false.
## bool open ( int port )

Opens the socket on a given port. When the socket receives data, packets from all network interfaces will be received. When the socket sends data, the default IP address will be used.
### Arguments

- *int* **port** - Port number, on which the socket will be opened.

### Return value

true if the socket is opened successfully; otherwise, false.
## bool recv ( int size )

Resizes an internal receiving buffer for a socket.
### Arguments

- *int* **size** - Receive buffer size in bytes.

### Return value

true if the buffer is resized successfully; otherwise, false.
## bool send ( int size )

Resizes an internal sending buffer for a socket.
### Arguments

- *int* **size** - Send buffer size in bytes.

### Return value

true if the buffer is resized successfully; otherwise, false.
