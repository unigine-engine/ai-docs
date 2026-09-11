# Unigine::Exporter Class (CPP)

**Header:** #include <UnigineExport.h>


This class is used to manage a node exporter. Node exporters are used by the Engine's [export system](../../../../principles/export_system/index.md) to export UNIGINE�s nodes to files of different formats. A single exporter can be used to export multiple nodes, but **there shouldn't be two or more exporters [registered](../../../../api/library/common/export/class.export_cpp.md#registerExporter_const_char_ptr_const_Vectortmplargs_ref_void) for a single node type**.


Each exporter has a set of parameters that control the whole export process (e.g., whether to export lights, cameras, and material normal maps, reset root node transformation, etc.). The exporter should be [initialized](../../../../api/library/common/export/class.exporter_cpp.md#init_int) before the use.


> **Notice:** This is a base class for all exporters. Your custom exporter class must be inherited from it.


## Exporter Class

---

## Exporter ( )

Constructor. Creates an exporter with default settings.
## int containsParameter ( const char* name ) const

Returns a value indicating whether the list of export parameters includes a parameter with a given name.
### Arguments

- *const char** **name** - Parameter name.

### Return value

true if the list of export parameters includes a parameter with a given name; otherwise, false.
## void setParameterInt ( const char* name , int v )

Sets a new value for the specified integer parameter.
### Arguments

- *const char** **name** - Name of the integer parameter.
- *int* **v** - New value to be set.

## int getParameterInt ( const char* name ) const

Returns the current value of the specified integer parameter.
### Arguments

- *const char** **name** - Name of the integer parameter.

### Return value

Value of the integer parameter.
## void setParameterFloat ( const char* name , float v )

Sets a new value for the specified float parameter.
### Arguments

- *const char** **name** - Name of the float parameter.
- *float* **v** - New value to be set.

## float getParameterFloat ( const char* name ) const

Returns the current value of the specified float parameter.
### Arguments

- *const char** **name** - Name of the float parameter.

### Return value

Value of the float parameter.
## void setParameterDouble ( const char* name , double v )

Sets a new value for the specified double parameter.
### Arguments

- *const char** **name** - Name of the double parameter.
- *double* **v** - New value to be set.

## double getParameterDouble ( const char* name ) const

Returns the current value of the specified double parameter.
### Arguments

- *const char** **name** - Name of the double parameter.

### Return value

Value of the double parameter.
## void setParameterString ( const char* name , const char* v )

Sets a new value for the specified string parameter.
### Arguments

- *const char** **name** - Name of the string parameter.
- *const char** **v** - New value to be set.

## const char* getParameterString ( const char* name ) const

Returns the current value of the specified string parameter.
### Arguments

- *const char** **name** - Name of the string parameter.

### Return value

Value of the string parameter.
## int init ( )

Initializes the exporter.
## int doExport ( const NodePtr& root_node , const char* output_filepath )


Exports the node to the specified output file.


> **Notice:** To customize actions to be performed on node export processing you can override the *[onExport()](#onExport_const_NodePtr_ref_const_char_ptr_bool)* method.


### Arguments

- *const NodePtr&* **root_node** - Root node of the hierarchy to be exported.
- *const char** **output_filepath** - Output path to be used to store generated file(s) with exported data.

## void deinit ( )

Uninitializes the exporter.
## bool onInit ( )

Initializes the exporter. This function is called each time when the *[init()](#init_int)* function is called. You can specify your custom actions to be performed on exporter initialization.
## bool onExport ( const NodePtr& root_node , const char* output_filepath )

Node export processing event handler function. This function is called each time when the *[doExport()](#doExport_const_NodePtr_ref_const_char_ptr_int)* function is called. You can specify your custom actions to be performed on node export processing.
### Arguments

- *const NodePtr&* **root_node** - Root node of the hierarchy to be exported.
- *const char** **output_filepath** - Output path to be used to store generated file(s) with exported data.

### Return value

true if export operation for the specified output path was successful; otherwise, false.
## void onDeinit ( )

Uninitializes the exporter. This function is called each time when the *[deinit()](#deinit_void)* function is called. You can specify your custom actions to be performed on exporter uninitialization.
