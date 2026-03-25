# Unigine::SSLSocket Class (CS)

**Inherits from:** Socket


## SSLSocket Class

### Enums

## SSL_HANDSHAKE

| Name | Description |
|---|---|
| **ERROR_NONE** = 0 | The TLS/SSL I/O operation completed. |
| **ERROR_SSL** = 1 | A non-recoverable, fatal error in the SSL library occurred, usually a protocol error. The OpenSSL error queue contains more information on the error. If this error occurs then no further I/O operations should be performed on the connection. |
| **ERROR_WANT_READ** = 2 | Error code returned when the last operation was a read operation from a nonblocking BIO. It means that not enough data was available at this time to complete the operation. If at a later time the underlying BIO has data available for reading the same function can be called again. |
| **ERROR_WANT_WRITE** = 3 | Error code returned when the last operation was a write to a nonblocking BIO and it was unable to sent all data to the BIO. When the BIO is writable again, the same function can be called again. |
| **ERROR_WANT_X509_LOOKUP** = 4 | The operation did not complete because an application callback has asked to be called again. The TLS/SSL I/O function should be called again later. Details depend on the application. |
| **ERROR_SYSCALL** = 5 | Some non-recoverable, fatal I/O error occurred. The OpenSSL error queue may contain more information on the error. For socket I/O on Unix systems, consult errno for details. If this error occurs then no further I/O operations should be performed on the connection. |
| **ERROR_ZERO_RETURN** = 6 | The TLS/SSL peer has closed the connection for writing by sending the close_notify alert. No more data can be read. Note that *SSL_ERROR_ZERO_RETURN* does not necessarily indicate that the underlying transport has been closed. |
| **ERROR_WANT_CONNECT** = 7 | The operation did not complete; the same TLS/SSL I/O function should be called again later. The underlying BIO was not connected yet to the peer and the call would block in connect(). The SSL function should be called again when the connection is established. |
| **ERROR_WANT_ACCEPT** = 8 | The operation did not complete; the same TLS/SSL I/O function should be called again later. The underlying BIO was not connected yet to the peer and the call would block in accept(). The SSL function should be called again when the connection is established. |
| **ERROR_WANT_ASYNC** = 9 | The operation did not complete because an asynchronous engine is still processing data. The TLS/SSL I/O function should be called again later. The function must be called from the same thread that the original call was made from. |
| **ERROR_WANT_ASYNC_JOB** = 10 | The asynchronous job could not be started because there were no async jobs available in the pool. The application should retry the operation after a currently executing asynchronous operation for the current thread has completed. |
| **ERROR_WANT_CLIENT_HELLO_CB** = 11 | The operation did not complete because an application callback set by *SSL_CTX_set_client_hello_cb()* has asked to be called again. The TLS/SSL I/O function should be called again later. Details depend on the application. |
| **OK** = 100 | Hadnshake operation was successful. |
| **FAILED** = 101 | Hadnshake operation failed. |

## SSL_CTX_METHOD

| Name | Description |
|---|---|
| **TLS** = 0 | General-purpose version-flexible SSL/TLS methods. The actual protocol version used will be negotiated to the highest version mutually supported by the client and the server. Currently supported protocols are TLS 1.0, TLS 1.1, and TLS 1.2. |
| **TLS_1_0** = 1 | *Transport Layer Security Version 1.0* protocol. |
| **TLS_1_1** = 2 | *Transport Layer Security Version 1.1* protocol. |
| **TLS_1_2** = 3 | *Transport Layer Security Version 1.2* protocol. |
| **DTLS** = 4 | Version-flexible DTLS methods. Currently supported protocols are DTLS 1.0 and DTLS 1.2. |
| **DTLS_1** = 5 | *Datagram Transport Layer Security Version 1.0* protocol. |
| **DTLS_1_2** = 6 | *Datagram Transport Layer Security Version 1.2* protocol. |

## LOADER_TYPE

| Name | Description |
|---|---|
| **RSA_KEY** = 3 | RSA key. |
| **X509_CERT** = 1 | Self-signed X.509 certificate. |
| **X509_CACERT** = 2 | X.509 certificate issued by a Certification Agency. |

