# IG::HLA::Connector Class (CPP)

**Header:** #include <plugins/Unigine/HLAConnector/UnigineHLAConnector.h>


## IG::HLA::Connector Class

### Members

---

## int init ( int version , const char * fom_path , const char * federate_name , const char * federation_execution_name )

Initializes the HLA Connector using the given parameters.
### Arguments

- *int* **version** - Callback type. One of the following values: [RTI13](#RTI13), [RTI1516](#RTI1516), or [RTI1516E](#RTI1516E).
- *const char ** **fom_path** - path to FOM file (.fed or .xml, depends on version)
- *const char ** **federate_name** - name of the current instance
- *const char ** **federation_execution_name** - name of the group of federates with the same FOM. > **Notice:** OpenRTI uses names like "*rti://fedExecName*", Pitch RTI uses simple "*fedExecName*".

### Return value

1 if the HLA Connector was initialized successfully; otherwise, 0.
## void setTimeRegulation ( bool start_constrained , bool start_regulating )

Sets time management mode for the federate. In general, a federate may be "regulating," "constrained," "regulating and constrained," or "neither regulating nor constrained.
### Arguments

- *bool* **start_constrained** - Constrained flag: true if the federate is a constrained one (can receive TSO messages); otherwise, false.
- *bool* **start_regulating** - Regulating flag: true if the federate is a regulating one (can send TSO messages); otherwise, false.

## int isConstrained ( )

Returns a value indicating if the federate is a constrained one, i.e. can receive TSO (time-stamped order) messages.
### Return value

1 if the federate is a constrained one; otherwise, 0.
## int isRegulating ( )

Returns a value indicating if the federate is a regulating one, i.e. can send TSO (time-stamped order) messages.
### Return value

1 if the federate is a regulating one; otherwise, 0.
## void setTimeStep ( double time_step )

Sets a lookahead value for a regulating federate, this value determines the frequency of calling the [*timeAdvanceRequest()*](#timeAdvanceRequest_double_void) method.
### Arguments

- *double* **time_step** - Enable flag. Use 1 to show the [debug window](../../../../../code/plugins/syncker/index.md#debug_window), or 0 - to hide it.

## double getLocalTime ( )

Returns the local time of the current federate.
### Return value

Local time of the current federate.
## void registerFederationSynchronizationPoint ( const char * label , const char * tag )

Registers a new synchronization point for all federates.
### Arguments

- *const char ** **label** - String uniquely identifying the synchronization point.
- *const char ** **tag** - User-supplied tag.

## void registerFederationSynchronizationPoint ( const char * label , const char * tag , const Vector <unsigned long> & sync_set )

Registers a new synchronization point.
### Arguments

- *const char ** **label** - String uniquely identifying the synchronization point.
- *const char ** **tag** - User-supplied tag.
- *const [Vector](../../../../../api/library/containers/vector/class.vector_cpp.md)<unsigned long> &* **sync_set** - List containing handles of federates to synchronize.

## void synchronizationPointAchieved ( const char * label )

Sends a message that specified synchronization point was successfully achieved with all requirements fulfilled.
### Arguments

- *const char ** **label** - String uniquely identifying the synchronization point.

## unsigned long getInteractionClassHandle ( const char * name )

Returns interaction class handle.
### Arguments

- *const char ** **name** - Interaction class name.

### Return value

Interaction class handle.
## unsigned long getParameterHandle ( const char * name , unsigned long which_class )

Returns parameter handle.
### Arguments

- *const char ** **name** - Parameter name.
- *unsigned long* **which_class** - Class to which the parameter belongs.

### Return value

Handle of the specified parameter.
## unsigned long getObjectClassHandle ( const char * name )

Returns object class handle.
### Arguments

- *const char ** **name** - Object class name

### Return value

Handle of the specified object class.
## unsigned long getAttributeHandle ( const char * name , unsigned long which_class )

Returns attribute handle.
### Arguments

- *const char ** **name** - Attribute name.
- *unsigned long* **which_class** - Class to which the attribute belongs.

### Return value

Handle of the specified attribute.
## void publishAndSubscribeObject ( unsigned long handle_id , const int & attributes )

Publish and subscribe for the specified Object Class.
### Arguments

- *unsigned long* **handle_id** - Handle ID.
- *const int &* **attributes** - List of attributes.

## void publishObject ( unsigned long handle_id , const int & attributes )

Publish the specified Object Class.
### Arguments

- *unsigned long* **handle_id** - Handle ID.
- *const int &* **attributes** - List of attributes.

## void subscribeObject ( unsigned long handle_id , const int & attributes )

Subscribe for the specified Object Class.
### Arguments

- *unsigned long* **handle_id** - Handle ID.
- *const int &* **attributes** - List of attributes.

## void publishAndSubscribeInteraction ( unsigned long handle_id )

Publish and subscribe for the specified Interaction Class.
### Arguments

- *unsigned long* **handle_id** - Class handle ID.

## void publishInteraction ( unsigned long handle_id )

Publish the specified Interaction Class.
### Arguments

- *unsigned long* **handle_id** - Class handle ID.

## void subscribeInteraction ( unsigned long handle_id )

Subscribe to the specified Interaction Class.
### Arguments

- *unsigned long* **handle_id** - Class handle ID.

## unsigned long registerObjectInstance ( unsigned long class_handle_id , const char * name )

Registers a new object instance instance with the specified name.
### Arguments

- *unsigned long* **class_handle_id** - Class handle ID.
- *const char ** **name** - Object name.

### Return value

Object handle.
## int updateAttributeValues ( unsigned long object_id , const int & attributes , const char * tag )

Updates attribute values for the specified object instance.
### Arguments

- *unsigned long* **object_id** - Object ID.
- *const int &* **attributes** - List of attributes.
- *const char ** **tag** - User-supplied tag.

### Return value

1 if the specified attribute values were updated successfully; otherwise, 0.
## int updateAttributeValues ( unsigned long object_id , const int & attributes , double time , const char * tag )

Updates attribute values for the specified object instance.
### Arguments

- *unsigned long* **object_id** - Object ID.
- *const int &* **attributes** - List of attributes.
- *double* **time** - Federation time.
- *const char ** **tag** - User-supplied tag.

### Return value

1 if the specified attribute values were updated successfully; otherwise, 0.
## int deleteObjectInstance ( unsigned long object_id , const char * tag )

Deletes the specified object instance.
### Arguments

- *unsigned long* **object_id** - Object ID.
- *const char ** **tag** - User-supplied tag.

### Return value

1 if the specified object instance was deleted successfully; otherwise, 0.
## int deleteObjectInstance ( unsigned long object_id , double time , const char * tag )

Deletes the specified object instance.
### Arguments

- *unsigned long* **object_id** - Object ID.
- *double* **time** - Federation time.
- *const char ** **tag** - User-supplied tag.

### Return value

1 if the specified object instance was deleted successfully; otherwise, 0.
## int sendInteraction ( unsigned long handle_id , const int & parameters , const char * tag )

Sends an interaction with the specified parameters.
### Arguments

- *unsigned long* **handle_id** - Handle ID.
- *const int &* **parameters** - List of parameters.
- *const char ** **tag** - User-supplied tag.

### Return value

1 if interaction was sent successfully; otherwise, 0.
## int sendInteraction ( unsigned long handle_id , const int & parameters , double time , const char * tag )

Sends an interaction with the specified parameters.
### Arguments

- *unsigned long* **handle_id** - Handle ID.
- *const int &* **parameters** - List of parameters.
- *double* **time** - Federation time.
- *const char ** **tag** - User-supplied tag.

### Return value

1 if interaction was sent successfully; otherwise, 0.
## void enableTimeRegulation ( double federate_time , double lookahead )

Enables time regulation mode for the federate.
### Arguments

- *double* **federate_time** - Federate time.
- *double* **lookahead** - Lookahead value for a regulating federate, this value determines the frequency of calling the [*timeAdvanceRequest()*](#timeAdvanceRequest_double_void) method.

## void disableTimeRegulation ( )

Disables time regulation mode for the federate.
## void enableTimeConstrained ( )

Enables time-constrained mode for the federate.
## void disableTimeConstrained ( )

Disables time-constrained mode for the federate.
## void timeAdvanceRequest ( double time )

Issues a Time Advance Request for the federate.


> **Notice:** This method is used by time-stepped federates.


### Arguments

- *double* **time** - Time value.

## void timeAdvanceRequestAvailable ( double time )

Enables time regulation mode for the federate.


> **Notice:** This method is used by time-stepped federates.


### Arguments

- *double* **time** - Time value.

## void nextEventRequest ( double time )

Advances the federate�s logical time to the time-stamp of the next relevant TSO event in the federation.


> **Notice:** This method is used by event-based federates.


### Arguments

- *double* **time** - Time stamp of the next local event the federate wishes to advance to.

## void nextEventRequestAvailable ( double time )

Advances the federate�s logical time to the time-stamp of the next relevant TSO event in the federation. The method is similar to [*nextEventRequest()*](#nextEventRequest_double_void), except that a time advance might be granted before all TSO events at the grant time have been delivered to the federate.


> **Notice:** This method is used by event-based federates.


### Arguments

- *double* **time** - Time stamp of the next local event the federate wishes to advance to.

## void flushQueueRequest ( double time )

Process all federation events regardless of time.
### Arguments

- *double* **time** - Time value.

## void enableAsynchronousDelivery ( )

Instructs the LRC to begin delivering receive-ordered events to the federate even while no time-advancement service is in progress.
## void disableAsynchronousDelivery ( )

Instructs the LRC not to deliver receive-ordered events in the absense of an in-progress time-advancement service. This has only a meaning for time-constrained federates, since non-constrained federates receive all events in receive order.
## void modifyLookahead ( double lookahead )

Sets the new lookahead window for the federate.
### Arguments

- *double* **lookahead** - New size of the interval extending forward from the federate�s logical time at a given point in execution in which a federate will not generate any time stamp ordered events.

## void queryLookahead ( double lookahead )

Returns the current lookahead window being used for the federate.
### Arguments

- *double* **lookahead** - Time value.

## Unigine:: CallbackBase * addCallback ( int callback , Unigine:: CallbackBase * func )

Adds a callback function of the specified type.
### Arguments

- *int* **callback** - Callback type. One of the [CALLBACK_*](#CALLBACK_DISCOVER_OBJECT_INSTANCE) variables.
- *Unigine::[CallbackBase](../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **func** - Callback pointer.

### Return value

Pointer to the added callback.
## void removeCallback ( int callback , Unigine:: CallbackBase * func )

Removes a specified callback function of the specified type.
### Arguments

- *int* **callback** - Callback type. One of the [CALLBACK_*](#CALLBACK_DISCOVER_OBJECT_INSTANCE) variables.
- *Unigine::[CallbackBase](../../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **func** - Callback pointer.

## void clearCallbacks ( int callback )

Clears all callback functions of the specified type.
### Arguments

- *int* **callback** - Callback type. One of the [CALLBACK_*](#CALLBACK_DISCOVER_OBJECT_INSTANCE) variables.

## int shutdown ( )

Shuts down the HLA Connector.
### Return value

1 if the HLA Connector was shut down successfully; otherwise, 0.
