# Unigine::SSLSocket Class (CPP)

**Header:** #include <UnigineSSLSocket.h>

**Inherits from:** Socket


## SSLSocket Class

### Enums

## SSL_HANDSHAKE

| Name | Description |
|---|---|
| **SSL_HANDSHAKE_ERROR_NONE** = 0 | The TLS/SSL I/O operation completed. |
| **SSL_HANDSHAKE_ERROR_SSL** = 1 | A non-recoverable, fatal error in the SSL library occurred, usually a protocol error. The OpenSSL error queue contains more information on the error. If this error occurs then no further I/O operations should be performed on the connection. |
| **SSL_HANDSHAKE_ERROR_WANT_READ** = 2 | Error code returned when the last operation was a read operation from a nonblocking BIO. It means that not enough data was available at this time to complete the operation. If at a later time the underlying BIO has data available for reading the same function can be called again. |
| **SSL_HANDSHAKE_ERROR_WANT_WRITE** = 3 | Error code returned when the last operation was a write to a nonblocking BIO and it was unable to sent all data to the BIO. When the BIO is writable again, the same function can be called again. |
| **SSL_HANDSHAKE_ERROR_WANT_X509_LOOKUP** = 4 | The operation did not complete because an application callback has asked to be called again. The TLS/SSL I/O function should be called again later. Details depend on the application. |
| **SSL_HANDSHAKE_ERROR_SYSCALL** = 5 | Some non-recoverable, fatal I/O error occurred. The OpenSSL error queue may contain more information on the error. For socket I/O on Unix systems, consult errno for details. If this error occurs then no further I/O operations should be performed on the connection. |
| **SSL_HANDSHAKE_ERROR_ZERO_RETURN** = 6 | The TLS/SSL peer has closed the connection for writing by sending the close_notify alert. No more data can be read. Note that *SSL_ERROR_ZERO_RETURN* does not necessarily indicate that the underlying transport has been closed. |
| **SSL_HANDSHAKE_ERROR_WANT_CONNECT** = 7 | The operation did not complete; the same TLS/SSL I/O function should be called again later. The underlying BIO was not connected yet to the peer and the call would block in connect(). The SSL function should be called again when the connection is established. |
| **SSL_HANDSHAKE_ERROR_WANT_ACCEPT** = 8 | The operation did not complete; the same TLS/SSL I/O function should be called again later. The underlying BIO was not connected yet to the peer and the call would block in accept(). The SSL function should be called again when the connection is established. |
| **SSL_HANDSHAKE_ERROR_WANT_ASYNC** = 9 | The operation did not complete because an asynchronous engine is still processing data. The TLS/SSL I/O function should be called again later. The function must be called from the same thread that the original call was made from. |
| **SSL_HANDSHAKE_ERROR_WANT_ASYNC_JOB** = 10 | The asynchronous job could not be started because there were no async jobs available in the pool. The application should retry the operation after a currently executing asynchronous operation for the current thread has completed. |
| **SSL_HANDSHAKE_ERROR_WANT_CLIENT_HELLO_CB** = 11 | The operation did not complete because an application callback set by *SSL_CTX_set_client_hello_cb()* has asked to be called again. The TLS/SSL I/O function should be called again later. Details depend on the application. |
| **SSL_HANDSHAKE_OK** = 100 | Hadnshake operation was successful. |
| **SSL_HANDSHAKE_FAILED** = 101 | Hadnshake operation failed. |

## SSL_CTX_METHOD

| Name | Description |
|---|---|
| **SSL_CTX_METHOD_TLS** = 0 | General-purpose version-flexible SSL/TLS methods. The actual protocol version used will be negotiated to the highest version mutually supported by the client and the server. Currently supported protocols are TLS 1.0, TLS 1.1, and TLS 1.2. |
| **SSL_CTX_METHOD_TLS_1_0** = 1 | *Transport Layer Security Version 1.0* protocol. |
| **SSL_CTX_METHOD_TLS_1_1** = 2 | *Transport Layer Security Version 1.1* protocol. |
| **SSL_CTX_METHOD_TLS_1_2** = 3 | *Transport Layer Security Version 1.2* protocol. |
| **SSL_CTX_METHOD_DTLS** = 4 | Version-flexible DTLS methods. Currently supported protocols are DTLS 1.0 and DTLS 1.2. |
| **SSL_CTX_METHOD_DTLS_1** = 5 | *Datagram Transport Layer Security Version 1.0* protocol. |
| **SSL_CTX_METHOD_DTLS_1_2** = 6 | *Datagram Transport Layer Security Version 1.2* protocol. |

## LOADER_TYPE

