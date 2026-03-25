# Unigine::CPUTask Class (CS)


**CPUTask** is a single-threaded task that can be dispatched to any of the Engine's thread pools. Unlike **[CPUShader](../../../../api/library/common/mt/class.cpushader_cs.md)**, which distributes work across multiple threads, a CPUTask runs its *process()* method once on a single worker thread within the chosen pool.


Inherit from this class and override the pure virtual *process()* method to define your task logic, then call one of the *run*Thread()* methods to submit it to a specific pool.


## CPUTask Class

### Members

---

## CPUTask ( )

Default constructor.
