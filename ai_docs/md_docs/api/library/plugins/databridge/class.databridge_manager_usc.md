# Unigine::Plugins::DataBridge::Manager Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This class controls the DataBridge plugin and provides access to variables.


## Manager Class

---

## NetworkManager getNetworkManager ( )

Returns the Network Manager interface.
### Return value

Network Manager interface.
## DataBridgeUI getDataBridgeUI ( )

Returns the DataBridge user interface.
### Return value

DataBridge UI.
## DBVariable getVariable ( string path )

Returns the DataBridge variable by its path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

DataBridge variable.
## DBVariable getVariable ( long id )

Returns the DataBridge variable by its ID.
### Arguments

- *long* **id** - Variable ID.

### Return value

DataBridge variable.
## DBVariable getRootVariable ( )

Returns the root variable.
### Return value

DataBridge variable.
## DBVariable createVariable ( string path , long id )

Returns the variable created using the specified arguments.
### Arguments

- *string* **path** - Path to the variable.
- *long* **id** - Variable ID.

### Return value

DataBridge variable.
## void queueVariableToRemove ( string path )

Marks the variable at the specified path for removal.
### Arguments

- *string* **path** - Path to the variable.

## void queueVariableToRemove ( long id )

Marks the variable with the specified ID for removal.
### Arguments

- *long* **id** - Variable ID.

## void queueVariableToRemove ( DBVariable * OUT_var )

Marks the variable for removal.
### Arguments

- *[DBVariable](../../../../api/library/plugins/databridge/class.dbvariable_usc.md) ** **OUT_var** - DataBridge variable. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void removeQueuedVariables ( )

Deletes all the variables marked for removal by a **queueVariableToRemove** method.
## void setVariableInt32 ( string path , int val )

Sets an integer value for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.
- *int* **val** - Integer value.

## void setVariableUInt32 ( string path , unsigned int val )

Sets an unsigned integer value for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.
- *unsigned int* **val** - Unsigned integer value.

## void setVariableInt64 ( string path , long val )

Sets a long long value for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.
- *long* **val** - Long long value.

## void setVariableUInt64 ( string path , long val )

Sets an unsigned long long value for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.
- *long* **val** - Unsigned long long value.

## void setVariableFloat32 ( string path , float val )

Sets a floating point value for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.
- *float* **val** - Floating point value.

## void setVariableFloat64 ( string path , double val )

Sets a double value for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.
- *double* **val** - Double value.

## void setVariableString ( string path , String val )

Sets a string value for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.
- *String* **val** - String value.

## void setVariableBlob ( string path , Blob & val )

Sets a blob value for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.
- *[Blob](../../../../api/library/common/class.blob_usc.md) &* **val** - Blob value.

## int getVariableInt32 ( string path )

Returns the integer value set for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

Integer value.
## unsigned int getVariableUInt32 ( string path )

Returns the unsigned integer value set for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

Unsigned integer value.
## long getVariableInt64 ( string path )

Returns the long long value set for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

Long long value.
## long getVariableUInt64 ( string path )

Returns the unsigned long long value set for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

Unsigned long long value.
## float getVariableFloat32 ( string path )

Returns the floating point value set for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

Floating point value.
## double getVariableFloat64 ( string path )

Returns the double value set for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

Double value.
## String getVariableString ( string path )

Returns the string value set for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

String value.
## Blob getVariableBlob ( string path )

Returns the blob value set for the variable at the specified path.
### Arguments

- *string* **path** - Path to the variable.

### Return value

Blob value.
