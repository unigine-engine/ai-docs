# Unigine::Plugins::DataBridge::Manager Class (CPP)

**Header:** #include <plugins/Unigine/DataBridge/UnigineDataBridge.h>

> **Notice:** This class is a singleton.


This class controls the DataBridge plugin and provides access to variables.


## Manager Class

---

## NetworkManager * getNetworkManager ( )

Returns the Network Manager interface.
### Return value

Pointer to the Network Manager interface.
## DataBridgeUI * getDataBridgeUI ( )

Returns the DataBridge user interface.
### Return value

Pointer to DataBridge UI.
## DBVariable * getVariable ( const char * path )

Returns the DataBridge variable by its path.
### Arguments

- *const char ** **path** - Path to the variable.

### Return value

Pointer to the DataBridge variable.
## DBVariable * getVariable ( unsigned long long id )

Returns the DataBridge variable by its ID.
### Arguments

- *unsigned long long* **id** - Variable ID.

### Return value

Pointer to the DataBridge variable.
## DBVariable * getRootVariable ( ) const

Returns the root variable.
### Return value

Pointer to the DataBridge variable.
## DBVariable * createVariable ( const char * path , unsigned long long id )

Returns the variable created using the specified arguments.
### Arguments

- *const char ** **path** - Path to the variable.
- *unsigned long long* **id** - Variable ID.

### Return value

Pointer to the DataBridge variable.
## void queueVariableToRemove ( const char * path )

Marks the variable at the specified path for removal.
### Arguments

- *const char ** **path** - Path to the variable.

## void queueVariableToRemove ( unsigned long long id )

Marks the variable with the specified ID for removal.
### Arguments

- *unsigned long long* **id** - Variable ID.

## void queueVariableToRemove ( DBVariable * OUT_var )

Marks the variable for removal.
### Arguments

- *[DBVariable](../../../../api/library/plugins/databridge/class.dbvariable_cpp.md) ** **OUT_var** - DataBridge variable. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void removeQueuedVariables ( )

Deletes all the variables marked for removal by a **queueVariableToRemove** method.
## void setVariableInt32 ( const char * path , int val )

Sets an integer value for the variable at the specified path.
### Arguments

- *const char ** **path** - Path to the variable.
- *int* **val** - Integer value.

## void setVariableUInt32 ( const char * path , unsigned int val )

Sets an unsigned integer value for the variable at the specified path.
### Arguments

- *const char ** **path** - Path to the variable.
- *unsigned int* **val** - Unsigned integer value.

## void setVariableInt64 ( const char * path , long long val )

Sets a long long value for the variable at the specified path.
### Arguments

- *const char ** **path** - Path to the variable.
- *long long* **val** - Long long value.

## void setVariableUInt64 ( const char * path , unsigned long long val )

Sets an unsigned long long value for the variable at the specified path.
### Arguments

- *const char ** **path** - Path to the variable.
- *unsigned long long* **val** - Unsigned long long value.

## void setVariableFloat32 ( const char * path , float val )

Sets a floating point value for the variable at the specified path.
### Arguments

- *const char ** **path** - Path to the variable.
- *float* **val** - Floating point value.

## void setVariableFloat64 ( const char * path , double val )

Sets a double value for the variable at the specified path.
### Arguments

- *const char ** **path** - Path to the variable.
- *double* **val** - Double value.

## void setVariableString ( const char * path , const char * val )

Sets a string value for the variable at the specified path.
### Arguments

- *const char ** **path** - Path to the variable.
- *const char ** **val** - String value.

## void setVariableBlob ( const char * path , Ptr < Blob > & val )

Sets a blob value for the variable at the specified path.
### Arguments

- *const char ** **path** - Path to the variable.
- *[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../../api/library/common/class.blob_cpp.md)> &* **val** - Blob value.

## int getVariableInt32 ( const char * path )

Returns the integer value set for the variable at the specified path.
### Arguments

- *const char ** **path** - Path to the variable.

### Return value

Integer value.
## unsigned int getVariableUInt32 ( const char * path )

Returns the unsigned integer value set for the variable at the specified path.
### Arguments

- *const char ** **path** - Path to the variable.

### Return value

Unsigned integer value.
## long long getVariableInt64 ( const char * path )

Returns the long long value set for the variable at the specified path.
### Arguments

- *const char ** **path** - Path to the variable.

### Return value

Long long value.
## unsigned long long getVariableUInt64 ( const char * path )

Returns the unsigned long long value set for the variable at the specified path.
### Arguments

- *const char ** **path** - Path to the variable.

### Return value

Unsigned long long value.
## float getVariableFloat32 ( const char * path )

Returns the floating point value set for the variable at the specified path.
### Arguments

- *const char ** **path** - Path to the variable.

### Return value

Floating point value.
## double getVariableFloat64 ( const char * path )

Returns the double value set for the variable at the specified path.
### Arguments

- *const char ** **path** - Path to the variable.

### Return value

Double value.
## String getVariableString ( const char * path )

Returns the string value set for the variable at the specified path.
### Arguments

- *const char ** **path** - Path to the variable.

### Return value

String value.
## Ptr < Blob > getVariableBlob ( const char * path )

Returns the blob value set for the variable at the specified path.
### Arguments

- *const char ** **path** - Path to the variable.

### Return value

Blob value.
