# C# API Reference


Most functions and classes in C# API have the same names and behavior as [in C++ API](../../../api/index.md). The main specific features of C# API are the following:


- Names of all methods in C# start with a capital letter.
- All C++ setters and getters are represented by properties in C#.
- In the C# API, you can inherit from *Package* and *Plugin* classes only once.


## Special Aspects of Pointers


You should take into account that each class of C# API has methods for managing pointers:


- *IntPtr GetPtr();* � returns the internal pointer.
- *bool IsValidPtr { get; }* � returns false if the native object has been destroyed.
- *bool IsNullPtr { get; }* � returns true if the native object has been destroyed.
- *void DeleteLater();* � destroys the native object.


Pointers are managed in the same way as in C++.


## Differences in Function Exporting


To export your function from C# to UnigineScript, you should use *Interpreter.Function()* with different postfixes instead of *MakeExternFunction()*. The postfix of Function shows the number of arguments (up to **8** arguments) and the type of return value:


- **no postfix** - void.
- **i** - int.
- **d** - double.
- **f** - float.
- **s** - string.
- **v** - *Unigine.Variable* (the same class as the *[C++ API Unigine::Variable](../../../api/library/common/class.variable_cpp.md)* class).


See also an [example](../../../code/csharp/usage/script/arrays.md) of function exporting.


## View Documentation by Using Visual Studio


You can read the documentation of some C# API methods by using the Object Browser in Visual Studio.


1. In Visual Studio, click *View -> Object Browser* or press **CTRL + W** and then **J**. ![](1_ref_object_browser.png) The Object Browser window will open. The Object Browser displays three panes: the *Objects* pane on the left, the *Members* pane on the top right, and the *Description* pane on the bottom right. ![](1_object_browser_d_sm.png)
2. Select the **UnigineSharp_x64d** object in the *Object* pane and choose the class you want to view. ![](1_class_choose.png)
3. Specify the member in the *Members* pane.
4. If the description for the selected member exists, it will appear in the *Description* pane.


## See Also


- Article on [*C++ API Reference*](../../../api/index.md).
