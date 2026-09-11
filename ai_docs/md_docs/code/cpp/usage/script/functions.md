# Function Export

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Unigine API supports export of:


- Pure functions
- Methods of specific objects as pure functions


### See also


An example can be found in `<UnigineSDK>/source/samples/Api/Scripts/Functions/` directory.


## Function Export Example


Pure functions and object methods that are exported can take up to 9 arguments.


> **Notice:** The object whose methods are exported should not be destroyed while it is used by the engine in a script.


Below is an example of function and method export.


1. Create a pointer to an external function via *MakeExternFunction()*. For object methods, use *MakeExternObjectFunction()*.
2. Register the function or a method via *[Unigine::Interpreter::addExternFunction()](../../../../api/library/common/class.interpreter_cpp.md#addExternFunction_const_char_ptr_ExternFunctionBase_ptr_int_void)*.
3. All functions are exported into a global namespace. To limit the scope of the exported function or a method, use [library namespace](../../../../code/cpp/usage/script/namespace.md).


```cpp
#include <UnigineApp.h>
#include <UnigineConsole.h>
#include <UnigineEngine.h>
#include <UnigineInterface.h>
#include <UnigineLogic.h>
#include <UnigineString.h>
#include <UnigineWorld.h>

using namespace Unigine;
using namespace Unigine::Math;

//////////////////////////////////////////////////////////////////////////
// User defined functions
//////////////////////////////////////////////////////////////////////////

/*
 */
Variable my_sum(const Variable &v0, const Variable &v1)
{
	if (v0.getType() == Variable::INT && v1.getType() == Variable::INT)
	{
		Log::message("my_sum(%d,%d): called\n", v0.getInt(), v1.getInt());
		return Variable(v0.getInt() + v1.getInt());
	}

	if (v0.getType() == Variable::STRING && v1.getType() == Variable::STRING)
	{
		Log::message("my_sum(%s,%s): called\n", v0.getString(), v1.getString());
		return Variable((String(v0.getString()) + "+" + String(v1.getString())).get());
	}

	Log::message("my_sum(%s,%s): called\n", v0.getTypeName().get(), v1.getTypeName().get());

	return Variable("unknown");
}

/*
 */
float my_mul(float a, float b)
{
	Log::message("my_mul(%g,%g): called\n", a, b);

	return a * b;
}

/*
 */
float my_dot(const vec3 &v0, const vec3 &v1)
{
	Log::message("my_dot((%g,%g,%g),(%g,%g,%g)): called\n", v0.x, v0.y, v0.z, v1.x, v1.y, v1.z);

	return dot(v0, v1);
}

//////////////////////////////////////////////////////////////////////////
// User defined class member functions
//////////////////////////////////////////////////////////////////////////

/*
 */
class MyApplication
{
public:
	MyApplication()
		: seed(1)
	{
	}

	void init(int s = 1)
	{
		Log::message("MyApplication::init(%d) called\n", s);
		seed = s;
	}

	void shutdown()
	{
		Log::message("MyApplication::shutdown() called\n");
		seed = 1;
	}

	int update()
	{
		seed = (seed * 3877 + 29573) % 139968;
		return seed;
	}

	int get() const
	{
		return seed;
	}

private:
	int seed;
};

//////////////////////////////////////////////////////////////////////////
// System logic class
//////////////////////////////////////////////////////////////////////////

class AppSystemLogic : public SystemLogic
{
public:
	AppSystemLogic() {}
	virtual ~AppSystemLogic() {}

	int init() override
	{
		App::setUpdate(1);
		// load the world with a script file in UnigineScript using our functions
		World::loadWorld("functions");

		return 1;
	}
};
//////////////////////////////////////////////////////////////////////////
// Main
//////////////////////////////////////////////////////////////////////////
 int main(int argc, char **argv)
{
	// singleton
	MyApplication my_application;

	// export functions
	Interpreter::addExternFunction("my_sum", MakeExternFunction(&my_sum, ",1"));
	Interpreter::addExternFunction("my_mul", MakeExternFunction(&my_mul));
	Interpreter::addExternFunction("my_dot", MakeExternFunction(&my_dot));

	// export class member functions
	Interpreter::addExternLibrary("my_application");
	Interpreter::addExternFunction("my_application.init", MakeExternObjectFunction(&my_application, &MyApplication::init, "1"));
	Interpreter::addExternFunction("my_application.shutdown", MakeExternObjectFunction(&my_application, &MyApplication::shutdown));
	Interpreter::addExternFunction("my_application.update", MakeExternObjectFunction(&my_application, &MyApplication::update));
	Interpreter::addExternFunction("my_application.get", MakeExternObjectFunction(&my_application, &MyApplication::get));

	// init engine
	EnginePtr engine(argc, argv);

	// enter main loop
	AppSystemLogic system_logic;
	engine->main(&system_logic, NULL, NULL);

	return 0;
}

```


### Access from Scripts


After the registration, the exported functions and methods can be used in a script written in UnigineScript (loaded in *AppSystemLogic::init()* above):


```cpp
/*
 */
int init()
{
	/////////////////////////////////

	log.message("\nFunctions:\n\n");

	// my_sum(1) with default second argument
	log.message("result is: %s\n\n", typeinfo(my_sum(1)));

	// my_sum(1,2)
	log.message("result is: %s\n\n", typeinfo(my_sum(1, 2)));

	// my_sum("begin","end")
	log.message("result is: %s\n\n", typeinfo(my_sum("begin", "end")));

	// my_sum(1,"end")
	log.message("result is: %s\n\n", typeinfo(my_sum(1, "end")));

	// my_mul(16,64)
	log.message("result is: %s\n\n", typeinfo(my_mul(16, 64)));

	// my_dot(vec3(1.0f,2.0f,3.0f),vec3(4.0f,5.0f,6.0f))
	log.message("result is: %s\n\n", typeinfo(my_dot(vec3(1.0f, 2.0f, 3.0f), vec3(4.0f, 5.0f, 6.0f))));

	/////////////////////////////////

	log.message("Member functions:\n\n");

	// default argument
	my_application.init();

	// manual argument
	my_application.init(100);

	// update application
	for (int i = 0; i < 4; i++)
		log.message("%d: %d\n", i, my_application.update());

	// shutdown
	my_application.shutdown();

	/////////////////////////////////

	// show console
	engine.console.setActivity(1);

	return 1;
}

```


### Output


The following result will be printed into the console:


```text
Functions:

my_sum(1,1): called
result is: int: 2

my_sum(1,2): called
result is: int: 3

my_sum(begin,end): called
result is: string: "begin+end"

my_sum(int,string): called
result is: string: "unknown"

my_mul(16,64): called
result is: float: 1024

my_dot((1,2,3),(4,5,6)): called
result is: float: 32

Member functions:

MyApplication::init(1) called
MyApplication::init(100) called
0: 137337
1: 46850
2: 128527
3: 42672
MyApplication::shutdown() called

```


## Default Argument Values


If you want to export functions with default values for their arguments, you can specify them as the last argument of *MakeExternFunction()*. The order of values should be the same as the order of arguments in the function declaration, and the values should be comma-separated. For example:


```cpp
void foo(const char *a,float b) { }

// To specify default values:
Interpreter::addExternFunction("foo",MakeExternFunction(&foo,"\"Unigine\",0.4"));

```


If you want to specify default values not for all arguments, simply omit those that do not have defaults, but don't forget commas:


```cpp
// To specify only required default value:
Interpreter::addExternFunction("foo",MakeExternFunction(&foo,",0.4"));

```


### Expression as a Default Argument


Besides constants, you can also specify expressions as default values.


- Expressions are evaluated before the function is registered.
- An expression provided as a default argument should return a value of the same type as the corresponding argument. Type conversions are not supported, the only exception being a two-way conversion between *float* and *int*.


## Overloading Caveats


Unlike C++, UnigineScript is not a strongly typed language. In C++ code you can have two or more functions with the same name that return a value of the same type, but accept different types of arguments (or the number of arguments differs). If you attempt to export them into scripts simply by registering function names, *MakeExternFunction()* will fail.


To make registration work, you need to explicitly specify:


1. Return value type
2. Arguments types


```cpp
void foo(int a) { }
void foo(float a) { }

/* Interpreter::addExternFunction("foo",MakeExternFunction(&foo));
 * This expression will not work since Interpreter cannot choose between functions.
 */

// To register void foo(int a), use:
Interpreter::addExternFunction("foo",MakeExternFunction<void,int>(&foo));

// To register void foo(float a), use:
Interpreter::addExternFunction("foo",MakeExternFunction<void,float>(&foo));

```


Let's say we have got a more difficult situation: the first arguments of functions are of the same type. In such case, following syntax is used for registration:


```cpp
void foo(int a) { }
void foo(int a,int b) { }

/* Interpreter::addExternFunction("foo",MakeExternFunction<void,int>(&foo));
 * This expression will not work since both functions take an integer as a first argument.
 */

// To register void foo(int a), use:
Interpreter::addExternFunction("foo",MakeExternFunction((void (*)(int))&foo));

// To register void foo(int a,int b), use:
Interpreter::addExternFunction("foo",MakeExternFunction((void (*)(int,int))&foo));

/* Interpreter::addExternFunction("foo",MakeExternFunction<void,int,int>(&foo));
 * This expression will also allow to register void foo(int a,int b).
 */

```


### Overloading Exported Methods


If ambiguity exists for class static methods names, it is resolved in a similar way as for functions.


```cpp
class Class {

	public:

		static int foo(float a) { return 1; }
        static int foo(int a) { return 1; }
		static void foo(int a,int b) { return 1; }
};

/*
*/

// To register foo(float a):
Interpreter::addExternFunction("foo",MakeExternFunction((int (*)(float))&Class::foo));
// To register foo(int a):
Interpreter::addExternFunction("foo",MakeExternFunction((int (*)(int))&Class::foo));
// To register foo(int a,int b):
Interpreter::addExternFunction("foo",MakeExternFunction((void (*)(int,int))&Class::foo));

```
