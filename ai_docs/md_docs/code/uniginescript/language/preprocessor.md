# Preprocessor Directives

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


**Preprocessor directives** are special language constructs, which control the script interpreter behavior. All UnigineScript directives begin with the *#* sign, and each of them should be on its own line. Note that there are no semicolons at the end of strings that start with directives.


## Preprocessor Macros


A **macro** is a fragment of code which has been given a name. Whenever the name is used, it is replaced by the contents of the macro.


There is a pre-defined set of macros:

- **__VERSION__** - the UnigineScript interpreter version, for example, "1.82".
- **NDEBUG** - the binary does not contain debugging information (release build).
- **_WIN32** - target operating system is Windows.
- **_LINUX** - target operating system is Linux.
- **_ARCH_X86** - target operating system version is 32-bit.
- **_ARCH_X64** - target operating system version is 64-bit.
- **HAS_BLOB** - [Blob class](../../../api/library/common/class.blob_cpp.md) is available in the Core Library.
- **HAS_BOUNDS** - Bounds-related classes are available in the Core Library.
- **HAS_DIRECT3D11** - the binary is built with Direct3D 11 rendering system.
- **HAS_JOYSTICK** - the binary is built with support of a joystick.
- **HAS_IMAGE** - [Image class](../../../api/library/common/class.image_cpp.md) is available in the Core Library.
- **HAS_MESH** - [Mesh class](../../../api/library/rendering/class.mesh_cpp.md) is available in the Core Library.
- **HAS_MEMORY** - the binary is built with Unigine memory management system.
- **HAS_OPENAL** - the binary is built with OpenAL sound system.
- **HAS_OPENGL** - the binary is built with OpenGL rendering system.
- **HAS_OPENEXR** - the binary is built with support for the OpenEXR format.
- **HAS_PATH** - [Path class](../../../api/library/common/class.path_cpp.md) is available in the Core Library.
- **HAS_REGEXP** - [Regexp Class](../../../api/library/common/class.regexp_cpp.md) is available in the Core Library.
- **HAS_SIXAXIS** - the binary is built with support for a sixaxis controller.
- **HAS_SOCKET** - [Socket Class](../../../api/library/networking/class.socket_cpp.md) is available in the Core Library.
- **HAS_XAUDIO2** - the binary is built with XAudio2 sound system.
- **HAS_XML** - [Xml Class](../../../api/library/common/class.xml_cpp.md) is available in the Core Library.
- **HAS_XPAD360** - the binary is built with support for Xbox 360 gamepad.
- **HAS_ELLIPSOID** - the binary is built including the ellipsoid functionality.
- **USE_DOUBLE** - the binary is built with support for double precision of coordinates.
- **USE_GEODETICS** - the binary is built with support for geodetics.
- **USE_MICROPROFILE** - the binary is built with support of microprofile.


These macros can be used as conditions and combined with logical operators: *()* for grouping, *||* for "or", *&&* for "and".


## #include


Loads the content of a given file.


Syntax: *#include "someFile"*


Here *someFile* is a target file name.


```cpp
#include "foo.h"
foo(); // ok if foo.h contains declaration of foo()

```


To avoid conflicts it's recommended to include files this way:

```cpp
#ifndef __MYLIB_H__
#define __MYLIB_H__

#include "myLib.h"

#endif /* __MYLIB_H__ */

```

 In this case, even being included several times from different places, "myLib.h" will not cause re-definition collisions, since it will be compiled only once.
> **Notice:** If a base path to the file is not mentioned in the *#include* pragma, the file will be searched among all files located in the [data directory](../../../principles/filesystem/index_cpp.md#paths) of the project.


## #define


Sets an identifier and a character sequence, by which the identifier will be replaced in the text of the program.


Syntax: *#define macro_name character_sequence*


Here *macro_name* will be replaced with *character_sequence* everywhere in the code. Note that *character_sequence* shouldn't contain spaces (except for strings, which must be enclosed in double quotes) and can be omitted.


