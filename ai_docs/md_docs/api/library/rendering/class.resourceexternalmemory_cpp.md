# Unigine::ResourceExternalMemory Class (CPP)

**Header:** #include <UnigineResourceExternalMemory.h>


This class is designed for interaction with the external memory objects.


## ResourceExternalMemory Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **TYPE_UNKNOWN** = 0 | The resource type is unknown. |
| **TYPE_TEXTURE** = 1 | The resource type is texture. |
| **TYPE_STRUCTURED_BUFFER** = 2 | The resource type is structured buffer. |
| **TYPE_MESH_DYNAMIC_VERTEX_BUFFER** = 3 | The resource type is vertex buffer of mesh dynamic. |
| **TYPE_MESH_DYNAMIC_INDEX_BUFFER** = 4 | The resource type is index buffer of mesh dynamic. |

### Members

---

## void* getWin32Handle ( ) const

Returns the pointer to a variable that receives the NT HANDLE value to the resource to share. You can use this handle in calls to access the resource.
### Return value

Win32 handle. If called under Linux, returns nullptr.
## int getFdHandle ( ) const

Returns the file descriptor referencing the payload of the device memory object.
### Return value

Linux handle. If called under Windows, returns -1.
## ResourceExternalMemory::TYPE getType ( ) const

Returns the type of the object for which resource external memory is created.
### Return value

The type of the object for which resource external memory is created.
## unsigned long long getSize ( ) const

Returns the size of video memory occupied by the resource.
### Return value

Size of video memory occupied by the resource, in bytes.
## void closeHandle ( )

Closes the handle. To avoid memory leaks, use this method when you no longer need the resource handle (for example, as soon as you imported the object to another graphics API).
