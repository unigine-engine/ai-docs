# CallbackBase Class (CPP)

**Header:** #include <UnigineCallback.h>


A base class for engine callbacks.


This class allows you to create your own callbacks with up to 5 arguments.


### Usage Example


This section contains the simple CallbackBase usage example.


In the header file:


```cpp
#include <UnigineLogic.h>
#include <UnigineStreams.h>
#include <UnigineCallback.h>

class AppWorldLogic : public Unigine::WorldLogic {

public:
	/* other methods */

	// function
	void setNewCallback(Unigine::CallbackBase *cb);

private:
	// Callback function
	Unigine::CallbackBase *callback_func;
};

```


The implementation file looks like:


```cpp
#include "AppWorldLogic.h"
#include "UnigineCallback.h"

using namespace Unigine;
CallbackBase *func;

/* other methods */

void AppWorldLogic::setNewCallback(CallbackBase *func) {
	callback_func = func;
}

```


## CallbackBase Class

### Members

---

## void run ( A0 a0 , A1 a1 )

Executes the callback function with two arguments.
### Arguments

- *A0* **a0** - The first argument of the callback function.
- *A1* **a1** - The second argument of the callback function.

## void run ( A0 a0 , A1 a1 , A2 a2 , A3 a3 )

Executes the callback function with four arguments.
### Arguments

- *A0* **a0** - The first argument of the callback function.
- *A1* **a1** - The second argument of the callback function.
- *A2* **a2** - The third argument of the callback function.
- *A3* **a3** - The fourth argument of the callback function.

## void run ( A0 a0 , A1 a1 , A2 a2 , A3 a3 , A4 a4 )

Executes the callback function with five arguments.
### Arguments

- *A0* **a0** - The first argument of the callback function.
- *A1* **a1** - The second argument of the callback function.
- *A2* **a2** - The third argument of the callback function.
- *A3* **a3** - The fourth argument of the callback function.
- *A4* **a4** - The fifth argument of the callback function.

## void run ( A0 a0 , A1 a1 , A2 a2 )

Executes the callback function with three arguments.
### Arguments

- *A0* **a0** - The first argument of the callback function.
- *A1* **a1** - The second argument of the callback function.
- *A2* **a2** - The third argument of the callback function.

## void run ( A0 a0 )

Executes the callback function with one argument.
### Arguments

- *A0* **a0** - The first argument of the callback function.

## void run ( )

Executes the callback function without arguments.
