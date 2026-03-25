# IG::CIGI::Connector Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>


This class implements the connection between the IG Plugin and the CIGI protocol.

> **Notice:** [IG](../../../../../api/library/plugins/ig/api/index.md) plugin must be loaded.


## IG::CIGI::Connector Class

### Enums

## CIGI_MODE

| Name | Description |
|---|---|
| **CIGI_MODE_STANDBY** = 0 | Standby mode of the IG. This is the normal real-time operating mode for the IG. All packets issued by the Host will be processed by the IG. The IG should not perform diagnostics in this mode. |
| **CIGI_MODE_OPERATE** = 1 | Operate mode of the IG. This is the normal real-time operating mode for the IG. All packets issued by the Host will be processed by the IG. The IG should not perform diagnostics in this mode. |
| **CIGI_MODE_DEBUG** = 2 | Debug mode of the IG. This mode is similar to the Operate mode but provides data and/or error logging and other debugging features to aid integration or troubleshooting of the Host and IG interface. Because of the overhead of these debugging features, the IG may not always operate in a hard real-time fashion. |
| **CIGI_MODE_OFFLINE** = 3 | Offline Maintenance mode of the IG. In this mode, the IG ignores all data from the Host and sends only Start of Frame packets. This mode can be activated only from the IG. Because the IG Control packets from the Host are ignored by the IG, the IG must be placed into Reset/Standby mode before the Host can initiate further mode changes. |

### Members

---

## int init ( int version , const char * host , int send , int recv , int size = 1432 )

Initializes the CIGI Connector using the given parameters.
### Arguments

