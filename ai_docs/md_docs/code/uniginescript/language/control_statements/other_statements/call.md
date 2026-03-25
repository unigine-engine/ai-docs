# Call()

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## variable call ( string function_name , variable arguments )

Calls a function, which name is provided as an argument.
> **Notice:** The above expression is equivalent to this one: *function_name(arguments)*.


### Arguments

- *string* **function_name** - Name of the function to call.
- *variable* **arguments** - Function arguments.

### Return value

Function execution result.
### Examples


```cpp
call("log.message","%d %s\n",13,"some text");

// the result is: 13 some text

```


## variable call ( int function_id , variable arguments )

Calls a function by its ID, which is almost as fast as the direct function call. In order to get this ID, use *get_function()*.
### Arguments

- *int* **function_id** - ID of the function to call.
- *variable* **arguments** - Function arguments.

### Return value

Function execution result.
### Examples


```cpp
void foo(int a) {
	log.message("%d\n",a);
}

int id = get_function("foo",1);
call(id,3);

// the result is: 3

```

 If you need to call a user class method by its ID rather then as a static method, you can use the following:
```cpp
class MyClass {

    void print_me() {
        log.message("MyClass::print_me() called\n");
    }

    void id_func(MyClass obj) {
        obj.print_me();
    }
};

MyClass m = new MyClass();
call(get_function("MyClass::id_func",1),m);

// the result is: MyClass::print_me() called

```

 Also you can call the *id_func()* function as follows:
```cpp
int id = get_function("MyClass::id_func",1);
m.call(id,m);

```


## variable call ( string function_name , variable array )

Calls a function, whose name is provided as an argument. The number of function arguments can vary.
### Arguments

- *string* **function_name** - Name of the function to call.
- *variable* **array** - Function arguments. The number of function arguments can vary.

### Return value

Function execution result.
### Examples


```cpp
int args[] = ("%s\n","hello world");
call("log.message",args);

// ouput: hello world

```


## variable call ( string method_name , variable arguments )

Calls methods of external or user-defined classes.
### Arguments

- *string* **method_name** - Name of the method to call.
- *variable* **arguments** - Function arguments.

### Return value

Function execution result.
### Examples


Call methods of an external class:

```cpp
File file = new File("test.cpp","rb");
log.message("%d %s\n",file.call("isOpened"),file.call("getName"));
file.call("close");	// same as file.close();
delete file;

// the output is: 1 test.cpp

```

 Call a method of a user-defined class:
```cpp
class Foo {
	void print(int a) {
		log.message("Foo::print(): %d\n",a);
	}
};
Foo foo = new Foo();
foo.print(1);
foo.call("print",2);

// Foo::print(): 1
// Foo::print(): 2

```
