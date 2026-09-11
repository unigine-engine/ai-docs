# OS Functions (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## double clock ( )

Returns time in seconds (with microsecond precision) passed from the engine start-up. This function returns the time with the highest precision possible from the operating system.
### Return value

Time from the application start-up.
## StringStack<> date ( string format )

Returns a current date in the given format.
### Arguments

- *string* **format** - Date format. The following placeholders can be used to show a date:

  - **a**: abbreviated weekday name (e.g., Sun)
  - **b**: abbreviated month name (e.g., Jan)
  - **d**: date and time (e.g., Thu Feb 8, 00:51)
  - **s**: second (00..60)
  - **m**: minute (00..59)
  - **h**: hour (0..23)
  - **D**: day of month (e.g, 1)
  - **M**: month (1..12)
  - **Y**: year
  - **W**: day of week (0..6); 0 is Sunday
  - **%**: a literal percent character

### Return value

Current date in the given format.
## string date ( string format , long time )

Returns a current date and time in the given format. This function can receive a second argument with an Unix timestamp to be converted into a readable format.
### Arguments

- *string* **format** - Date [format](#date_string).
- *long* **time** - Unix time stamp to be converted. This is an optional argument.

### Return value

Current date and time in the given format.
### Examples


```cpp
log.message("%s\n",date("%d\nMonth is %M\nYear is %Y\nDay is %D %b, %a\n"));
log.message("%s\n",date("%2h:%02m:%02s %04Y",));

```


```text
Wed Mar 20, 16:11
Month is 3
Year is 2013
Day is 20 Mar, Wed

16:11:14 2013

```


## string getenv ( string name )

Gets a value of an environment variable.
### Arguments

- *string* **name** - Variable name.

### Return value

Variable value.
## Variable system ( string command , int wait = 1 )


Executes a shell command or commands.


> **Notice:** On Windows, this function returns **0** if the *wait* argument is **0**.


### Arguments

- *string* **command** - Command or commands to execute.
- *int* **wait** - Value indicating if the program should wait for completion of command execution: The value is required only on Windows.

  - 1 to wait for completion. This value is used by default.
  - 0 not to wait.

### Return value

Exit code of the last executed command if it was executed successfully; otherwise, **-1**.
### Examples


```cpp
// the following instruction will open a command prompt on Windows
system("cmd",1);

```


## int time ( )

Returns the time since the Epoch (00:00:00 UTC, January 1, 1970), measured in seconds.
### Return value

Number of seconds since 00:00:00, January 1, 1970.
