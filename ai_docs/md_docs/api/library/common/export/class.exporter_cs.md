# Unigine::Exporter Class (CS)


This class is used to manage a node exporter. Node exporters are used by the Engine's [export system](../../../../principles/export_system/index.md) to export UNIGINE�s nodes to files of different formats. A single exporter can be used to export multiple nodes, but **there shouldn't be two or more exporters [registered](../../../../api/library/common/export/class.export_cs.md#registerExporter_const_char_ptr_const_Vectortmplargs_ref_void) for a single node type**.


Each exporter has a set of parameters that control the whole export process (e.g., whether to export lights, cameras, and material normal maps, reset root node transformation, etc.). The exporter should be [initialized](../../../../api/library/common/export/class.exporter_cs.md#init_int) before the use.


> **Notice:** This is a base class for all exporters. Your custom exporter class must be inherited from it.


## Exporter Class

### Members

---

## Exporter ( )

Constructor. Creates an exporter with default settings.
## bool ContainsParameter ( string name )

Returns a value indicating whether the list of export parameters includes a parameter with a given name.
### Arguments

- *string* **name** - Parameter name.

### Return value

true if the list of export parameters includes a parameter with a given name; otherwise, false.
## void SetParameterInt ( string name , int v )

Sets a new value for the specified integer parameter.
### Arguments

- *string* **name** - Name of the integer parameter.
- *int* **v** - New value to be set.

## int GetParameterInt ( string name )

Returns the current value of the specified integer parameter.
### Arguments

- *string* **name** - Name of the integer parameter.

### Return value

Value of the integer parameter.
## void SetParameterFloat ( string name , float v )

Sets a new value for the specified float parameter.
### Arguments

- *string* **name** - Name of the float parameter.
- *float* **v** - New value to be set.

## float GetParameterFloat ( string name )

Returns the current value of the specified float parameter.
### Arguments

- *string* **name** - Name of the float parameter.

### Return value

Value of the float parameter.
## void SetParameterDouble ( string name , double v )

Sets a new value for the specified double parameter.
### Arguments

- *string* **name** - Name of the double parameter.
- *double* **v** - New value to be set.

## double GetParameterDouble ( string name )

Returns the current value of the specified double parameter.
### Arguments

- *string* **name** - Name of the double parameter.

### Return value

Value of the double parameter.
## void SetParameterString ( string name , string v )

Sets a new value for the specified string parameter.
### Arguments

- *string* **name** - Name of the string parameter.
- *string* **v** - New value to be set.

## string GetParameterString ( string name )

Returns the current value of the specified string parameter.
### Arguments

- *string* **name** - Name of the string parameter.

### Return value

Value of the string parameter.
## bool Init ( )

Initializes the exporter.
## bool Export ( Node root_node , string output_filepath )

Exports the node to the specified output file.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **root_node** - Root node of the hierarchy to be exported.
- *string* **output_filepath** - Output path to be used to store generated file(s) with exported data.