```cpp
#define LEFT 1
#define RIGHT 0

log.message("%d %d\n",LEFT,RIGHT);
// Output: 1 0

#define FRUIT "an apple"

log.message("%s\n", "today we will eat "FRUIT);
// Output: today we will eat an apple

// arguments are also supported:
#define saturate(v) clamp(v,0.0,1.0)

```


Inside the *#define* directive, the literal *#* operator can be used. It turns a macro argument into a string constant. This operator can also be used inside [templates](../../../code/uniginescript/language/templates.md).


Syntax: *#macro_arg*


Here *macro_arg* is an argument to a macro.


```cpp
#define assert(EXP) { if(EXP) { } else { throw("Assertion: '%s'",#EXP); } }
```


See also [Templates](../../../code/uniginescript/language/templates.md).


## #undef


Removes a previously defined identifier.


Syntax: *#undef macro_name*


```cpp
#define LOCK
#undef LOCK

#ifndef LOCK
log.message("unlocked\n"); // this fragment will be executed
#endif

```


## #ifdef


Allows executing some fragment of code conditionally, if a given identifier is defined with *#define*.


Syntax: *#ifdef macro_name*
 *some_code #endif*


If *macro_name* is defined, then *some_code* will be executed.


```cpp
#define LOCK1
#define LOCK2

#ifdef (LOCK1 && LOCK2) || LOCK3
log.message("locked\n"); // this fragment will be executed
#endif

```


## #ifndef


Allows executing some fragment of code conditionally, if a given identifier is not defined with *#define* or is undefined with *#undef*.


Syntax: *#ifndef macro_name*
 *some_code #endif*


If *macro_name* is not defined, then *some_code* will be executed.


```cpp
#define LOCK

#ifndef LOCK
log.message("unlocked\n"); // this fragment will NOT be executed
#endif

```


## #else


Creates an alternative to *#ifdef* and *#ifndef* pragmas.


Syntax: *#ifdef macro_name some_code*
 *#else some_more_code*
 *#endif*


Here *#ifndef* can be used instead of *#ifdef* (however, the meaning of the condition will be reversed). If the first condition is false, then everything from the first *#else* up to the first *#endif* will be executed.


```cpp
#define SOUND_ENABLE

#ifdef SOUND_ENABLE
log.message("sound enabled\n");
#else
log.message("sound disabled\n"); // this fragment will be executed
#endif

```


## #elif


Create a conditional alternative to *#ifdef* and *#ifndef* pragmas.


Syntax: *#ifdef macro_name1 some_code1*
 *#elif macro_name2 some_code2*
 *#endif*


Here *#ifndef* can be used instead of *#ifdef* (however, the meaning of the condition will be reversed). If *macro_name1* is false, then *macro_name2* is tested, and if it's true, everything from this *#elif* up to the first *#elif*, *#else* or *#endif* will be executed.


```cpp
#define VAL2

#ifdef VAL1
log.message("it is 1\n");
#elif VAL2
log.message("it is 2\n"); // this fragment will be executed
#elif VAL3
log.message("it is 3\n");
#endif

```


## #endif


Marks an end of conditional compilation.


## #error


Terminates execution of the script and logs the message into the console and a system log file.


Syntax: *#error message_text*


```cpp
#error I don't want to execute it any longer
```


## #warning


Logs the message into the console and a system log file, the script continues execution.


Syntax: *#warning message_text*


```cpp
#warning There is somethings wrong in here
```


## #warn_long


Terminates compilation if a variable of a [long](../../../code/uniginescript/language/data_types.md#long) type is used in the script, and logs the error message into the console and a system log file.


## #warn_double


Terminates compilation if a variable of a [double](../../../code/uniginescript/language/data_types.md#double) type is used in the script, and logs the error message into the console and a system log file.


## #no_long


Replaces all variables of a [long](../../../code/uniginescript/language/data_types.md#long) type in the script with an [int](../../../code/uniginescript/language/data_types.md#int) type.


## #no_double


Replaces all variables of a [double](../../../code/uniginescript/language/data_types.md#double) type in the script with a [float](../../../code/uniginescript/language/data_types.md#float) type.
