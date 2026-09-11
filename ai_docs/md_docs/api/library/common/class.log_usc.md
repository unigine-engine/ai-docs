# Unigine::Log Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class represents an interface for printing various types of messages to the [console](../../../code/console/index.md) and to the Engine's log file. It can be useful to monitor overall progress of application execution and report errors which can be helpful in the process of debugging.


> **Notice:** To enable displaying system messages in the Console use the following command: [`console_onscreen 1`](../../../code/console/index.md#console_onscreen)


There are two custom color schemes highlighting log syntax for Notepad++ included in the SDK:


- `<SDK>/utils/log_styles/notepad_light.xml`
- `<SDK>/utils/log_styles/notepad_dark.xml`


> **Notice:** By default all logged messages are saved to the Engine's log file, and printed to stdout, the latter **may significantly affect peformance** in case of much logging. If logging causes performance issues, you can control the two logging targets via the following console commands:
> - [`log_stdout`](../../../code/console/index.md#log_stdout)
> - [`log_file`](../../../code/console/index.md#log_file)


### Example


The following code demonstrates how to print various types of messages.


### Handling Events


## Log Class

### Members

## void setDialogFatalEnabled ( int enabled )

Sets a new value indicating if displaying *Fatal* dialog messages is enabled (when disabled, the corresponding message will be printed to the log).
Can be used, for example, to disable when running console tools like *[Runtimes Generator](../../../tools/runtimes_generator/index.md)* or *[Build Tool](../../../editor2/projects/build_project.md#console_build)* (use the `-dialog_fatal_enabled` command).


> **Notice:** Available for Windows OS only.

### Arguments

- *int* **enabled** - The displaying *Fatal* dialog messages

## int isDialogFatalEnabled () const

Returns the current value indicating if displaying *Fatal* dialog messages is enabled (when disabled, the corresponding message will be printed to the log).
Can be used, for example, to disable when running console tools like *[Runtimes Generator](../../../tools/runtimes_generator/index.md)* or *[Build Tool](../../../editor2/projects/build_project.md#console_build)* (use the `-dialog_fatal_enabled` command).


> **Notice:** Available for Windows OS only.

### Return value

Current displaying *Fatal* dialog messages
## getEventMessage () const

The event handler signature is as follows: *myhandler()*
### Return value

Event instance.
## getEventWarning () const

The event handler signature is as follows: *myhandler()*
### Return value

Event instance.
## getEventError () const

The event handler signature is as follows: *myhandler()*
### Return value

Event instance.
## getEventFatal () const

> **Notice:** Available for Windows OS only.

The event handler signature is as follows: *myhandler()*
### Return value

Event instance.
---

## void log.error ( string format , ... )

Prints an error message to the console and the log file.
### Arguments

- *string* **format** - Error message to print.
- *...*  - Arguments, multiple allowed.

## void log.fatal ( string format , ... )

Prints a fatal error message to the log file and quits the engine.

> **Notice:** Available for Windows OS only.

### Arguments

- *string* **format** - Fatal error message to print.
- *...*  - Arguments, multiple allowed.

## void log.message ( string format , ... )

Prints a message to the console and the log file.
### Arguments

- *string* **format** - Message to print.
- *...*  - Arguments, multiple allowed.

## void log.warning ( string format , ... )

Prints a warning to the console and the log file.
### Arguments

- *string* **format** - Warning to print.
- *...*  - Arguments, multiple allowed.
