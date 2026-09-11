# Unigine::SSLSocket Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Socket


## SSLSocket Class

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
## SSLSocket ( int socket_type , int ssl_method )

Constructor. Creates a new SSL socket with the specified parameters.
### Arguments

- *int* **socket_type** - SSL socket type.
- *int* **ssl_method** - SSL connection method to be used.

## void close ( )

Closes the socket.
## int accept ( Socket socket )

Accepts a connection on the socket.
### Arguments

- *[Socket](../../../api/library/networking/class.socket_usc.md)* **socket** - Socket that is bound to an address and listens to connections.

### Return value

**1** if the connection is accepted; otherwise, fals.
## int connect ( )

Initiates a connection on the socket.
### Return value

**1** if the connection is initialized; otherwise, **0**.
## int load ( int loader_type , string path )

Loads a certificate from the file.
### Arguments

- *int* **loader_type** - Certificate type, one of the [LOADER_TYPE](#LOADER_TYPE_RSA_KEY) values.
- *string* **path** - Path to a certificate file.

### Return value

**1** if the certificate is loaded successfully, otherwise **0**.
## int parse ( int loader_type , string data )

Parses a specified certificate.
### Arguments

- *int* **loader_type** - Certificate type, one of the [LOADER_TYPE](#LOADER_TYPE_RSA_KEY) values.
- *string* **data** - Certificate data.

### Return value

**1** if the certificate is parsed successfully, otherwise **0**.
## int handshake ( )

Starts a handshake and returns the result.
### Return value

Handshake status.
## int pending ( )

Returns the number of bytes available for immediate retrieval without reading from the socket object. This function is essential if you work with event loops.
### Return value

Number of bytes.
## int read ( void * ptr , int size , int nmemb )

Reads the specified number of blocks of the specified size from the SSL connection to the specified destination buffer.
### Arguments

- *void ** **ptr** - Pointer to the destination buffer to which the data is to be read.
- *int* **size** - Size of a message block in bytes.
- *int* **nmemb** - Number of message blocks to read from the SSL connection.

### Return value

Number of bytes actually read.
## int write ( const void * ptr , int size , int nmemb )

Writes the specified number of blocks of the specified size from the specified source buffer to the SSL connection.
### Arguments

- *const void ** **ptr** - Pointer to the source buffer from which the data is to be written.
- *int* **size** - Size of a message block in bytes.
- *int* **nmemb** - Number of message blocks to be written to the SSL connection.

### Return value

Number of bytes actually written.
## int peek ( void * ptr , int size , int nmemb )

Reads the specified number of blocks of the specified size from the SSL connection to the specified destination buffer. This method is identical to *[read()](../../...md#read_void_size_t_size_t_size_t)* except no bytes are actually removed from the underlying BIO during the read, so that a subsequent call to *[read()](../../...md#read_void_size_t_size_t_size_t)* will yield at least the same bytes.
### Arguments

- *void ** **ptr** - Pointer to the destination buffer to which the data is to be read.
- *int* **size** - Size of a message block in bytes.
- *int* **nmemb** - Number of message blocks to be written to the SSL connection.

### Return value

Number of bytes actually written.
