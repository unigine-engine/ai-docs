# UUSL Compute Shaders


UUSL supports compute shaders: there are special functions, semantics and parameters for compute shaders.


In UNIGINE, compute shaders have a `*.comp` extension.


A compute shader is a special part of the graphics pipeline. It allows to execute code on the GPU, read and write buffer data.

 Prior KnowledgeThis article assumes you have prior knowledge of the compute shaders. Also, read the following topics on UUSL before proceeding:
- *[UUSL Data Types and Common Intrinsic Functions](../../code/uusl/types.md)*
- *[UUSL Textures](../../code/uusl/textures.md)*
- *[UUSL Semantics](../../code/uusl/semantics.md)*
- *[UUSL Parameters](../../code/uusl/parameters.md)*


## Main Function


To start and end the *void Main* function of the compute shader, use the following instructions:


```glsl
#include <core/materials/shaders/render/common.h>

MAIN_COMPUTE_BEGIN(WIDTH_GROUP,HEIGHT_GROUP)
	<your code here>
MAIN_COMPUTE_END

```


This code is equivalent to:


```glsl
#include <core/materials/shaders/render/common.h>

[numthreads(WIDTH_GROUP, HEIGHT_GROUP, 1)]
void main(DISPATCH_INFO dispatch_info) {
	<your code here>
}

```


## Semantics


| UUSL | Direct3D | Description |
|---|---|---|
| *GROUP_ID* | *SV_GroupID* | Contains the index of the workgroup currently being operated on by a compute shader |
| *GROUP_THREAD_ID* | *SV_GroupThreadID* | Contains the index of work item currently being operated on by a compute shader |
| *DISPATCH_THREAD_ID* | *SV_DispatchThreadID* | Contains the global index of work item currently being operated on by a compute shader |
| *GROUP_INDEX* | *SV_GroupIndex* | Contains the local linear index of work item currently being operated on by a compute shader |


![Image from learn.microsoft.com](threadgroupids.png)

*Image fromlearn.microsoft.com*


## Keywords


| UUSL | Direct3D | Description |
|---|---|---|
| *SHARED* | *groupshared* | Mark a variable for thread-group-shared memory for compute shaders |
| *MEMORY_BARRIER_SHARED* | *GroupMemoryBarrier()* | Blocks execution of all threads in a group until all group shared accesses have been completed |
| *MEMORY_BARRIER_SHARED_SYNC* | *GroupMemoryBarrierWithGroupSync()* | Blocks execution of all threads in a group until all group shared accesses have been completed and all threads in the group have reached this call |
