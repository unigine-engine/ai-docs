# IG::DIS::Connector Class (CPP)

**Header:** #include <plugins/Unigine/DISConnector/UnigineDISConnector.h>


## IG::DIS::Connector Class

### Members

---

## void init ( String ip , int site , int exercise , int app , int port )

Initializes the DIS Connector using the given parameters.
### Arguments

- *[String](../../../../../api/library/common/class.string_cpp.md)* **ip** - Broadcast address of the server computer that is used to broadcast messages to IG over the network
- *int* **site** - Site ID of this application instance.
- *int* **exercise** - Exercise ID of the DIS.
- *int* **app** - Application ID of this application instance. If not set, will be generated automatically.
- *int* **port** - Connection port. This argument is optional, default value is 3000.

## void init ( KDIS::NETWORK::Connection* newConnection )

Initializes the DIS Connector using the custom user connection.
### Arguments

- *KDIS::NETWORK::Connection** **newConnection** - Custom user connection.

## void shutdown ( )

Shuts down the DIS Connector. If the DIS Connection is initialized using a custom user connection, the method doesn't clear or stop the custom connection.
## void * addConnectCallback ( Unigine:: CallbackBase * func )

Sets the parameter to be called when connection is established.
### Arguments

- *Unigine::[CallbackBase](../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **func** - Parameter to be called when connection is established.

### Return value

ID of the last added connect callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeConnectCallback_void_ptr_bool) this callback when necessary.
## bool removeConnectCallback ( void * id )

Removes the specified callback from the list of Connect callbacks.
### Arguments

