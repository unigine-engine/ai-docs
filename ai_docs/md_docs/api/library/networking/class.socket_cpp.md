# Unigine::Socket Class (CPP)

**Header:** #include <UnigineStreams.h>

**Inherits from:** Stream


This class provides basic functionality for network interaction using stream sockets.


### Usage Example


In this example we create UDP sockets: server and five clients.


- The server sends broadcast packets containing the ID of the receiving client.
- Each client processes only the messages, that were addressed to it.
- In the world's *update()* method the server sends messages addressed to clients **2** and **5**.


In the `AppWorldLogic.h` header file we describe our client and server and declare server and array of clients.


```cpp
#ifndef __APP_WORLD_LOGIC_H__
#define __APP_WORLD_LOGIC_H__

#include <UnigineLogic.h>
#include <UnigineStreams.h>
#include <UnigineInput.h>
#include <UnigineGame.h>

 // UDP port to be used
const int UDP_PORT = 8889;

// UDP receive buffer size
const int RECV_SIZE = 7;

// UDP send buffer size
const int SEND_SIZE = 7;

/* ... */

/// Class representing the Server Socket
class ServerSocket
{
public:
	/// Server constructor
	ServerSocket()
	{
		// creating a UDP socket
		socket = Unigine::Socket::create(Unigine::Socket::SOCKET_TYPE_DGRAM);

		// opening a socket on the specified port with a specified broadcast address
		socket->open("127.255.255.255", UDP_PORT);

		// setting the size of the sending buffer
		socket->send(SEND_SIZE);

		// setting the socket as a broadcasting one
		socket->broadcast();

		// setting the socket as a non-blocking one
		socket->nonblock();
	}

	/// Server destructor
	~ServerSocket()
	{
		// closing the socket
		socket->close();

		// clearing the socket
		socket.clear();
	}

	/// method sending a message to a certain client
	void send_message(int client_num, const char* message)
	{
		// preparing a message to be received by a client with a given client_id
		Unigine::BlobPtr blob = Unigine::Blob::create();
		blob->clear();
		blob->writeShort(client_num);
		blob->write(message, strlen(message));
		int size = blob->getSize();

		// sending the message
		socket->write(blob->getData(), size);
		blob.clear();
	}

private:
	// socket pointer
	Unigine::SocketPtr socket;
};

/// Class representing the Client Socket
class ClientSocket {

public:

	/// Client constructor
	ClientSocket()
	{
		// creating a UDP socket
		socket = Unigine::Socket::create(Unigine::Socket::SOCKET_TYPE_DGRAM);

		// opening a socket on the specified port

		socket->open(UDP_PORT);

		// setting the size of the receiving buffer
		socket->recv(RECV_SIZE);

		// binding the socket to an address figured out from the host used for socket initialization
		socket->bind();

		// setting the socket as a non-blocking one
		socket->nonblock();
	}

	/// Client destructor
	~ClientSocket()
	{
		// closing the socket
		socket->close();

		// clearing the socket
		socket.clear();
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
		Unigine::BlobPtr temp_blob = Unigine::Blob::create();
		temp_blob->clear();

		// reading data from the socket
		socket->readStream(temp_blob, RECV_SIZE);

		if (temp_blob->getSize() > 0) {

			// setting current position to start
			temp_blob->seekSet(0);

			// getting client's ID
			int num_client = temp_blob->readShort();

			// checking if the received message is addressed to this particular client and processing it
			if (num_client == id) {
				Unigine::Log::message("\nClient[%d] - OPERATION_CODE: %s", id, temp_blob->readLine().get());
			}
		}
		return 1;
	}
private:
	// socket pointer
	Unigine::SocketPtr socket;

	// client ID
	int id = 0;
};

class AppWorldLogic : public Unigine::WorldLogic
{

public:
	AppWorldLogic();
	virtual ~AppWorldLogic();

	int init() override;

	int update() override;
	int postUpdate() override;
	int updatePhysics() override;

	int shutdown() override;

	int save(const Unigine::StreamPtr &stream) override;
	int restore(const Unigine::StreamPtr &stream) override;
private:

	// declaring client and server sockets
	ServerSocket server_socket;
	ClientSocket clients[5];
};

#endif // __APP_WORLD_LOGIC_H__

```


In the `AppWorldLogic.cpp` implementation file we do the following:


- In the *AppWorldLogic::init()* method we initialize our clients.
- In the *AppWorldLogic::update()* we check which keys were pressed and send messages to corresponding clients: Here we also call *update()* method for all clients to process server's messages.

  - **Client 2** - on ENTER key
  - **Client 5** - on WASD keys


Here are the *AppWorldLogic::init()* and *AppWorldLogic::update()* methods:


