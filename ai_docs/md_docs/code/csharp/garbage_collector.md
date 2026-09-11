# Garbage Collector


The **Garbage Collector** (GC) represents an automatic memory manager responsible for allocation and release of memory for an application. So, developers working with managed code don't have to think about memory management tasks, and write any specific code for this purpose. Automatic memory management helps eliminate common problems, such as forgetting to free an object and causing a memory leak or attempting to access memory for an object that's already been freed.


Here are the benefits the Garbage Collector provides:


- Frees developers from having to release memory manually.
- Efficiently allocates objects on the managed heap.
- Reclaims objects that are no longer used, clears their memory, keeping the memory available for future allocations. Managed objects automatically get clean content to start with, so you don't have to initialize each and every data field in their constructors.
- Provides memory safety making sure that the content of an object cannot be used by another object.


## Garbage Collection Modes


UNIGINE's Garbage Collector offers you the following set of modes (*Engine.GCMode*) making the process of garbage collection management flexible:


- **DEFAULT** (default) - default C# garbage collector mode. In this case heavy spikes and excessive memory consumption are imminent if you don�t manage your objects properly and do not use the *Dispose()* method.
- **USE_MEMORY_PRESSURE** - passes the information about C++ memory consumption to C#. This results in more frequent GC calls preventing the application from eating too much memory right after startup and removing heavy spikes.
- **EVERY_FRAME** - the garbage collector is called every frame. This results in overall performance reduction, but removes heavy spikes.
- **WORLD_SHUTDOWN** - the garbage collector is called on closing the world. This mode is ideal if the number of memory allocations is your code is insignificant.


You can set Garbage Collector's mode in the *[*SystemLogic::Init()*](../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic_init)* method or anywhere in your code, and you can change it when necessary, depending on the current situation. It is also safe to do it in your C# components.


```csharp
class UnigineApp
{
  class AppSystemLogic : SystemLogic
  {
    // ...

    public override bool Init()
    {
      Engine.GCMode = Engine.GCMODE.EVERY_FRAME;
      // ...
      return true;
    }
    // ...
}

```
