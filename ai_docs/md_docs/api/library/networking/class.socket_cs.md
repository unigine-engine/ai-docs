# Unigine::Socket Class (CS)

**Inherits from:** Stream


This class provides basic functionality for network interaction using stream sockets.


### Usage Example


In this example we create UDP sockets: server and five clients.


- The server sends broadcast packets containing the ID of the receiving client.
- Each client processes only the messages, that were addressed to it.
- In the world's *Update()* method the server sends messages addressed to clients **2** and **5**.


In the `AppWorldLogic.cs` we do the following:


- First, we describe our client and server and declare server and array of clients.
- In the *AppWorldLogic.Init()* method we initialize our clients.
- In the *AppWorldLogic.Update()* we check which keys were pressed and send messages to corresponding clients: Here we also call *Update()* method for all clients to process server's messages.

  - **Client 2** - on ENTER key
  - **Client 5** - on WASD keys


```csharp
//AppWorldLogic.cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Runtime.InteropServices;

namespace UnigineApp
{
	static class Constants
	{
		// UDP port to be used
		public const int UDP_PORT = 8889;
		// UDP receive buffer size
		public const int RECV_SIZE = 7;
		// UDP send buffer size
		public const int SEND_SIZE = 7;
	}

	/// Class representing the Server Socket
	class ServerSocket
	{
		Socket socket;

		/// Server constructor
		public ServerSocket()
		{
			// creating a UDP socket
			socket = new Socket(Socket.SOCKET_TYPE.DGRAM);

			// opening a socket on the specified port with a specified broadcast address
			socket.Open("127.255.255.255", Constants.UDP_PORT);

			// setting the size of the sending buffer
			socket.Send(Constants.SEND_SIZE);

			// setting the socket as a broadcasting one
			socket.Broadcast();

			// setting the socket as a non-blocking one
			socket.Nonblock();
		}

		/// Server destructor
		~ServerSocket()
		{
			// closing the socket
			socket.Close();
		}

		/// method sending a message to a certain client
		public void send_message(short client_num, string message)
		{
			// preparing a message to be received by a client with a given client_id
			Blob blob = new Blob();
			blob.Clear();
			blob.WriteShort(client_num);
			blob.Write(Marshal.StringToHGlobalUni(message), (uint)message.Length);

			// getting message size
			var size = blob.GetSize();

			// setting current position to start
			blob.SeekSet(0);

			// sending the message
			socket.WriteStream(blob, size);

			blob.Clear();
		}
	};

	/// Class representing the Client Socket
	class ClientSocket
	{
		Socket socket;
		int id = 0;

		/// Client constructor
		public ClientSocket()
		{
			// creating a UDP socket
			socket = new Socket(Socket.SOCKET_TYPE.DGRAM);

			// opening a socket on the specified port
			socket.Open(Constants.UDP_PORT);

			// setting the size of the receiving buffer
			socket.Recv(Constants.RECV_SIZE);

			// binding the socket to an address figured out from the host used for socket initialization
			socket.Bind();

			// setting the socket as a non-blocking one
			socket.Nonblock();
		}

		/// Client destructor
		~ClientSocket()
		{

			// closing the socket
			socket.Close();
		}

		public void setID(int num)
		{
			// setting client's ID
			id = num;
		}

		/// method checking for received packets from the server
		public int update()
		{
			// preparing a blob to read the message into
			Blob temp_blob = new Blob();
			temp_blob.Clear();

			// reading data from the socket
			socket.ReadStream(temp_blob, Constants.RECV_SIZE);

			if (temp_blob.GetSize() > 0)
			{
				// setting current position to start
				temp_blob.SeekSet(0);

				// getting client's ID
				short num_client = temp_blob.ReadShort();

				// checking if the received message is addressed to this particular client and processing it
				if (num_client == id)
					Log.Message("\nClient[{0}] - OPERATION_CODE: {1}", id, temp_blob.ReadLine());
			}
			return 1;
		}
	};

	class AppWorldLogic : WorldLogic
	{
		//declaring server and client sockets
		ServerSocket server_socket;
		ClientSocket[] clients = new ClientSocket[5];

		// World logic, it takes effect only when the world is loaded.
		// These methods are called right after corresponding world script's (UnigineScript) methods.

		public AppWorldLogic()
		{
		}

		private void Init()
		{

			server_socket = new ServerSocket();
			// Write here code to be called on world initialization: initialize resources for your world scene during the world start.
			for (int i = 0; i < 5; i++)
			{
				clients[i] = new ClientSocket();
				clients[i].setID(i + 1);
			}
		}

		// start of the main loop
		private void Update()
		{
			// sending messages on keys pressed to clients 2 and 5
			if (Input.IsKeyDown(Input.KEY.E))
				server_socket.send_message(2, "E");
			else if (Input.IsKeyDown(Input.KEY.W))
				server_socket.send_message(5, "W");
			else if (Input.IsKeyDown(Input.KEY.A))
				server_socket.send_message(5, "A");
			else if (Input.IsKeyDown(Input.KEY.S))
				server_socket.send_message(5, "S");
			else if (Input.IsKeyDown(Input.KEY.D))
				server_socket.send_message(5, "D");

			// updating clients
			for (int i = 0; i < 5; i++)
				clients[i].update();

		}

		/* ... */

	}
}

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
| **STREAM** = 0 | Socket for TCP packets. |
| **DGRAM** = 1 | Socket for UDP packets. |

### Members

---

## Socket ( Socket.SOCKET_TYPE type )

Creates a socket of the specified type. When the socket receives data, packets from all network interfaces will be received. When the socket sends data, the default IP address will be used.
### Arguments

- *[Socket.SOCKET_TYPE](../../../api/library/networking/class.socket_cs.md#SOCKET_TYPE)* **type** - Socket type for TCP or UDP connections.

## Socket ( Socket.SOCKET_TYPE type , int port )

Creates a socket for TCP or UDP connections and opens it on a given port. When the socket receives data, packets from all network interfaces will be received. When the socket sends data, the default IP address will be used.
### Arguments

- *[Socket.SOCKET_TYPE](../../../api/library/networking/class.socket_cs.md#SOCKET_TYPE)* **type** - Socket type for TCP or UDP connections.
- *int* **port** - Port, on which the socket will be opened.

## Socket ( Socket.SOCKET_TYPE type , string host , int port )

Creates a socket for TCP or UDP connections and opens it on a given host and a given port. The host specifies the address, from and to which data will be sent.
### Arguments

- *[Socket.SOCKET_TYPE](../../../api/library/networking/class.socket_cs.md#SOCKET_TYPE)* **type** - Socket type for TCP or UDP connections.
- *string* **host** - Host, on which the socket will be opened.
- *int* **port** - Port, on which the socket will be opened.

## int GetFD ( )

Returns the socket file descriptor.
### Return value

Socket file descriptor.
## string GetHost ( )

Returns the host name on which the socket is opened.
### Return value

Host name.
## int GetPort ( )

Returns the port number on which the socket is opened.
### Return value

Port number.
## bool Accept ( Socket socket )

Accepts a connection on the socket.
### Arguments

- *[Socket](../../../api/library/networking/class.socket_cs.md)* **socket** - Socket that is bound to an address and listens to connections.

### Return value

**true** if the connection is accepted; otherwise, **false**.
## bool Bind ( )

Binds the socket to an address figured out from the host used for socket initialization.
### Return value

true if the address is bound; otherwise, false.
## bool Block ( )

Sets up a blocking socket.
### Return value

true if the socket is blocking; otherwise, false.
## bool Broadcast ( )

Sets up a broadcast socket. To create a broadcast socket, you need to create it with a broadcast host address first and then use this function.
### Return value

true if the socket is set up successfully; otherwise, false is returned.
## void Close ( )

Closes the socket.
## bool Connect ( )

Initiates a connection on the socket. If the socket has been switched to the [non-blocking mode](#nonblock_int), this method will wait for a connection for up to 10 seconds. If the socket is blocking (either by default, or [set](#block_int) intentionally), the timeout period is defined either by OS. This method blocks the thread in which it is called, regardless of whether the socket is set as blocking or non-blocking.
### Return value

true if the connection is initialized; otherwise, false.
## bool Connect ( size_t timeout_ms )

Initiates the connection on a socket. This method will wait for a connection up to the time set as the argument. This method blocks the thread in which it is called, regardless of whether the socket is set as blocking or non-blocking.
### Arguments

- *size_t* **timeout_ms** - Timeout during which the thread is blocked by this method, in ms.

### Return value

true if the connection is initialized; otherwise, false.
## bool Listen ( int num )

Makes the socket listen to connections.
### Arguments

- *int* **num** - Maximum number of pending connections.

### Return value

true if the socket has started listening; otherwise, false.
## bool ListenMulticastGroup ( )

Joins the socket to a multicast group. Available for [UDP sockets](#SOCKET_TYPE_DGRAM) only.
> **Notice:** The socket class doesn't allow creating a multicast server.


```csharp
const int PORT = 8888;
Socket socket = new Socket(Socket.SOCKET_TYPE.DGRAM, PORT);
socket.listenMulticastGroup();