```cpp
// AppWorldLogic.cpp

using namespace Unigine;

/* ... */

int AppWorldLogic::init()
{
	//initializing clients IDs
	for (int i = 0; i < 5; i++)
		clients[i].setID(i+1);

	return 1;
}

int AppWorldLogic::update()
{
	// sending messages on keys pressed to clients 2 and 5
	if (Input::isKeyDown(Input::KEY_E))
		server_socket.send_message(2, "E");
	else if (Input::isKeyDown(Input::KEY_W))
		server_socket.send_message(5, "W");
	else if (Input::isKeyDown(Input::KEY_A))
		server_socket.send_message(5, "A");
	else if (Input::isKeyDown(Input::KEY_S))
		server_socket.send_message(5, "S");
	else if (Input::isKeyDown(Input::KEY_D))
		server_socket.send_message(5, "D");

	// updating clients
	for (int i = 0; i < 5; i++)
		clients[i].update();

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

### Enums

## SOCKET_TYPE

| Name | Description |
|---|---|
| **SOCKET_TYPE_STREAM** = 0 | Socket for TCP packets. |
| **SOCKET_TYPE_DGRAM** = 1 | Socket for UDP packets. |

---

## static SocketPtr create ( Socket::SOCKET_TYPE type )

Creates a socket of the specified type. When the socket receives data, packets from all network interfaces will be received. When the socket sends data, the default IP address will be used.
### Arguments

- *[Socket::SOCKET_TYPE](../../../api/library/networking/class.socket_cpp.md#SOCKET_TYPE)* **type** - Socket type for TCP or UDP connections.

## static SocketPtr create ( Socket::SOCKET_TYPE type , int port )

Creates a socket for TCP or UDP connections and opens it on a given port. When the socket receives data, packets from all network interfaces will be received. When the socket sends data, the default IP address will be used.
### Arguments

- *[Socket::SOCKET_TYPE](../../../api/library/networking/class.socket_cpp.md#SOCKET_TYPE)* **type** - Socket type for TCP or UDP connections.
- *int* **port** - Port, on which the socket will be opened.

## static SocketPtr create ( Socket::SOCKET_TYPE type , const char * host , int port )

Creates a socket for TCP or UDP connections and opens it on a given host and a given port. The host specifies the address, from and to which data will be sent.
### Arguments

- *[Socket::SOCKET_TYPE](../../../api/library/networking/class.socket_cpp.md#SOCKET_TYPE)* **type** - Socket type for TCP or UDP connections.
- *const char ** **host** - Host, on which the socket will be opened.
- *int* **port** - Port, on which the socket will be opened.

## int getFD ( ) const

Returns the socket file descriptor.
### Return value

Socket file descriptor.
## const char * getHost ( ) const

Returns the host name on which the socket is opened.
### Return value

Host name.
## int getPort ( ) const

Returns the port number on which the socket is opened.
### Return value

Port number.
## bool accept ( const Ptr < Socket > & socket )

Accepts a connection on the socket.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Socket](../../../api/library/networking/class.socket_cpp.md)> &* **socket** - Socket that is bound to an address and listens to connections.

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
## void close ( )

Closes the socket.
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
const int PORT = 8888;
SocketPtr socket = Socket::create(Socket::SOCKET_TYPE_DGRAM, PORT);
socket->listenMulticastGroup();

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
## bool open ( int port )

Opens the socket on a given port. When the socket receives data, packets from all network interfaces will be received. When the socket sends data, the default IP address will be used.
### Arguments

- *int* **port** - Port number, on which the socket will be opened.

### Return value

true if the socket is opened successfully; otherwise, false.
## bool open ( const char * host , int port )

Opens the socket on a given port. When the socket receives data, packets from all network interfaces will be received. When the socket sends data, the default IP address will be used.
### Arguments

- *const char ** **host** - Host name, on which the socket will be opened.
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
## bool isReadyToRead ( int timeout_usec = 0 ) const

Returns a value indicating whether the socked is ready for reading data, waiting for the specified timeout period if necessary, to perform synchronous I/O.
### Arguments

- *int* **timeout_usec** - The maximum time for to wait for the socket's response, in microseconds. By default, the timeout is **0**.

### Return value

true if the socket is ready for reading data; otherwise, false.
## bool isReadyToWrite ( int timeout_usec = 0 ) const

Returns a value indicating whether the socked is ready for writing data, waiting for the specified timeout period if necessary, to perform synchronous I/O.
### Arguments

- *int* **timeout_usec** - The maximum time for to wait for the socket's response, in microseconds. By default, the timeout is **0**

### Return value

true if the socket is ready for writing data; otherwise, false.
