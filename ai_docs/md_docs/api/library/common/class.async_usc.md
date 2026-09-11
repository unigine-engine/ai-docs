# Async Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


### See Also


A set of UnigineScript API samples:


-
-
-
-
-
-
-
-


## Async Class

### Members

---

## int setPriority ( int p )

Sets the priority for the thread.
### Arguments

- *int* **p** - Priority of the thread: > **Notice:** If the value is higher than 3, 3 will be passed; if the value is lower than -3, -3 will be passed.

  - **0** - normal
  - **1** - above normal
  - **-1** - below normal
  - **2** - high
  - **-2** - low
  - **3** - maximum
  - **-3** - minimum

### Return value

1 if the priority is set successfully; otherwise - 0.
## int getPriority ( )

Returns the priority of the thread.
### Return value

Priority of the thread:


- **0** - normal
- **1** - above normal
- **-1** - below normal
- **2** - high
- **-2** - low
- **3** - maximum
- **-3** - minimum


## int getQueue ( )

Returns the number of queued async threads.
### Return value

The number of queued threads.
## variable getResult ( int id )

Returns the function result.
### Arguments

- *int* **id**

### Return value

The function result.
## int isRunning ( )

Indicates if any thread is active.
### Return value

**1** if there is an active thread, otherwise - **0**.
## int isRunning ( int id )

Indicates if the required thread is active.
### Arguments

- *int* **id** - Thread ID.

### Return value

**1** if the required thread is active; otherwise - **0**.
## Async ( )

Default constructor. An empty instance with default parameters is created.
## void clearQueue ( )

Clears all the queued async threads.
## void clearResult ( )

Clears all the functions results.
## void lock ( )