```


### Return value

true if the sockect has been joined successfully; otherwise, false.
## bool Nodelay ( )

Enables Nagle's algorithm.
### Return value

true if the algorithm has been enabled successfully; otherwise, false.
## bool Nonblock ( )

Makes the socket a non-blocking one.
### Return value

true if the socket has become non-blocking; otherwise, false.
## bool Open ( int port )

Opens the socket on a given port. When the socket receives data, packets from all network interfaces will be received. When the socket sends data, the default IP address will be used.
### Arguments

- *int* **port** - Port number, on which the socket will be opened.

### Return value

true if the socket is opened successfully; otherwise, false.
## bool Open ( string host , int port )

Opens the socket on a given port. When the socket receives data, packets from all network interfaces will be received. When the socket sends data, the default IP address will be used.
### Arguments

- *string* **host** - Host name, on which the socket will be opened.
- *int* **port** - Port number, on which the socket will be opened.

### Return value

true if the socket is opened successfully; otherwise, false.
## bool Recv ( int size )

Resizes an internal receiving buffer for a socket.
### Arguments

- *int* **size** - Receive buffer size in bytes.

### Return value

true if the buffer is resized successfully; otherwise, false.
## bool Send ( int size )

Resizes an internal sending buffer for a socket.
### Arguments

- *int* **size** - Send buffer size in bytes.

### Return value

true if the buffer is resized successfully; otherwise, false.
## bool IsReadyToRead ( int timeout_usec = 0 )

Returns a value indicating whether the socked is ready for reading data, waiting for the specified timeout period if necessary, to perform synchronous I/O.
### Arguments

- *int* **timeout_usec** - The maximum time for to wait for the socket's response, in microseconds. By default, the timeout is **0**.

### Return value

true if the socket is ready for reading data; otherwise, false.
## bool IsReadyToWrite ( int timeout_usec = 0 )

Returns a value indicating whether the socked is ready for writing data, waiting for the specified timeout period if necessary, to perform synchronous I/O.
### Arguments

- *int* **timeout_usec** - The maximum time for to wait for the socket's response, in microseconds. By default, the timeout is **0**

### Return value

true if the socket is ready for writing data; otherwise, false.