- *void ** **id** - Connect callback ID obtained when [adding](#addConnectCallback_CallbackBase_ptr_void_ptr) it.

### Return value

True if the Connect callback with the given ID was removed successfully; otherwise false.
## void * addReceivePacketCallback ( int pdu_type , Unigine:: CallbackBase * func )

Adds a callback function to be fired when the packet is received.
### Arguments

- *int* **pdu_type** - PDU type.
- *Unigine::[CallbackBase](../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **func** - Callback function to be called when the packet is received. Callback signature: void func(KDIS::PDU::Header *packet).

### Return value

ID of the last added Receive Packet callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeReceivePacketCallback_void_ptr_bool) this callback when necessary.
## bool removeReceivePacketCallback ( void * id )

Removes the specified callback from the list of Receive Packet callbacks.
### Arguments

- *void ** **id** - Receive Packet callback ID obtained when [adding](#addReceivePacketCallback_int_CallbackBase_ptr_void_ptr) it.

### Return value

True if the Receive Packet callback with the given ID was removed successfully; otherwise false.
## void setSiteID ( int site )

Sets the Site ID for the connector.
### Arguments

- *int* **site** - Site ID of the application instance.

## int getSiteID ( )

Returns the current Site ID of the connector.
### Return value

Site ID of the current application instance.
## void setAppID ( int app )

Sets the Application ID for the connector.
### Arguments

- *int* **app** - Application ID of the application instance.

## int getAppID ( )

Returns the current Application ID of the connector.
### Return value

Application ID of the current application instance.
## void setExerciseID ( int exercise )

Sets the Exercise ID for the connector.
### Arguments

- *int* **exercise** - Exercise ID of the DIS.

## int getExerciseID ( )

Returns the current Exercise ID of the connector.
### Return value

Exercise ID of the DIS.
## void sendPacket ( KDIS::PDU::Header packet )

Sends the custom packet.
### Arguments

- *KDIS::PDU::Header* **packet** - Custom packet.

## void installCustomPacketIDFilter ( PacketIDFilterInterface * filter )

Sets the custom user rules for filtering packets and entities by using the configuration parameters of the connector (Site ID, Exercise ID, Application ID). For example, you can create your packet filter and accept only packets and entities whose Site IDs and Exercise IDs match the current ones and the Application IDs don't match (actually, this is the default DIS Connector behavior):
```cpp
// inherit your own class from PacketIDFilterInterface
class CustomPacketIDFilter : public Unigine::Plugins::IG::DIS::PacketIDFilterInterface
{
public:
	// override the "check" methods
	virtual bool checkSiteID(int id) const override { return Unigine::Plugins::IG::DIS::Connector::get()->getSiteID() == id; }
	virtual bool checkExerciseID(int id) const override { return Unigine::Plugins::IG::DIS::Connector::get()->getExerciseID() == id; }
	virtual bool checkAppID(int id) const override { return Unigine::Plugins::IG::DIS::Connector::get()->getAppID() != id; }
};

// perform the following somewhere on the init or update stage
CustomPacketIDFilter *filter = new CustomPacketIDFilter();
Unigine::Plugins::IG::DIS::Connector::get()->installCustomPacketIDFilter(filter);

```


### Arguments

- *PacketIDFilterInterface ** **filter** - Custom filter.

## void setProcessPacket ( int op_code , bool enabled )

Sets a value indicating if the specified IG packets received are to be processed or skipped.
### Arguments

- *int* **op_code** - PDU type identifier.
- *bool* **enabled** - true to process packets of the specified type, **false** to skip them.

## void setConnectionThreadCallbacks ( Unigine:: CallbackBase * on_connect , Unigine:: CallbackBase * on_disconnect )

Sets callbacks for tuning the connection instance.
> **Warning:** This callback will be invoked in a thread that is not the main thread.


### Arguments

- *Unigine::[CallbackBase](../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **on_connect** - Parameter to be called in the connection thread immediately after the connection is established. Callback's signature: void func(KDIS::NETWORK::Connection * connection).
- *Unigine::[CallbackBase](../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **on_disconnect** - Parameter to be called after a connection failure or shutdown. Callback's signature: void func(KDIS::NETWORK::Connection * connection). > **Notice:** Connection may be nullptr.

## void setDeadReckoningStatic ( Unigine::Plugins::IG::Entity * entity )

Sets the Static dead reckoning algorithm to be used for the specified entity (Entity does not move).
 Dead Reckoning algorithms (*Static, FPW, RPW, RVW, FVW, FPB, RPB, RVB, FVB*) are used in Advanced Distributed Simulation to reduce the need to continually update a simulated entity's state information by the estimation of the position and orientation of an entity, based on a previously known position and orientation and estimates of the passage of simulation time and motion.
### Arguments

- *Unigine::Plugins::IG::Entity ** **entity** - Simulated Entity, for which the Static dead reckoning algorithm is to be used.

## void setDeadReckoningFPW ( Unigine::Plugins::IG::Entity * entity , const Vec3 & linear_velocity )

Sets the FPW dead reckoning algorithm to be used for the specified entity along with the specified constant rates. FPW means: **F** - fixed rotation, **P** - rate of position is to be held constant (velocity), **B** - world coordinate system.
 Dead Reckoning algorithms (*Static, FPW, RPW, RVW, FVW, FPB, RPB, RVB, FVB*) are used in Advanced Distributed Simulation to reduce the need to continually update a simulated entity's state information by the estimation of the position and orientation of an entity, based on a previously known position and orientation and estimates of the passage of simulation time and motion.
### Arguments

- *Unigine::Plugins::IG::Entity ** **entity** - Simulated Entity, for which the FPW dead reckoning algorithm is to be used with the specified values.
- *const [Vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **linear_velocity** - Linear velocity vector.

## void setDeadReckoningRPW ( Unigine::Plugins::IG::Entity * entity , const Vec3 & linear_velocity , const vec3 & angular_velocity_deg )

Sets the RPW dead reckoning algorithm to be used for the specified entity along with the specified constant rates. RPW means: **R** - rotating, **P** - rate of position is to be held constant (velocity), **B** - world coordinate system.
 Dead Reckoning algorithms (*Static, FPW, RPW, RVW, FVW, FPB, RPB, RVB, FVB*) are used in Advanced Distributed Simulation to reduce the need to continually update a simulated entity's state information by the estimation of the position and orientation of an entity, based on a previously known position and orientation and estimates of the passage of simulation time and motion.
### Arguments

- *Unigine::Plugins::IG::Entity ** **entity** - Simulated Entity, for which the RPW dead reckoning algorithm is to be used with the specified values.
- *const [Vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **linear_velocity** - Linear velocity vector.
- *const [vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **angular_velocity_deg** - Vector containing angular velocity values for each of the axes, in degrees.

## void setDeadReckoningRVW ( Unigine::Plugins::IG::Entity * entity , const Vec3 & linear_velocity , const Vec3 & linear_acceleration , const vec3 & angular_velocity_deg )

Sets the RVW dead reckoning algorithm to be used for the specified entity along with the specified constant rates. RVW means: **R** - rotating, **V** - rate of velocity is to be held constant (velocity + acceleration), **W** - world coordinate system.
 Dead Reckoning algorithms (*Static, FPW, RPW, RVW, FVW, FPB, RPB, RVB, FVB*) are used in Advanced Distributed Simulation to reduce the need to continually update a simulated entity's state information by the estimation of the position and orientation of an entity, based on a previously known position and orientation and estimates of the passage of simulation time and motion.
### Arguments

- *Unigine::Plugins::IG::Entity ** **entity** - Simulated Entity, for which the RVW dead reckoning algorithm is to be used with the specified values.
- *const [Vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **linear_velocity** - Linear velocity vector.
- *const [Vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **linear_acceleration** - Linear acceleration vector.
- *const [vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **angular_velocity_deg** - Vector containing angular velocity values for each of the axes, in degrees.

## void setDeadReckoningFVW ( Unigine::Plugins::IG::Entity * entity , const Vec3 & linear_velocity , const Vec3 & linear_acceleration )

Sets the FVW dead reckoning algorithm to be used for the specified entity along with the specified constant rates. FVW means: **F** - fixed rotation, **V** - rate of velocity is to be held constant (velocity + acceleration), **W** - world coordinate system.
 Dead Reckoning algorithms (*Static, FPW, RPW, RVW, FVW, FPB, RPB, RVB, FVB*) are used in Advanced Distributed Simulation to reduce the need to continually update a simulated entity's state information by the estimation of the position and orientation of an entity, based on a previously known position and orientation and estimates of the passage of simulation time and motion.
### Arguments

- *Unigine::Plugins::IG::Entity ** **entity** - Simulated Entity, for which the FVW dead reckoning algorithm is to be used with the specified values.
- *const [Vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **linear_velocity** - Linear velocity vector.
- *const [Vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **linear_acceleration** - Linear acceleration vector.

## void setDeadReckoningFPB ( Unigine::Plugins::IG::Entity * entity , const Vec3 & linear_velocity , const vec3 & angular_velocity_deg )

Sets the FPB dead reckoning algorithm to be used for the specified entity along with the specified constant rates. FPB means: **F** - fixed rotation, **P** - rate of position is to be held constant (velocity), **B** - body-centered coordinate system.
 Dead Reckoning algorithms (*Static, FPW, RPW, RVW, FVW, FPB, RPB, RVB, FVB*) are used in Advanced Distributed Simulation to reduce the need to continually update a simulated entity's state information by the estimation of the position and orientation of an entity, based on a previously known position and orientation and estimates of the passage of simulation time and motion.
### Arguments

- *Unigine::Plugins::IG::Entity ** **entity** - Simulated Entity, for which the FPB dead reckoning algorithm is to be used with the specified values.
- *const [Vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **linear_velocity** - Linear velocity vector.
- *const [vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **angular_velocity_deg** - Vector containing angular velocity values for each of the axes, in degrees.

## void setDeadReckoningRPB ( Unigine::Plugins::IG::Entity * entity , const Vec3 & linear_velocity , const vec3 & angular_velocity_deg )

Sets the RPB dead reckoning algorithm to be used for the specified entity along with the specified constant rates. RPB means: **R** - rotating, **P** - rate of position is to be held constant (velocity), **B** - body-centered coordinate system.
 Dead Reckoning algorithms (*Static, FPW, RPW, RVW, FVW, FPB, RPB, RVB, FVB*) are used in Advanced Distributed Simulation to reduce the need to continually update a simulated entity's state information by the estimation of the position and orientation of an entity, based on a previously known position and orientation and estimates of the passage of simulation time and motion.
### Arguments

- *Unigine::Plugins::IG::Entity ** **entity** - Simulated Entity, for which the RPB dead reckoning algorithm is to be used with the specified values.
- *const [Vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **linear_velocity** - Linear velocity vector.
- *const [vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **angular_velocity_deg** - Vector containing angular velocity values for each of the axes, in degrees.

## void setDeadReckoningRVB ( Unigine::Plugins::IG::Entity * entity , const Vec3 & linear_velocity , const Vec3 & linear_acceleration , const vec3 & angular_velocity_deg )

Sets the RVB dead reckoning algorithm to be used for the specified entity along with the specified constant rates. RVB means: **R** - rotating, **V** - rate of velocity is to be held constant (velocity + acceleration), **B** - body-centered coordinate system.
 Dead Reckoning algorithms (*Static, FPW, RPW, RVW, FVW, FPB, RPB, RVB, FVB*) are used in Advanced Distributed Simulation to reduce the need to continually update a simulated entity's state information by the estimation of the position and orientation of an entity, based on a previously known position and orientation and estimates of the passage of simulation time and motion.
### Arguments

- *Unigine::Plugins::IG::Entity ** **entity** - Simulated Entity, for which the RVB dead reckoning algorithm is to be used with the specified values.
- *const [Vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **linear_velocity** - Linear velocity vector.
- *const [Vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **linear_acceleration** - Linear acceleration vector.
- *const [vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **angular_velocity_deg** - Vector containing angular velocity values for each of the axes, in degrees.

## void setDeadReckoningFVB ( Unigine::Plugins::IG::Entity * entity , const Vec3 & linear_velocity , const Vec3 & linear_acceleration , const vec3 & angular_velocity_deg )

Sets the FVB dead reckoning algorithm to be used for the specified entity along with the specified constant rates. FVB means: **F** - fixed rotation, **V** - rate of velocity is to be held constant (velocity + acceleration), **B** - body-centered coordinate system.
 Dead Reckoning algorithms (*Static, FPW, RPW, RVW, FVW, FPB, RPB, RVB, FVB*) are used in Advanced Distributed Simulation to reduce the need to continually update a simulated entity's state information by the estimation of the position and orientation of an entity, based on a previously known position and orientation and estimates of the passage of simulation time and motion.
### Arguments

- *Unigine::Plugins::IG::Entity ** **entity** - Simulated Entity, for which the FVB dead reckoning algorithm is to be used with the specified values.
- *const [Vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **linear_velocity** - Linear velocity vector.
- *const [Vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **linear_acceleration** - Linear acceleration vector.
- *const [vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **angular_velocity_deg** - Vector containing angular velocity values for each of the axes, in degrees.
