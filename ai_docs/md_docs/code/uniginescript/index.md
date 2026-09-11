# UnigineScript

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


UnigineScript is a programming language used in UNIGINE engine and introduced by UNIGINE for optimizing a project creation process. It is similar to C++ in syntax, but includes some additional features.


You can read [more](../../code/uniginescript/language/features.md#diff) about syntactical differences between UnigineScript and C++.


The purpose of UnigineScript is to make coding easy-to-use even for junior programmers and at once provide the most optimal engine usage.


### Why use UnigineScript?


- Close to zero compile time, therefore increased iteration speed
- [Automatic memory manager with garbage collection](../../code/uniginescript/memory_management.md)
- [Object-oriented programming](../../code/uniginescript/language/oop.md)
- Built-in fast 3D mathematics
- Easy interaction with C++ code
- [Large built-in library (more than 5000 functions)](../../api/index.md)


All the features of UNIGINE engine are accessible via UnigineScript.


### Which platforms have UnigineScript?


Platforms supported by UNIGINE engine (Windows and Linux), no recompilation is required.


### What does a UnigineScript program creating process look like?


UnigineScript program can be written by using a plain text editor.


There are two ways of running UnigineScript programs:


- Via the built-in UnigineScript runtime (by running an engine instance)
- Via any standalone CLI interpreter ([usc](../../tools/usc/index.md)) � the same way as `.bat/.sh/.py` scripts work


### How do I get started with UnigineScript?


First, you have to learn how to program in UnigineScript. Read [The Language](../../code/uniginescript/language/index.md) information and try [tutorial](../../code/uniginescript/add_scripts/index.md). You probably will need information about core and engine libraries, [High-Level Script](../../code/uniginescript/scripts/index.md) and [Script Debugging](../../code/uniginescript/language/debugging.md) for extended UnigineScript features.


Learn about UnigineScript Programming Language, find out how to start writing programs in UnigineScript, work through the information, and get from Novice to Expert.


## Articles in This Section

- [Creating UnigineScript Application](../../code/uniginescript/application.md)

- [Adding Scripts to the Project](../../code/uniginescript/add_scripts/index.md)

- [The Language](../../code/uniginescript/language/index.md)

  - [Structure of a Program](../../code/uniginescript/language/structure.md)
  - [Data Types](../../code/uniginescript/language/data_types.md)
  - [Operators](../../code/uniginescript/language/operators.md)
  - [Control Statements](../../code/uniginescript/language/control_statements/index.md)

    - [Selection Statements](../../code/uniginescript/language/control_statements/selection_statements/index.md)

      - [if-else](../../code/uniginescript/language/control_statements/selection_statements/if_else.md)
      - [switch-case](../../code/uniginescript/language/control_statements/selection_statements/switch_case.md)
    - [Iteration Statements](../../code/uniginescript/language/control_statements/iteration_statements/index.md)

      - [for](../../code/uniginescript/language/control_statements/iteration_statements/for.md)
      - [while](../../code/uniginescript/language/control_statements/iteration_statements/while.md)
      - [do-while](../../code/uniginescript/language/control_statements/iteration_statements/do_while.md)
      - [forloop](../../code/uniginescript/language/control_statements/iteration_statements/forloop.md)
      - [foreach](../../code/uniginescript/language/control_statements/iteration_statements/foreach.md)
      - [foreachkey](../../code/uniginescript/language/control_statements/iteration_statements/foreachkey.md)
    - [Jump Statements](../../code/uniginescript/language/control_statements/jump_statements/index.md)

      - [return](../../code/uniginescript/language/control_statements/jump_statements/return.md)
      - [goto](../../code/uniginescript/language/control_statements/jump_statements/goto.md)
      - [break](../../code/uniginescript/language/control_statements/jump_statements/break.md)
      - [continue](../../code/uniginescript/language/control_statements/jump_statements/continue.md)
    - [Other Statements](../../code/uniginescript/language/control_statements/other_statements/index.md)

      - [yield](../../code/uniginescript/language/control_statements/other_statements/yield.md)
      - [wait](../../code/uniginescript/language/control_statements/other_statements/wait.md)
      - [call()](../../code/uniginescript/language/control_statements/other_statements/call.md)
      - [thread()](../../code/uniginescript/language/control_statements/other_statements/thread.md)
  - [Containers](../../code/uniginescript/language/containers/index.md)
  - [Functions](../../code/uniginescript/language/functions.md)
  - [Scope. Namespaces](../../code/uniginescript/language/scope.md)
  - [Object Oriented Programming](../../code/uniginescript/language/oop.md)
  - [Interface Class](../../code/uniginescript/language/class_interface.md)
  - [Preprocessor Directives](../../code/uniginescript/language/preprocessor.md)
  - [Templates](../../code/uniginescript/language/templates.md)
  - [Language Features](../../code/uniginescript/language/features.md)
  - [System Functions (USC)](../../api/library/common/class.system_usc.md)
  - [String Global Functions (USC)](../../code/uniginescript/language/strings_global_usc.md)

- [Script Debugging](../../code/uniginescript/language/debugging.md)

- [Handling Ownership When Using Scripts](../../code/uniginescript/memory_management.md)

- [High-Level Systems](../../code/uniginescript/scripts/index.md)

  - [UnigineScript Basic Utilities (USC)](../../code/uniginescript/scripts/utility/unigine_usc.md)
  - [Unigine::Widgets](../../code/uniginescript/scripts/systems/unigine_widgets/index.md)

    - [User Interfaces for Unigine::Widgets](../../code/uniginescript/scripts/systems/unigine_widgets/unigine_widgets_interface.md)
  - [Input System](../../code/uniginescript/scripts/input.md)
  - [Dialogs Script](../../code/uniginescript/scripts/dialogs.md)

- [Samples](../../code/uniginescript/samples/index.md)

- [Cache Files](../../code/uniginescript/cache.md)
