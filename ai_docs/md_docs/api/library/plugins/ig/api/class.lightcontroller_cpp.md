# Unigine::Plugins::IG::LightController Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


## LightController Class

### Members

---

## void setEnabled ( const Ptr < Node > & parent_node , const char * path , bool enable )

Enables or disables all lights of a given parent node within a specified [category](../../../../../ig/light.md#lights_hierarchy).
### Arguments

- *const [Ptr](../../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../../api/library/nodes/class.node_cpp.md)> &* **parent_node** - Parent node of lights to be enabled.
- *const char ** **path** - Category of lights in the [lights hierarchy](../../../../../ig/light.md#lights_hierarchy).
- *bool* **enable** - true to enable lights, false to disable.

## void setEnabled ( const char * path , bool enable )

Enables or disables all lights within a specified [category](../../../../../ig/light.md#lights_hierarchy).
### Arguments

- *const char ** **path** - Category of lights in the [lights hierarchy](../../../../../ig/light.md#lights_hierarchy).
- *bool* **enable** - true to enable lights, false to disable.

## void setEnabled ( Unigine:: Vector <unsigned int> & hash_path , bool enable )

Enables or disables all lights within a specified [category](../../../../../ig/light.md#lights_hierarchy) using its hash.
> **Notice:** Toggling lights using the path hash is faster than using categories, therefore, is recommended for use, where appropriate.


### Arguments

- *Unigine::[Vector](../../../../../api/library/containers/vector/class.vector_cpp.md)<unsigned int> &* **hash_path** - Hash of the category of lights in the [lights hierarchy](../../../../../ig/light.md#lights_hierarchy).
- *bool* **enable** - true to enable lights, false to disable.

## void setStrobed ( const char * path , bool enable )

Enables or disables lights strobing within a specified [category](../../../../../ig/light.md#lights_hierarchy).
### Arguments

- *const char ** **path** - Category of lights in the [lights hierarchy](../../../../../ig/light.md#lights_hierarchy).
- *bool* **enable** - true to enable strobing, false to disable.

## void setStrobed ( Unigine:: Vector <unsigned int> & hash_path , bool enable )

Enables or disables lights strobing within a specified [category](../../../../../ig/light.md#lights_hierarchy) using its hash.
### Arguments

- *Unigine::[Vector](../../../../../api/library/containers/vector/class.vector_cpp.md)<unsigned int> &* **hash_path** - Hash of the category of lights in the [lights hierarchy](../../../../../ig/light.md#lights_hierarchy).
- *bool* **enable** - true to enable strobing, false to disable.

## void setBright ( const char * path , float bright )

Sets the intensity of lights within a specified [category](../../../../../ig/light.md#lights_hierarchy).
### Arguments

- *const char ** **path** - Category of lights in the [lights hierarchy](../../../../../ig/light.md#lights_hierarchy).
- *float* **bright** - Light intensity value within the [0.0f; 1.0f] range.

## void setBright ( Unigine:: Vector <unsigned int> & hash_path , float bright )

Sets the intensity of lights within a specified [category](../../../../../ig/light.md#lights_hierarchy) using its hash.
### Arguments

- *Unigine::[Vector](../../../../../api/library/containers/vector/class.vector_cpp.md)<unsigned int> &* **hash_path** - Hash of the category of lights in the [lights hierarchy](../../../../../ig/light.md#lights_hierarchy).
- *float* **bright** - Light intensity value within the [0.0f; 1.0f] range.

## void getIndexPath ( const char * path , Unigine:: Vector <unsigned int> & ret_hash_path )

Fills in the vector data array with the path hash values.
### Arguments

- *const char ** **path** - Category of lights in the [lights hierarchy](../../../../../ig/light.md#lights_hierarchy).
- *Unigine::[Vector](../../../../../api/library/containers/vector/class.vector_cpp.md)<unsigned int> &* **ret_hash_path** - Pointer to the array storing hash of the path.
