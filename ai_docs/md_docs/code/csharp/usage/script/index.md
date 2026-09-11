# UnigineScript Extension Examples for C

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


UnigineScript can be easily extended through the Unigine API. Source code of examples is provided within source and binary versions of UNIGINE SDK.


The idea is that some functionality is done by means of the C# part of an application, and it should be registered in UnigineScript system in order to be used inside scripts.


You can export functions from your C# code to UnigineScript. The exported function can have up to **8** arguments. However, you cannot export classes. The function that is written in C# and must be exported to UnigineScript can receive arguments of the *Variable* type only. To get a value of the required type, use the corresponding getter functions. You can also work with UnigineScript containers from the C# side. On the C# side, vectors and maps can be accessed via the *ArrayVector* and *ArrayMap* classes.


For more information see common usage examples:


- [Callbacks](../../../../code/csharp/usage/script/callbacks.md)
- [Variable Export](../../../../code/csharp/usage/script/variables.md)
- [UnigineScript Containers](../../../../code/csharp/usage/script/arrays.md)