### Properties

## 🔒︎ bool IsAvailable

The value indicating if the socket is available (has been established, but not opened).
## 🔒︎ bool IsCertificateVerified

The value indicating if SSL certificate for the socket is successfully verified.
### Members

---

## SSLSocket ( )

Constructor. Creates a new SSL socket with default parameters (TLS).
## SSLSocket ( Socket.SOCKET_TYPE socket_type , SSLSocket.SSL_CTX_METHOD ssl_method )

Constructor. Creates a new SSL socket with the specified parameters.
### Arguments

- *[Socket.SOCKET_TYPE](../../../api/library/networking/class.socket_cs.md#SOCKET_TYPE)* **socket_type** - SSL socket type.
- *[SSLSocket.SSL_CTX_METHOD](../../../api/library/networking/class.sslsocket_cs.md#SSL_CTX_METHOD)* **ssl_method** - SSL connection method to be used.

## void Close ( )

Closes the socket.
## bool Accept ( Socket socket )

Accepts a connection on the socket.
### Arguments

- *[Socket](../../../api/library/networking/class.socket_cs.md)* **socket** - Socket that is bound to an address and listens to connections.

### Return value

true if the connection is accepted; otherwise, fals.
## bool Connect ( )

Initiates a connection on the socket.
### Return value

true if the connection is initialized; otherwise, false.
## bool Load ( SSLSocket.LOADER_TYPE loader_type , string path )

Loads a certificate from the file.
### Arguments

- *[SSLSocket.LOADER_TYPE](../../../api/library/networking/class.sslsocket_cs.md#LOADER_TYPE)* **loader_type** - Certificate type, one of the [LOADER_TYPE](#LOADER_TYPE_RSA_KEY) values.
- *string* **path** - Path to a certificate file.

### Return value

true if the certificate is loaded successfully, otherwise false.
## bool Parse ( SSLSocket.LOADER_TYPE loader_type , string data )

Parses a specified certificate.
### Arguments

- *[SSLSocket.LOADER_TYPE](../../../api/library/networking/class.sslsocket_cs.md#LOADER_TYPE)* **loader_type** - Certificate type, one of the [LOADER_TYPE](#LOADER_TYPE_RSA_KEY) values.
- *string* **data** - Certificate data.

### Return value

true if the certificate is parsed successfully, otherwise false.
## SSLSocket.SSL_HANDSHAKE Handshake ( )

Starts a handshake and returns the result.
### Return value

Handshake status.
## int Pending ( )

Returns the number of bytes available for immediate retrieval without reading from the socket object. This function is essential if you work with event loops.
### Return value

Number of bytes.
## uint Read ( IntPtr ptr , uint size , uint nmemb )

Reads the specified number of blocks of the specified size from the SSL connection to the specified destination buffer.
### Arguments

- *IntPtr* **ptr** - Pointer to the destination buffer to which the data is to be read.
- *uint* **size** - Size of a message block in bytes.
- *uint* **nmemb** - Number of message blocks to read from the SSL connection.

### Return value

Number of bytes actually read.
## uint Write ( IntPtr ptr , uint size , uint nmemb )

Writes the specified number of blocks of the specified size from the specified source buffer to the SSL connection.
### Arguments

- *IntPtr* **ptr** - Pointer to the source buffer from which the data is to be written.
- *uint* **size** - Size of a message block in bytes.
- *uint* **nmemb** - Number of message blocks to be written to the SSL connection.

### Return value

Number of bytes actually written.
## uint Peek ( IntPtr ptr , uint size , uint nmemb )

Reads the specified number of blocks of the specified size from the SSL connection to the specified destination buffer. This method is identical to *[Read()](../../...md#read_void_size_t_size_t_size_t)* except no bytes are actually removed from the underlying BIO during the read, so that a subsequent call to *[Read()](../../...md#read_void_size_t_size_t_size_t)* will yield at least the same bytes.
### Arguments

- *IntPtr* **ptr** - Pointer to the destination buffer to which the data is to be read.
- *uint* **size** - Size of a message block in bytes.
- *uint* **nmemb** - Number of message blocks to be written to the SSL connection.

### Return value

Number of bytes actually written.
