# UnigineScript Interop

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/cpp-api-samples](https://github.com/unigine-engine/cpp-api-samples)**.


## Usc Arrays

This sample showcases integration between *C++* and *UnigineScript* by registering external *C++* functions that manipulate *UnigineScript* array types.


The registered functions allow for setting and getting values, generating test data, and enumerating the contents of both *[ArrayVector](../../../api/library/containers/class.arrayvector_cpp.md)* (indexed container) and *[ArrayMap](../../../api/library/containers/arraymap/class.arraymap_cpp.md)* (associative container).


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/unigine_script_interop/usc_arrays*
## Usc Callbacks

This sample demonstrates how to call *UnigineScript* functions from *C++* code via callbacks.


The mechanism is based on *[Variable](../../../api/library/common/class.variable_cpp.md)* Class instances and allows calling both custom and built-in script functions by name.


The sample registers a *C++* wrapper function to expose script invocation capability to *UnigineScript* via the *[Interpreter](../../../api/library/common/class.interpreter_cpp.md)* class.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/unigine_script_interop/usc_callbacks*
## Usc Classes

This sample demonstrates how to export classes from *C++* side to *UnigineScript*.


A simple *C++* class named *ExternClass* is used to export custom *MyExternObject* into the *UnigineScript* environment. This allows scripts to instantiate the class, call its methods, and interact with its properties at runtime.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/unigine_script_interop/usc_classes*
## Usc Functions

This sample demonstrates how to export functions from *C++* side to *UnigineScript*. It includes examples of exporting regular functions, handling multiple data types, and registering class members for a singleton-like object.
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/unigine_script_interop/usc_functions*

## Usc Inheritance

This sample demonstrates how to work with *UnigineScript* containers via *C++ API*. It showcases class composition, constructor registration, base-to-derived linkage, and virtual method exposure within a scripting context.


Each class in the hierarchy is registered via the *[Interpreter](../../../api/library/common/class.interpreter_cpp.md)* class, allowing scripts to instantiate and interact with derived types, call inherited methods, and override behavior.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/unigine_script_interop/usc_inheritance*
## Usc Stack

This sample demonstrates how to use a stack implemented via *C++* in *UnigineScript*.


The sample defines a simple formatter function on the *C++* side. This function takes a format string and substitutes tokens with values popped from a runtime stack. Values are passed from the script and pushed onto the stack prior to the call.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/unigine_script_interop/usc_stack*
## Usc Structures

This sample demonstrates how to expose *C++* structs to *UnigineScript* using the *[Interpreter](../../../api/library/common/class.interpreter_cpp.md)* class.


It defines a simple *C++* structure *MyVector* with four float fields (*x, y, z, w*) and registers it. Each field is mapped via explicit getter and setter methods to allow full read/write access from the *UnigineScript* side.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/unigine_script_interop/usc_structures*
## Usc Transfer

This sample demonstrates how to transfer complex data between *UnigineScript* and *C++* using the [Variable](../../../api/library/common/class.variable_cpp.md) class and the *TypeToVariable* utility.


The example shows several ways to pass and return [Image](../../../api/library/common/class.image_cpp.md) objects between script and native code. It compares direct object passing, conversion via *[Variable](../../../api/library/common/class.variable_cpp.md)*, and using *TypeToVariable*.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/unigine_script_interop/usc_transfer*
## Usc Types

This sample demonstrates how to enable type conversion between custom *C++* types and *UnigineScript* using the [Variable](../../../api/library/common/class.variable_cpp.md) class.


A user-defined *MyVector3* class is introduced to represent a *3D* vector. To integrate this class with the *UnigineScript* environment, custom specializations of the *TypeToVariable* and *VariableToType* templates are implemented. These allow automatic conversion between *MyVector3* and *vec3* values inside the *UnigineScript* runtime.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/unigine_script_interop/usc_types*
## Usc Variable

This sample demonstrates how to work with different variable types in *UnigineScript* using the *[Variable](../../../api/library/common/class.variable_cpp.md)* class from *C++* code.


Various types (*int, long, float, double*), and vector types (*vec3, vec4, dvec3*, etc.), are wrapped in *Variable* objects and passed into a *UnigineScript* callback function.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/unigine_script_interop/usc_variable*
