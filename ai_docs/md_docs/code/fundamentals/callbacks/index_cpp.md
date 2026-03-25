# Event Handling Callbacks (CPP)


Callback is a function wrapper representing a pointer to static and member functions which are expected to be executed with specified parameters at a certain moment. A callback can be passed as an argument to a function.


> **Notice:** Callbacks are guaranteed to be reentrant and provide safe multi-threaded execution.


In Unigine C++ API, the *[**CallbackBase**](../../../api/library/common/callbacks/class.callbackbase_cpp.md)* is the base class to represent callbacks with variable number of arguments from **0** to **5**. To create a callback, the *[*MakeCallback()*](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Retm)* function is used:


```cpp
void callback_function() {
	/* .. */
}
CallbackBase *callback = MakeCallback(callback_function);

```


A callback to a member function of either the current class or another is created as follows:


```cpp
void ThisClass::callback_function() {
	/* .. */
}
/* .. */
// the first argument is an instance of a class, the second one is the pointer to a member function
CallbackBase *callback = MakeCallback(this, &ThisClass::callback_function);

```


The *[**CallbackBase**](../../../api/library/common/callbacks/index.md)* classes are used to create a callback with fixed number of arguments. Depending on the number of arguments the corresponding class should be used. In this case you should provide template arguments:


```cpp
void ThisClass::callback_function(NodePtr, int) {
	/* .. */
}
// create a callback with no predefined parameters
CallbackBase2<NodePtr, int> *callback = MakeCallback(this, &ThisClass::callback_function);

// create a callback with predefined parameters
CallbackBase2<NodePtr, int> *callback2 = MakeCallback(this, &ThisClass::callback_function, NodeDummy::create()->getNode(), 1);

// create a callback with parameters from lambda
CallbackBase2<NodePtr, int> *callback = MakeCallback([](NodePtr node, int value) { /* .. */ });

// create a callback with parameters from generic lambda
CallbackBase2<NodePtr, int> *callback = MakeCallback([](auto node, auto value) { /* .. */ });

```


To use overloaded functions and methods as callbacks, provide the template parameters:
*MakeCallback< Class, ReturnType, Callback Parameters Types >*


```cpp
void ThisClass::callback_method()
{
	/* .. */
}

void ThisClass::callback_method(WidgetPtr w, WidgetPtr w2, int i)
{
	/* .. */
}

CallbackBase *callback = MakeCallback<ThisClass, void, WidgetPtr, WidgetPtr, int>(this, &ThisClass::callback_method);

```


To raise a custom callback, the *[*run()*](../../../api/library/common/callbacks/class.callbackbase_cpp.md#run_void)* function of one of the *CallbackBase* classes is used.


```cpp
// run the callback with no parameters or with default predefined parameters
callback->run();

// run the callback with the specified parameters
callback->run(node, 2);

```


You can also use lambda expressions for callbacks:


```cpp
// create a callback from lambda
int value = 5;
CallbackBase* callback = MakeCallback([value](){ /* .. */ });

// or std function
std::function<void()> callable_obj = [value]() { /* .. */ };
CallbackBase* callback = MakeCallback(callable_obj);

// or any other type of callable
struct Callable
{
void operator()() const { /* .. */ }
int value;
} callable_obj = { /* .. */ };

CallbackBase* callback = MakeCallback(callable_obj);

```


### Usage Example


The following section contains the complete source code of a simple callback usage example.


<details>
<summary>AppWorldLogic.h | Close</summary>

```cpp
#ifndef __APP_WORLD_LOGIC_H__
#define __APP_WORLD_LOGIC_H__

#include <UnigineLogic.h>
#include <UnigineStreams.h>
#include <UnigineCallback.h>

using namespace Unigine;
using namespace Math;

class AppWorldLogic: public Unigine::WorldLogic
{

public:

	int init() override;

	int update() override;
	int postUpdate() override;
	int updatePhysics() override;

	int shutdown() override;
};

#endif // __APP_WORLD_LOGIC_H__

```

</details>


<details>
<summary>AppWorldLogic.cpp | Close</summary>

```cpp
#include "AppWorldLogic.h"

class SomeClass
{
public:
	// a member function to be called on the action
	void callback_method(int a, int b)
	{
		Log::message("\tcallback_method has been called %d %d\n", a, b);
	}

	void create_callbacks()
	{
		Log::message("Create a callback with no predefined parameters\n");
		CallbackBase * callback = MakeCallback(this, &SomeClass::callback_method);

		// run the callback with two parameters
		callback->run(73, 37);
		// run the callback with no parameters.
		// if the callback function has arguments, this will lead to unsafe behaviour
		callback->run();

		Log::message("Create a callback with predefined parameters\n");
		CallbackBase * callback2 = MakeCallback(this, &SomeClass::callback_method, 1, 2);

		// run the callback with no parameters. In this case, the predefined parameters will be used
		callback2->run();
		// run the callback with parameters. The predefined ones will be ignored
		callback2->run(351, 153);
		// run the callback with only 1 parameter.
		// the second predefined parameter will be used as the second argument
		callback2->run(118);
	}
};

// a callback function to be called on the action
void callback_function(int a, int b)
{
	Log::message("\tcallback_function has been called %d %d\n", a, b);
}

int AppWorldLogic::init()
{
	SomeClass *some = new SomeClass();
	// call the SomeClass member function
	some->create_callbacks();

	Log::message("Create a callback in the other instance\n");
	// use the callback function of the SomeClass to create a callback
	CallbackBase * callback3 = MakeCallback(some, &SomeClass::callback_method, 5, 25);
	callback3->run();

	Log::message("Create callback functions\n");
	CallbackBase * callback4 = MakeCallback(&callback_function);
	callback4->run(20, 70);
	CallbackBase * callback5 = MakeCallback(&callback_function, 50, 25);
	callback5->run();

	return 1;
}

int AppWorldLogic::update()
{

	return 1;
}

int AppWorldLogic::postUpdate()
{
	return 1;
}

int AppWorldLogic::updatePhysics()
{
	return 1;
}

int AppWorldLogic::shutdown()
{
	return 1;
}

```

</details>
