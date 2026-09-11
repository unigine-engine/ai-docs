# Performance Analyzer


A console command is available for analyzing performance of the scripts and the engine.


- [world_analyze](../code/console/index.md#world_analyze)


Per-function analysis can be output into the console or logged to a file (if its name is specified as a command argument, for example:


```text
			world_analyze new_file.txt

```


## Logged Data


Data logged by the analyzer includes the following:


- *total seconds* � the total number of seconds the interpreter spent executing this function.
- *self seconds* � the number of seconds accounted for by this function alone, without internal calls of other functions.
- *calls* � the total number of times the function was called.
- *total ms/call* � the average number of milliseconds spent in this function and its descendants per call.
- *self ms/call* � the average number of milliseconds spent in this function per call.
- *name* � function name.