| Name | Description |
|---|---|
| **LOADER_TYPE_RSA_KEY** = 3 | RSA key. |
| **LOADER_TYPE_X509_CERT** = 1 | Self-signed X.509 certificate. |
| **LOADER_TYPE_X509_CACERT** = 2 | X.509 certificate issued by a Certification Agency. |

### Members

## bool isAvailable () const

Returns the current value indicating if the socket is available (has been established, but not opened).
### Return value

**true** if the socket is available is enabled ; otherwise **false**.
## bool isCertificateVerified () const

Returns the current value indicating if SSL certificate for the socket is successfully verified.
### Return value

**true** if SSL certificate for the socket is successfully verified is enabled ; otherwise **false**.
---

## SSLSocket ( )

Constructor. Creates a new SSL socket with default parameters (TLS).
## SSLSocket ( Socket::SOCKET_TYPE socket_type , SSLSocket::SSL_CTX_METHOD ssl_method )

Constructor. Creates a new SSL socket with the specified parameters.
### Arguments

- *[Socket::SOCKET_TYPE](../../../api/library/networking/class.socket_cpp.md#SOCKET_TYPE)* **socket_type** - SSL socket type.
- *[SSLSocket::SSL_CTX_METHOD](../../../api/library/networking/class.sslsocket_cpp.md#SSL_CTX_METHOD)* **ssl_method** - SSL connection method to be used.

## void close ( )

Closes the socket.
## bool accept ( const Ptr < Socket > & socket )

Accepts a connection on the socket.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Socket](../../../api/library/networking/class.socket_cpp.md)> &* **socket** - Socket that is bound to an address and listens to connections.

### Return value

true if the connection is accepted; otherwise, fals.
## bool connect ( )

Initiates a connection on the socket.
### Return value

true if the connection is initialized; otherwise, false.
## bool load ( SSLSocket::LOADER_TYPE loader_type , const char * path )

Loads a certificate from the file.
### Arguments

- *[SSLSocket::LOADER_TYPE](../../../api/library/networking/class.sslsocket_cpp.md#LOADER_TYPE)* **loader_type** - Certificate type, one of the [LOADER_TYPE](#LOADER_TYPE_RSA_KEY) values.
- *const char ** **path** - Path to a certificate file.

### Return value

true if the certificate is loaded successfully, otherwise false.
## bool parse ( SSLSocket::LOADER_TYPE loader_type , const char * data )

Parses a specified certificate.
### Arguments

- *[SSLSocket::LOADER_TYPE](../../../api/library/networking/class.sslsocket_cpp.md#LOADER_TYPE)* **loader_type** - Certificate type, one of the [LOADER_TYPE](#LOADER_TYPE_RSA_KEY) values.
- *const char ** **data** - Certificate data.

### Return value

true if the certificate is parsed successfully, otherwise false.
## SSLSocket::SSL_HANDSHAKE handshake ( )

Starts a handshake and returns the result.
### Return value

Handshake status.
## int pending ( ) const

Returns the number of bytes available for immediate retrieval without reading from the socket object. This function is essential if you work with event loops.
### Return value

Number of bytes.
## size_t read ( void * ptr , size_t size , size_t nmemb ) const

Reads the specified number of blocks of the specified size from the SSL connection to the specified destination buffer.
### Arguments

- *void ** **ptr** - Pointer to the destination buffer to which the data is to be read.
- *size_t* **size** - Size of a message block in bytes.
- *size_t* **nmemb** - Number of message blocks to read from the SSL connection.

### Return value

Number of bytes actually read.
## size_t write ( const void * ptr , size_t size , size_t nmemb ) const

Writes the specified number of blocks of the specified size from the specified source buffer to the SSL connection.
### Arguments

- *const void ** **ptr** - Pointer to the source buffer from which the data is to be written.
- *size_t* **size** - Size of a message block in bytes.
- *size_t* **nmemb** - Number of message blocks to be written to the SSL connection.

### Return value

Number of bytes actually written.
## size_t peek ( void * ptr , size_t size , size_t nmemb ) const

Reads the specified number of blocks of the specified size from the SSL connection to the specified destination buffer. This method is identical to *[read](../../...md#read_void_size_t_size_t_size_t)* except no bytes are actually removed from the underlying BIO during the read, so that a subsequent call to *[read](../../...md#read_void_size_t_size_t_size_t)* will yield at least the same bytes.
### Arguments

- *void ** **ptr** - Pointer to the destination buffer to which the data is to be read.
- *size_t* **size** - Size of a message block in bytes.
- *size_t* **nmemb** - Number of message blocks to be written to the SSL connection.

### Return value

Number of bytes actually written.
