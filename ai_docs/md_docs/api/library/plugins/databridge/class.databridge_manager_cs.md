# Unigine::Plugins::DataBridge::Manager Class (CS)

> **Notice:** This class is a singleton.


This class controls the DataBridge plugin and provides access to variables.


## Manager Class

### Members

---

## NetworkManager GetNetworkManager ( )

Returns the Network Manager interface.
### Return value

Network Manager interface.
## DataBridgeUI GetDataBridgeUI ( )

Returns the DataBridge user interface.
### Return value

DataBridge UI.
## DBVariable GetVariable ( string path )

Returns the DataBridge variable by its path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

DataBridge variable.
## DBVariable GetVariable ( ulong id )

Returns the DataBridge variable by its ID.
### Arguments

- *ulong* **id** - Variable ID.

### Return value

DataBridge variable.
## DBVariable GetRootVariable ( )

Returns the root variable.
### Return value

DataBridge variable.
## DBVariable CreateVariable ( string path , ulong id )

Returns the variable created using the specified arguments.
### Arguments

- *string* **path** - Path to the variable.
- *ulong* **id** - Variable ID.

### Return value

DataBridge variable.
## void QueueVariableToRemove ( string path )

Marks the variable at the specified path for removal.
### Arguments

- *string* **path** - Path to the variable.

## void QueueVariableToRemove ( ulong id )

Marks the variable with the specified ID for removal.
### Arguments

- *ulong* **id** - Variable ID.

## void QueueVariableToRemove ( DBVariable [] OUT_var )

Marks the variable for removal.
### Arguments

- *[DBVariable](../../../../api/library/plugins/databridge/class.dbvariable_cs.md)[]* **OUT_var** - DataBridge variable. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void RemoveQueuedVariables ( )

Deletes all the variables marked for removal by a **QueueVariableToRemove** method.
## void SetVariableInt32 ( string path , int val )

Sets an integer value for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.
- *int* **val** - Integer value.

## void SetVariableUInt32 ( string path , uint val )

Sets an unsigned integer value for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.
- *uint* **val** - Unsigned integer value.

## void SetVariableInt64 ( string path , long val )

Sets a long long value for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.
- *long* **val** - Long long value.

## void SetVariableUInt64 ( string path , ulong val )

Sets an unsigned long long value for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.
- *ulong* **val** - Unsigned long long value.

## void SetVariableFloat32 ( string path , float val )

Sets a floating point value for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.
- *float* **val** - Floating point value.

## void SetVariableFloat64 ( string path , double val )

Sets a double value for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.
- *double* **val** - Double value.

## void SetVariableString ( string path , string val )

Sets a string value for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.
- *string* **val** - String value.

## void SetVariableBlob ( string path , Blob val )

Sets a blob value for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.
- *[Blob](../../../../api/library/common/class.blob_cs.md)* **val** - Blob value.

## int GetVariableInt32 ( string path )

Returns the integer value set for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

Integer value.
## uint GetVariableUInt32 ( string path )

Returns the unsigned integer value set for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

Unsigned integer value.
## long GetVariableInt64 ( string path )

Returns the long long value set for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

Long long value.
## ulong GetVariableUInt64 ( string path )

Returns the unsigned long long value set for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

Unsigned long long value.
## float GetVariableFloat32 ( string path )

Returns the floating point value set for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

Floating point value.
## double GetVariableFloat64 ( string path )

Returns the double value set for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

Double value.
## string GetVariableString ( string path )

Returns the string value set for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

String value.
## Blob GetVariableBlob ( string path )

Returns the blob value set for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

Blob value.
