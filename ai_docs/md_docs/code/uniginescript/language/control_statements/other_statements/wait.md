# Wait

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This construct suspends execution of the current function. The address of the function is placed into a list of waiting functions. Waiting functions are "unfrozen" after the *runWaits* call, which can be performed only in the C++ part of the application. Unigine runs functions from the waiting list each frame automatically. Therefore, you can create threads that act once per frame and use *wait* for synchronization.

> **Notice:** *wait* construst can only be used in a thread.


### Syntax


```cpp
wait value;
```


### Parts


- *value* is an optional return value (0 by default).


### Example


```cpp
void thread_func() {
	for(int i = 0; i < 4; i++) {
		log.message("%d\n",i);
		wait;
	}
}

thread("thread_func");

/* Output:
 * "0" // first frame
 * "1" // second frame
 * "2" // third frame
 * "3" // fourth frame
 */

```


> **Notice:** *wait* construct is valid when called from a simple function (rather then the member function of the class):


```cpp
void update_redirector(Sprite sprite) {
	while(1) {
		sprite.update();
		wait;
	}
}

```


If the class instance is set, an error will be generated, because a class instance is not stored when saving the function to be handled by *runWaits* in the next frame. However, *wait* is possible if the class function is called as a static function (without passing a class instance to it):

```cpp
class Foo {

	void update() {
		while(true) wait 1;
	}
};

Foo f = new Foo();
Foo::update();		// this is valid, because the method is called as a static function

// f.update();		// this would cause a crash, because a class instance is passed

```


See also: [*thread()*](../../../../../code/uniginescript/language/control_statements/other_statements/thread.md).
