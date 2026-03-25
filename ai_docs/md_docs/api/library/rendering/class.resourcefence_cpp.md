# Unigine::ResourceFence Class (CPP)

**Header:** #include <UnigineResourceFence.h>


This class allows managing the resource fence, an object that allows synchronizing the engine GPU thread and an external GPU thread.


> **Notice:** Fence synchronization is called implicitly by the engine, i.e. *ID3D12CommandQueue::Wait/ID3D12CommandQueue::Signal* (and similar for Vulkan using timeline semaphores) is called in **ID3D12CommandQueue::Wait - ID3D12CommandQueue::ExecuteCommandLists - ID3D12CommandQueue::Signal** order.
>
>
> For DX12, it is called in the Engine's Internal thread, while Vulkan implementation calls it from Engine's Main thread.
>
>
> Signal also increments values before signaling on the GPU.


## ResourceFence Class

### Members

---

## ResourceFence ( )

ResourceFence constructor. Resource fence is created as enabled by default. It is created in engine GPU thread and is to be manually imported to the external graphics API.
## void setEnabled ( bool enabled )

Toggles the resource fence on and off.
### Arguments

- *bool* **enabled** - true to enable the resource fence, false to disable it.

## bool isEnabled ( ) const

Returns the value indicating if the resource fence is enabled.
### Return value

true if the resource fence is enabled, otherwise false.
## void* getWin32Handle ( ) const

Returns the pointer to a variable that receives the NT HANDLE value to the resource to share. You can use this handle in calls to access the resource.
### Return value

Win32 handle. If called under Linux, returns nullptr.
## int getFdHandle ( ) const

Returns the file descriptor referencing the payload of the device memory object.
### Return value

Linux handle. If called under Windows, returns -1.
## unsigned long long getValue ( ) const

Returns the fence value (signal and wait value).
### Return value

The fence value.
## unsigned long long incrementValue ( )

Increments the fence value (signal and wait value).
### Return value

The fence value.
## void waitGPU ( )

This method ensures that all processes in the engine GPU thread are completed.
## void closeHandle ( )

Closes the handle. To avoid memory leaks, use this method when you no longer need the resource handle (for example, as soon as you imported the object to another graphics API).
