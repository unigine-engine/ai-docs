# Unigine.StructuredBuffer Class (CS)


*StructuredBuffer* is a buffer for structures: it represents a uniform array of structures.


*StructuredBuffer* resource can be specified [via the following flags](../../../api/library/rendering/class.structuredbuffer_cs.md#USAGE_RENDER).


### See Also


- **StructuredBuffer** C++ sample provided in the Samples (*Samples -> C++ -> Render*) section of UNIGINE SDK Browser.


## StructuredBuffer Class

### Properties

## string DebugName

The friendly name of the structured buffer used for GPU debugging (RenderDoc, NVIDIA Nsight). It can be used to help you determine if the corresponding object interface pointer caused the leak. Memory leaks are reported by the [debug software layer](https://docs.microsoft.com/en-us/windows/desktop/direct3d11/overviews-direct3d-11-devices-layers#debug-layer) by outputting a list of object interface pointers along with their friendly names.
## 🔒︎ int NumElements

The number of elements in the structured buffer.
## 🔒︎ bool IsUsageShared

The value indicating if the resource has the [USAGE_SHARED](#USAGE_SHARED) flag enabled.
## 🔒︎ bool IsUsageStaging

The value indicating if the resource has the [USAGE_STAGING](#USAGE_STAGING) flag enabled.
## 🔒︎ bool IsUsageImmutable

The value indicating if the resource has the [USAGE_IMMUTABLE](#USAGE_IMMUTABLE) flag enabled.
## 🔒︎ bool IsUsageRender

The value indicating if the resource has the [USAGE_RENDER](#USAGE_RENDER) flag enabled.
### Members

---

## StructuredBuffer ( )

Constructor. Creates a new structured buffer.


```cpp
StructuredBufferPtr input_buffer = StructuredBuffer::create();
```


## void Clear ( )

Clears smart pointer.
## int Create ( int flags , IntPtr data , uint structure_size , uint num_elements )

Creates a StructuredBuffer instance with specified parameters.
### Arguments

- *int* **flags** - [StructuredBuffer flag](#USAGE_RENDER).
- *IntPtr* **data** - Pointer to the source data.
- *uint* **structure_size** - The size of the structured buffer.
- *uint* **num_elements** - Number of elements in the structured buffer.

### Return value

**1** if the StructuredBuffer was created successfully; otherwise, **0**.
## int Create ( int flags , uint structure_size , uint num_elements )

Creates a StructuredBuffer instance with specified parameters.
### Arguments

- *int* **flags** - [StructuredBuffer flag](#USAGE_RENDER).
- *uint* **structure_size** - The size of the structured buffer.
- *uint* **num_elements** - Number of elements in the structured buffer.

### Return value

**1** if the StructuredBuffer was created successfully; otherwise, **0**.
## void Destroy ( )

Destroys smart pointer.
## void ClearBuffer ( )

Clears the structured buffer.
## void Copy ( StructuredBuffer src )

Copies the data from the specified source structured buffer.
### Arguments

- *[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cs.md)* **src** - Source structured buffer to copy data from.

## ResourceExternalMemory GetResourceExternalMemory ( )

Returns the resource in video memory. If the [USAGE_SHARED](#USAGE_SHARED) flag is not enabled for the resource, this method returns NULL.
### Return value

The resource in video memory. If the [USAGE_SHARED](#USAGE_SHARED) flag is not enabled for the resource, this method returns NULL.
## ulong GetVideoMemoryUsage ( )

Returns the current amount of video memory used by the structured buffer.
### Return value

Video memory amount used by the structured buffer, in bytes.
