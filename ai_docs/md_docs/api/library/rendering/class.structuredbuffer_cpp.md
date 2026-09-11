# Unigine.StructuredBuffer Class (CPP)

**Header:** #include <UnigineTextures.h>


*StructuredBuffer* is a buffer for structures: it represents a uniform array of structures.


*StructuredBuffer* resource can be specified [via the following flags](../../../api/library/rendering/class.structuredbuffer_cpp.md#USAGE_RENDER).


### See Also


- **StructuredBuffer** C++ sample provided in the Samples (*Samples -> C++ -> Render*) section of UNIGINE SDK Browser.


## StructuredBuffer Class

### Members

## void setDebugName ( const char * name )

Sets a new friendly name of the structured buffer used for GPU debugging (RenderDoc, NVIDIA Nsight). It can be used to help you determine if the corresponding object interface pointer caused the leak. Memory leaks are reported by the [debug software layer](https://docs.microsoft.com/en-us/windows/desktop/direct3d11/overviews-direct3d-11-devices-layers#debug-layer) by outputting a list of object interface pointers along with their friendly names.
### Arguments

- *const char ** **name** - The friendly debug name.

## const char * getDebugName () const

Returns the current friendly name of the structured buffer used for GPU debugging (RenderDoc, NVIDIA Nsight). It can be used to help you determine if the corresponding object interface pointer caused the leak. Memory leaks are reported by the [debug software layer](https://docs.microsoft.com/en-us/windows/desktop/direct3d11/overviews-direct3d-11-devices-layers#debug-layer) by outputting a list of object interface pointers along with their friendly names.
### Return value

Current friendly debug name.
## int getNumElements () const

Returns the current number of elements in the structured buffer.
### Return value

Current number of elements in the structured buffer.
## bool isUsageShared () const

Returns the current value indicating if the resource has the [USAGE_SHARED](#USAGE_SHARED) flag enabled.
### Return value

**true** if the [USAGE_SHARED](#USAGE_SHARED) flag is enabled ; otherwise **false**.
## bool isUsageStaging () const

Returns the current value indicating if the resource has the [USAGE_STAGING](#USAGE_STAGING) flag enabled.
### Return value

**true** if the [USAGE_STAGING](#USAGE_STAGING) flag is enabled ; otherwise **false**.
## bool isUsageImmutable () const

Returns the current value indicating if the resource has the [USAGE_IMMUTABLE](#USAGE_IMMUTABLE) flag enabled.
### Return value

**true** if the [USAGE_IMMUTABLE](#USAGE_IMMUTABLE) flag is enabled ; otherwise **false**.
## bool isUsageRender () const

Returns the current value indicating if the resource has the [USAGE_RENDER](#USAGE_RENDER) flag enabled.
### Return value

**true** if the [USAGE_RENDER](#USAGE_RENDER) flag is enabled ; otherwise **false**.
---

## static StructuredBufferPtr create ( )

Constructor. Creates a new structured buffer.


```cpp
StructuredBufferPtr input_buffer = StructuredBuffer::create();
```


## void clear ( )

Clears smart pointer.
## int create ( int flags , const void * data , unsigned int structure_size , unsigned int num_elements )

Creates a StructuredBuffer instance with specified parameters.


```cpp
#define NUMBERS_COUNT 4096 * 8192

// Input data structure
struct InputDataStructure {
	vec4 vector0;
	vec4 vector1;
};

// Source data
InputDataStructure *source_data = new InputDataStructure[NUMBERS_COUNT];

// Create immutable structure buffer (gpu_read-only) and store initial values
StructuredBufferPtr input_buffer = StructuredBuffer::create();
input_buffer->create(StructuredBuffer::IMMUTABLE, source_data, sizeof(InputDataStructure), NUMBERS_COUNT);

```


### Arguments

- *int* **flags** - [StructuredBuffer flag](#USAGE_RENDER).
- *const void ** **data** - Pointer to the source data.
- *unsigned int* **structure_size** - The size of the structured buffer.
- *unsigned int* **num_elements** - Number of elements in the structured buffer.

### Return value

**1** if the StructuredBuffer was created successfully; otherwise, **0**.
## int create ( int flags , unsigned int structure_size , unsigned int num_elements )

Creates a StructuredBuffer instance with specified parameters.
### Arguments

- *int* **flags** - [StructuredBuffer flag](#USAGE_RENDER).
- *unsigned int* **structure_size** - The size of the structured buffer.
- *unsigned int* **num_elements** - Number of elements in the structured buffer.

### Return value

**1** if the StructuredBuffer was created successfully; otherwise, **0**.
## void destroy ( )

Destroys smart pointer.
## void clearBuffer ( )

Clears the structured buffer.
## void copy ( const Ptr < StructuredBuffer > & src )

Copies the data from the specified source structured buffer.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cpp.md)> &* **src** - Source structured buffer to copy data from.

## Ptr < ResourceExternalMemory > getResourceExternalMemory ( ) const

Returns the pointer to the resource in video memory. If the [USAGE_SHARED](#USAGE_SHARED) flag is not enabled for the resource, this method returns nullptr.
### Return value

The pointer to the resource in video memory. If the [USAGE_SHARED](#USAGE_SHARED) flag is not enabled for the resource, this method returns nullptr.
## size_t getVideoMemoryUsage ( )

Returns the current amount of video memory used by the structured buffer.
### Return value

Video memory amount used by the structured buffer, in bytes.