Locks the resource. The resource can be locked by the other thread only after the first thread have [unlocked](#unlock_void) this resource.
## int run ( variable name )

Runs the given function in asynchronous way.
### Arguments

- *variable* **name** - Function to be run: *string* - function name, *int* - function ID. > **Notice:** You can also pass an ID of the external class method that can be obtained via [*functionid()*](../../../api/library/common/class.system_usc.md#functionid_variable_int).

### Return value

**-1** if the function is not found; otherwise - function ID in the queue.
## int run ( variable name , variable v0 )

Runs the given function with one argument or a member of a class in asynchronous way.
### Arguments

- *variable* **name** - Function to be run: *string* - function name, *int* - function ID, *object* - class name. > **Notice:** You can also pass an ID of the external class method that can be obtained via [*functionid()*](../../../api/library/common/class.system_usc.md#functionid_variable_int).
- *variable* **v0** - If **name** is an object: class member name or ID; otherwise - function argument.

### Return value

**-1** if the function is not found; otherwise - function ID in the queue.
## int run ( variable name , variable v0 , variable v1 )

Runs the given function with two arguments or a member of a class with one argument in asynchronous way.
### Arguments

- *variable* **name** - Function to be run: *string* - function name, *int* - function ID, *object* - class name. > **Notice:** You can also pass an ID of the external class method that can be obtained via [*functionid()*](../../../api/library/common/class.system_usc.md#functionid_variable_int).
- *variable* **v0** - If **name** is an object: class member name or ID; otherwise - function argument.
- *variable* **v1** - An argument of a function/class member.

### Return value

**-1** if the function is not found; otherwise - function ID in the queue.
## int run ( variable name , variable v0 , variable v1 , variable v2 )

Runs the given function with three arguments or a member of a class with two arguments in asynchronous way.
### Arguments

- *variable* **name** - Function to be run: *string* - function name, *int* - function ID, *object* - class name. > **Notice:** You can also pass an ID of the external class method that can be obtained via [*functionid()*](../../../api/library/common/class.system_usc.md#functionid_variable_int).
- *variable* **v0** - If **name** is an object: class member name or ID; otherwise - function argument.
- *variable* **v1** - An argument of a function/class member.
- *variable* **v2** - An argument of a function/class member.

### Return value

**-1** if the function is not found; otherwise - function ID in the queue.
## int run ( variable name , variable v0 , variable v1 , variable v2 , variable v3 )

Runs the given function with four arguments or a member of a class with three arguments in asynchronous way.
### Arguments

- *variable* **name** - Function to be run: *string* - function name, *int* - function ID, *object* - class name. > **Notice:** You can also pass an ID of the external class method that can be obtained via [*functionid()*](../../../api/library/common/class.system_usc.md#functionid_variable_int).
- *variable* **v0** - If **name** is an object: class member name or ID; otherwise - function argument.
- *variable* **v1** - An argument of a function/class member.
- *variable* **v2** - An argument of a function/class member.
- *variable* **v3** - An argument of a function/class member.

### Return value

**-1** if the function is not found; otherwise - function ID in the queue.
## int run ( variable name , variable v0 , variable v1 , variable v2 , variable v3 , variable v4 )

Runs the given function with four arguments or a member of a class with three arguments in asynchronous way.
### Arguments

- *variable* **name** - Function to be run: *string* - function name, *int* - function ID, *object* - class name. > **Notice:** You can also pass an ID of the external class method that can be obtained via [*functionid()*](../../../api/library/common/class.system_usc.md#functionid_variable_int).
- *variable* **v0** - If **name** is an object: class member name or ID; otherwise - function argument.
- *variable* **v1** - An argument of a function/class member.
- *variable* **v2** - An argument of a function/class member.
- *variable* **v3** - An argument of a function/class member.
- *variable* **v4** - An argument of a function/class member.

### Return value

**-1** if the function is not found; otherwise - function ID in the queue.
## int run ( variable name , variable v0 , variable v1 , variable v2 , variable v3 , variable v4 , variable v5 )

Runs the given function with five arguments or a member of a class with four arguments in asynchronous way.
### Arguments

- *variable* **name** - Function to be run: *string* - function name, *int* - function ID, *object* - class name. > **Notice:** You can also pass an ID of the external class method that can be obtained via [*functionid()*](../../../api/library/common/class.system_usc.md#functionid_variable_int).
- *variable* **v0** - If **name** is an object: class member name or ID; otherwise - function argument.
- *variable* **v1** - An argument of a function/class member.
- *variable* **v2** - An argument of a function/class member.
- *variable* **v3** - An argument of a function/class member.
- *variable* **v4** - An argument of a function/class member.
- *variable* **v5** - An argument of a function/class member.

### Return value

**-1** if the function is not found; otherwise - function ID in the queue.
## int run ( variable name , variable v0 , variable v1 , variable v2 , variable v3 , variable v4 , variable v5 , variable v6 )

Runs the given function with six arguments or a member of a class with five arguments in asynchronous way.
### Arguments

- *variable* **name** - Function to be run: *string* - function name, *int* - function ID, *object* - class name. > **Notice:** You can also pass an ID of the external class method that can be obtained via [*functionid()*](../../../api/library/common/class.system_usc.md#functionid_variable_int).
- *variable* **v0** - If **name** is an object: class member name or ID; otherwise - function argument.
- *variable* **v1** - An argument of a function/class member.
- *variable* **v2** - An argument of a function/class member.
- *variable* **v3** - An argument of a function/class member.
- *variable* **v4** - An argument of a function/class member.
- *variable* **v5** - An argument of a function/class member.
- *variable* **v6** - An argument of a function/class member.

### Return value

**-1** if the function is not found; otherwise - function ID in the queue.
## int runv ( variable name , int id = [] )

Runs the given function and a vector in asynchronous way.
### Arguments

- *variable* **name** - The argument.
- *int* **id** - Vector ID.

### Return value

**-1** if the function is not found; otherwise - function ID in the queue.
## void unlock ( )

Unlocks the previously [locked](#lock_void) resource.
## void wait ( int id )

Waits until the *[isRunning()](#isRunning_int_int)* function returns 0 (i.e. a thread with a specified ID is not active).
### Arguments

- *int* **id** - Thread ID.

## void wait ( )

Waits until the *[isRunning()](#isRunning_int)* function returns 0 (i.e. any thread is not active).
