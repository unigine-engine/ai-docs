# Unigine::Signal Class (CPP)

**Header:** #include <UnigineSignal.h>


This class implements the system of signals enabling synchronization of certain actions with certain events that occur asynchronously.


### Example


The following example illustrates how to make multiple subscriptions for a signal and cancel them if they are no longer needed, as well as how to invoke signals when necessary.


```cpp
#include <UnigineSignal.h>

class MyClass1
{
public:
	MyClass1() {}
	virtual ~MyClass1() {}

	// first callback function to be fired in case the signal is invoked
	int MySignalCallback1() {
		// do some actions
		Log::message("REPORT: MySignalCallback1() is called!");

		return 1;
	}
};

// second callback function to be fired in case the signal is invoked
int MySignalCallback2() {
	// do some actions (e.g. play a sound)
	Log::message("REPORT: MySignalCallback2() is called!");
	return 1;
}

// declaring an instance of the MyClass1
MyClass1 MyClass1Instance;

class MyClass2
{
public:
	Signal my_signal;	// Signal declaration

	int init()
	{
		// subscribing MyClass1Instance for the signal by adding a callback
		my_signal.add(MakeCallback(&MyClass1Instance, &MyClass1::MySignalCallback1));

		// subscribing for the signal by adding another callback and saving its ID to unsubscribe later
		void *cb2_id = my_signal.add(MakeCallback(MySignalCallback2));

		//...

		// whenever you want, execute the event (at this moment both callbacks will be fired)
		my_signal.invoke();

		// cancelling a subscription by removing a callback via ID
		my_signal.remove(cb2_id);

		return 0;

	}
	int shutdown(){
		// execute the event on shutdown (at this moment only the MyClass1::MySignalCallback1() callbacks will be fired, as the second one is no longer subscribed)
		my_signal.invoke();
	}
};


```


## Signal Class

### Members

---

## static SignalPtr create ( )

Default constructor that creates an empty signal.
## static SignalPtr create ( const Signal& )

Copy constructor that creates a signal using the specified one.
### Arguments

- *const Signal&*

## static SignalPtr create ( Signal&& )

Copy constructor that creates a signal using the specified one.
### Arguments

- *Signal&&*

## void * add ( CallbackBase* callback )

Adds a callback function to be fired when the signal is invoked (subscription for the signal). Callback functions can be used to determine specific actions to be performed when the signal is invoked.
### Arguments

- *CallbackBase** **callback**

### Return value

ID of the added callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#remove_void_ptr_bool) this callback when necessary.
## bool remove ( void* id )

Removes the specified callback from the list of callbacks associated with the signal. Callback functions can be used to determine specific actions to be performed when the signal is invoked.
### Arguments

- *void** **id** - Callback ID obtained when [adding](#add_CallbackBase_ptr_void_ptr) it.

### Return value

true if the callback with the given ID was removed successfully; otherwise false.
## void clear ( )

Clears the list of callbacks subscribed for the signal (all subscriptions are removed).
## bool empty ( ) const

Returns a value indicating if the list of subscriptions for the signal is empty.
### Return value

true if the list of subscriptions for the signal is empty otherwise false.
## int size ( ) const

Returns the total number of callback functions subscribed for the signal.
### Return value

Number of subscriptions for the signal.
## template<typename ... Ts> invoke ( Ts&& args )

Invokes the signal. Callback functions subscribed for this signal are executed according to their order in the list.
### Arguments

- *Ts&&* **args**

## void swap ( Signal& first , Signal& second )

Swaps the two specified signals.
### Arguments

- *Signal&* **first** - First signal.
- *Signal&* **second** - Second signal.
