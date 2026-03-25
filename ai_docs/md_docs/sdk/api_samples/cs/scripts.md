# UnigineScript Interop

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/csharp-component-samples](https://github.com/unigine-engine/csharp-component-samples)**.


## Usc Arrays

This sample showcases integration between *C#* and *UnigineScript* by registering external *C#* functions that manipulate *UnigineScript* array types.


The registered functions allow for setting and getting values, generating test data, and enumerating the contents of both *[ArrayVector](../../../api/library/containers/class.arrayvector_cpp.md)* (indexed container) and *[ArrayMap](../../../api/library/containers/arraymap/class.arraymap_cpp.md)* (associative container).


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/unigine_script_interop/usc_arrays*
## Usc Callbacks

This sample demonstrates how to call *UnigineScript* functions from *C#* code via callbacks.


The mechanism is based on *[Variable](../../../api/library/common/class.variable_cpp.md)* Class instances and allows calling both custom and built-in script functions by name. The sample registers a *C#* wrapper function to expose script invocation capability to *UnigineScript* via the *[Interpreter](../../../api/library/common/class.interpreter_cpp.md)* class.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/unigine_script_interop/usc_callbacks*
## Usc Variables

This sample demonstrates how to work with different variable types in *UnigineScript* using the *[Variable](../../../api/library/common/class.variable_cpp.md)* class from *C#* code.


Various types (*int, long, float, double*), and vector types (*vec3, vec4, dvec3*, etc.), are wrapped in *Variable* objects and passed into a *UnigineScript* callback function.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/unigine_script_interop/usc_variables*