- *int* **version** - CIGI protocol version. One of the [CIGI_VERSION_*](#CIGI_VERSION_30) values.
- *const char ** **host** - CIGI Host address.
- *int* **send** - TCP port number to be used for sending packets to the CIGI Host.
- *int* **recv** - TCP port number to be used for receiving packets from the CIGI Host.
- *int* **size** - Packet size. The default value is 1432.

### Return value

1 if the CIGI Connector was initialized successfully; otherwise, 0.
## int shutdown ( )

Returns a value indicating if the CIGI Connector was shutdown successfully.
### Return value

true if the CIGI Connector was shutdown successfully; otherwise, false.
## bool isInitialized ( ) const

Returns a value indicating if the CIGI Connector was initialized successfully.
### Return value

true if the CIGI Connector was initialized successfully; otherwise, false.
## void setIGMode ( CIGI::CIGI_MODE mode )

Sets the current IG mode.
### Arguments

- *CIGI::CIGI_MODE* **mode** - IG mode. One of the [CIGI_MODE_*](#CIGI_MODE_STANDBY) values.

## CIGI::CIGI_MODE getIGMode ( ) const

Returns the current IG mode.
### Return value

IG mode. One of the [CIGI_MODE_*](#CIGI_MODE_STANDBY) values.
## void setIGStatus ( int status )

Sets the current IG status.
### Arguments

- *int* **status** - IG status. The following values are supported:

  - 0 - normal
  - 1-255 - an error has occurred

## int getIGStatus ( ) const

Returns the current IG status.
### Return value

IG status. The following values are supported:
- 0 - normal
- 1-255 - an error has occurred


## void setSynchronous ( bool synchronous )

Sets a value indicating if synchronous operation mode is currently enabled (when disabled, asynchronous mode is used).
### Arguments

- *bool* **synchronous** - true to enable synchronous operation mode; false - to use asynchronous mode.

## bool isSynchronous ( ) const

Returns a value indicating if synchronous operation mode is currently enabled (when disabled, asynchronous mode is used).
### Return value

true if synchronous operation mode is currently enabled; otherwise, false.
## bool isInterpolation ( ) const

Returns a value indicating if interpolation and extrapolation are enabled.
### Return value

true if interpolation and extrapolation are enabled; otherwise, false.
## unsigned int getIGFrame ( ) const

Returns the number of the current frame for the IG.
### Return value

Current IG frame number.
## unsigned int getHostFrame ( ) const

Returns the number of the current frame for the Host.
### Return value

Current Host frame number.
## double getTime ( ) const

Returns the IG's simulation time.
### Return value

IG's simulation time, in seconds.
## double getLastReceivedHostTime ( ) const

Returns the last received Host time (*timestamp* value in "IG Control").
### Return value

Last received Host time, in seconds.
## void * addOnConnectCallback ( Unigine:: CallbackBase * func )

Adds a callback function to be fired when the Host has connected.
### Arguments

- *Unigine::[CallbackBase](../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **func** - Callback pointer.

### Return value

ID of the last added connect callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnConnectCallback_void_ptr_bool) this callback when necessary.
## bool removeOnConnectCallback ( void * id )

Removes the specified callback from the list of Connect callbacks.
### Arguments

- *void ** **id** - Connect callback ID obtained when [adding](#addOnConnectCallback_CallbackBase_ptr_void_ptr) it.

### Return value

True if the Connect callback with the given ID was removed successfully; otherwise false.
## void * addOnReceivePacketCallback ( int cigi_opcode , Unigine:: CallbackBase1 * func )

Sets a callback function to be fired when a packet of the specified type has been received from the Host.
### Arguments

- *int* **cigi_opcode** - CIGI data packet opcode. One of the [CIGI_OPCODE_*](#CIGI_OPCODE_IG_CONTROL) values.
- *Unigine::[CallbackBase1](../../../../../api/library/common/callbacks/class.callbackbase1_cpp.md) ** **func** - Callback pointer. The callback function must have the following signature: (*Unigine::Plugins::IG::CIGI::CigiHostPacket* ***packet**)

### Return value

ID of the last added Receive Packet callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnReceivePacketCallback_void_ptr_bool) this callback when necessary.
## bool removeOnReceivePacketCallback ( void * id )

Removes the specified callback from the list of Receive Packet callbacks.
### Arguments

- *void ** **id** - Receive Packet callback ID obtained when [adding](#addOnReceivePacketCallback_int_CallbackBase1_ptr_void_ptr) it.

### Return value

true if the Receive Packet callback with the given ID was removed successfully; otherwise false.
## void * addOnSendPacketCallback ( int cigi_opcode , Unigine:: CallbackBase4 * func )

Sets a callback function to be fired right before sending a response to a request. This can be used to send additional data required by a host (e.g., velocities of the point of intersection for LOS/HAT queries which is useful in case of landing on a moving platform).
A callback function has the following signature:


(*bool* &**ret**, *IG::CIGI::CigiIGPacket* ***response**, *IG::CIGI::CigiHostPacket* ***request**, *IG::IGIntersection* ***intersection**)


- **ret** - boolean value indicating if the packet is to be sent or not;
- **response** - the packet to be sent;
- **request** - request for which a packet is to be sent as a response (can be nullptr);
- **intersection** - additional info on intersection (if necessary).


```cpp
void AppSystemLogic::init_cigi()
{
    int index = Engine::get()->findPlugin("CIGIConnector");
    // check CIGIConnector plugin load
    if (index < 0)
        return;
    // get CIGI interface
    cigi = IG::CIGI::Connector::get();

    cigi->addOnSendPacketCallback(Plugins::IG::CIGI::CIGI_OPCODE_LOS_EXT_RESPONSE, MakeCallback(this, &AppSystemLogic::on_los_ext_send));
    cigi->addOnSendPacketCallback(Plugins::IG::CIGI::CIGI_OPCODE_LOS_RESPONSE, MakeCallback(this, &AppSystemLogic::on_los_ext_send));
}
void AppSystemLogic::on_los_ext_send(bool &ret, IG::CIGI::CigiIGPacket *response, IG::CIGI::CigiHostPacket *request, IG::IGIntersection *intersection)
{
    ret = false;
    Log::message("reject packet %d\n", response->getType());
    if (request)
        Log::message("request was %d\n", request->getType());
    if (intersection)
    {
        Log::message("intersection was\n");
        if (intersection->object)
            Log::message("intersection object %s\n", intersection->object->getName());
    }
}

```


### Arguments

- *int* **cigi_opcode** - CIGI data packet opcode. One of the [CIGI_OPCODE_*](#CIGI_OPCODE_IG_CONTROL) values.
- *Unigine::[CallbackBase4](../../../../../api/library/common/callbacks/class.callbackbase4_cpp.md) ** **func** - Callback pointer. The callback function must have the following signature: (*bool* &**ret**, *IG::CIGI::CigiIGPacket* ***response**, *IG::CIGI::CigiHostPacket* ***request**, *IG::IGIntersection* ***intersection**)

### Return value

ID of the last added Send Packet callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnSendPacketCallback_void_ptr_bool) this callback when necessary.
## bool removeOnSendPacketCallback ( void * id )

Removes the specified callback from the list of Send Packet callbacks.
### Arguments

- *void ** **id** - Send Packet callback ID obtained when [adding](#addOnSendPacketCallback_int_CallbackBase4_ptr_void) it.

### Return value

True if the Send Packet callback with the given ID was removed successfully; otherwise false.
## int getNumHostPackets ( )

Returns the total number of packets received from the Host.
### Return value

Total number of packets received from the Host.
## CigiHostPacket * getHostPacket ( int num )

Returns the specified [CIGI Host packet](../../../../../api/library/plugins/ig/cigi/class.icigihostpacket_cpp.md).
### Arguments

- *int* **num** - ID of the Host packet.

### Return value

CIGI Host packet.
## CigiIGPacket * createIGPacket ( int ig_opcode )

Creates IG Packet to be sent to the Host.
### Arguments

- *int* **ig_opcode** - IG opcode, one of [CIGI_OPCODE_*](#CIGI_OPCODE_START_OF_FRAME) values.

### Return value

IG Packet to be sent to the Host.
## void addIGPacket ( CigiIGPacket * packet )

Sends the specified [IG packet](../../../../../api/library/plugins/ig/cigi/class.icigiigpacket_cpp.md) to the Host.
### Arguments

- *[CigiIGPacket](../../../../../api/library/plugins/ig/cigi/class.icigiigpacket_cpp.md) ** **packet** - IG Packet to be sent to the Host.

## void setProcessPacket ( int op_code , bool enabled )

Sets a value indicating if the specified IG packets received are to be processed or skipped.
### Arguments

- *int* **op_code** - IG opcode, one of [CIGI_OPCODE_*](#CIGI_OPCODE_START_OF_FRAME) values.
- *bool* **enabled** - true to process packets of the specified type, **false** to skip them.

## void showDebug ( )

Displays the debug information.
## void setWeatherLayerType ( int id , const CigiWeatherLayerType& type )

### Arguments

- *int* **id** - Weather layer ID.
- *const CigiWeatherLayerType&* **type** - Weather layer type, one of the following values:

  - *Plugins::IG::WeatherLayerType::LAYER_BASE* - base layer.
  - *Plugins::IG::WeatherLayerType::LAYER_CLOUD* - [cloud layer](../../../../../api/library/plugins/weather/class.weatherlayercloud_cpp.md).
  - *Plugins::IG::WeatherLayerType::LAYER_PRECIPITATION* - [precipitation layer](../../../../../api/library/plugins/weather/class.weatherlayerprecipitation_cpp.md).

## const CigiWeatherLayerType & getWeatherLayerType ( int id ) const

### Arguments

- *int* **id** - Weather layer ID.

### Return value

Weather layer type, one of the following values:
- *Plugins::IG::WeatherLayerType::LAYER_BASE* - base layer.
- *Plugins::IG::WeatherLayerType::LAYER_CLOUD* - [cloud layer](../../../../../api/library/plugins/weather/class.weatherlayercloud_cpp.md).
- *Plugins::IG::WeatherLayerType::LAYER_PRECIPITATION* - [precipitation layer](../../../../../api/library/plugins/weather/class.weatherlayerprecipitation_cpp.md).
