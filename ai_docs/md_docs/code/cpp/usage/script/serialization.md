# Serialization

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Unigine API allows creating of objects whose states can be saved into a binary file and later restored from it.


### See also


An example can be found in `<UnigineSDK>/source/samples/Api/Scripts/Serialization/` directory.


## Serialization Guidelines


Saving and restoring of the object state is done by using a binary serialization mechanism of Unigine.  In order to be compatible with this mechanism,a class must implement methods that allow you to store states of the class objects into the *[Unigine::Stream](../../../../api/library/common/class.stream_cpp.md)* and restore them from it.


These methods can be grouped as follows:


- Methods for saving/restoring of **states**. The states are used for objects created and handled purely in UnigineScript.  It means, such object implemented on the C++ side is created in script via *new* operator and deleted via *delete*.  It is not passed between UnigineScript and any other system.

  - *saveState()* - saves a state of an object created on the UnigineScript side.
  - *restoreState()* � restores a state of an object created on the UnigineScript side. This function implies that a class has a default constructor that creates an empty object.
- Methods for saving/restoring of **pointers**. The pointers are used for objects that are created in a C++ part of the application and will be deleted there as well.  The script receives it, but is not responsible for managing them. For example, this is the case when a C++ function that creates an object is called from the script.

  - *savePointer()* � a static method which is used to save a state of an object created on C++ side and handled by a script.
  - *restorePointer()* � a static method which is used to restore a state of an object created on C++ side and handled by a script.


If an object is going to be created in script, as well as created on C++ side, all four functions should be implemented.


> **Notice:** If the above methods are implemented incorrectly, the objects will not be saved, and memory-related errors will appear.


### Step 1. Implement Object Saving and Restoring


By default, the following implementation is used (see the `include/UnigineInterpreter.h` header file):


```cpp
// functor to save a state of an object constructed in scripts
template <class Class>
void ExternClassSaveState(const StreamPtr &stream,Class *object) {
	object->saveState(stream);
}

// functor to restore a state of an object constructed in scripts
template <class Class>
Class *ExternClassRestoreState(const StreamPtr &stream) {
	Class *object = new Class();
	object->restoreState(stream);
	return object;
}

// functor to save a state of an object created on C++ side and handled by a script
template <class Class>
	void ExternClassSavePointer(const StreamPtr &stream,Class *object) {
	Class::savePointer(stream,object);
}

// functor to restore a state of an object created on C++ side and handled by a script
template <class Class>
Class *ExternClassRestorePointer(const StreamPtr &stream) {
	return Class::restorePointer(stream);
}

```


### Step 2. Export Class


You need to export classes whose instances are going to be serialized. One of the following functions can be used for that:


- *MakeExternClass()* function. Instances of classes [exported](../../../../code/cpp/usage/script/classes.md) by using this function are non-restorable, that is, they should be manually re-created. If you try to restore an instance of such the class, this instance will be restored to **null**.
- *MakeExternClassSaveRestoreState()* function, which allows you to save and restore instances created within UnigineScript.
- *MakeExternClassSaveRestorePointer()* function, which allows you to save and restore objects that were created in C++ code and exported into UnigineScript.
- *MakeExternClassSaveRestoreStatePointer()* function, which combines two previous possibilities, that is, objects created on both the UnigineScript and C++ sides can be saved and restored.


#### Changing Serialization Behaviour


After exporting, it is still possible to change serialization behavior in run-time. For that you can use two UnigineScript functions.


> **Notice:** It is completely safe only if both state and pointer saving/restoring is implemented.


- [*class_append()*](../../../../api/library/common/class.system_cpp.md#class_append_Variable) attaches the object to the script that will handle it (save, restore and delete it).
- [*class_remove()*](../../../../api/library/common/class.system_cpp.md#class_remove_Variable) removes the object from the script.


> **Notice:** UnigineScript does not destroy objects that were created on C++ side and were not appended to the script.


## Serialization Example


Here is an example of exporting a C++ class that fully supports serialization into UnigineScript.


### C++ Side


```cpp
#include <UnigineEngine.h>
#include <UnigineInterpreter.h>
#include <UnigineInterface.h>

#include "AppSystemLogic.h"
#include "AppWorldLogic.h"

using namespace Unigine;
using namespace Math;

/******************************************************************************\
*
* User defined class
*
\******************************************************************************/

class MyObject : public Base {

	public:

		MyObject() : mass(0.0f) {
			Log::warning("MyObject::MyObject(): called\n");
		}
		MyObject(const vec3 &size,float mass) : size(size), mass(mass) {
			Log::warning("MyObject::MyObject((%g,%g,%g),%g): called\n",size.x,size.y,size.z,mass);
		}
		~MyObject() {
			Log::warning("MyObject::~MyObject(): called\n");
		}

		// size
		void setSize(const vec3 &s) {
			Log::warning("MyObject::setSize((%g,%g,%g)): called\n",s.x,s.y,s.z);
			size = s;
		}
		const vec3 &getSize() const {
			return size;
		}

		// mass
		void setMass(float m) {
			Log::warning("MyObject::setMass(%g): called\n",m);
			mass = m;
		}
		float getMass() const {
			return mass;
		}

		// save state
		void saveState(StreamPtr &stream) const {
			Log::warning("MyObject::saveState(): called\n");
			stream->writeVec3(size);
			stream->writeFloat(mass);
		}

		// restore state
		void restoreState(StreamPtr &stream) {
			Log::warning("MyObject::restoreState(): called\n");
			size = stream->readVec3();
			mass = stream->readFloat();
		}

		// save pointer
		static void savePointer(StreamPtr &stream,MyObject *object) {
			Log::warning("MyObject::savePointer(): called\n");
			stream->writeVec3(object->size);
			stream->writeFloat(object->mass);
		}

		// restore pointer
		static MyObject *restorePointer(StreamPtr &stream) {
			MyObject *object = new MyObject();
			Log::warning("MyObject::restorePointer(): called\n");
			object->size = stream->readVec3();
			object->mass = stream->readFloat();
			return object;
		}

	private:

		vec3 size;
		float mass;
};

MyObject *MakeMyObject(const vec3 &size,float mass) {
	return new MyObject(size,mass);
}

void DeleteMyObject(MyObject *object) {
	delete object;
}

/******************************************************************************\
*
* Main
*
\******************************************************************************/

#ifdef _WIN32
	int wmain(int argc,wchar_t *argv[]) {
#else
	int main(int argc,char *argv[]) {
#endif

	// export class with serialization
	ExternClass<MyObject> *my_object = MakeExternClassSaveRestoreStatePointer<MyObject>();
	my_object->addConstructor<const vec3&,float>();
	my_object->addFunction("setSize",&MyObject::setSize);
	my_object->addFunction("getSize",&MyObject::getSize);
	my_object->addFunction("setMass",&MyObject::setMass);
	my_object->addFunction("getMass",&MyObject::getMass);
	Interpreter::addExternClass("MyObject",my_object);

	// export functions
	Interpreter::addExternFunction("MakeMyObject",MakeExternFunction(&MakeMyObject));
	Interpreter::addExternFunction("DeleteMyObject",MakeExternFunction(&DeleteMyObject));

	AppSystemLogic system_logic;
	AppWorldLogic world_logic;

	Unigine::EnginePtr engine(argc,argv);

	engine->main(&system_logic,&world_logic);

	return 0;
}

```


### Unigine Script Side


And here is how the exported class can be used in UnigineScript (see the description of the [*yield*](../../../../code/uniginescript/language/control_statements/other_statements/yield.md) control statement for better understanding of the example):


```cpp
/*
 */
MyObject object_0;
MyObject object_1;

/*
 */
void object_info(MyObject object) {

	// object parameters
	vec3 size = object.getSize();
	float mass = object.getMass();

	log.message("size is: (%g,%g,%g), mass is: %g\n",size.x,size.y,size.z,mass);
}

/*
 */
int init() {

	/////////////////////////////////

	log.message("\n");

	// make script constructed object
	object_0 = new MyObject(vec3(1.0f,2.0f,3.0f),10.0f);

	// make extern constructed object
	object_1 = MakeMyObject(vec3(4.0f,5.0f,6.0f),100.0f);

	/////////////////////////////////

	// show console
	engine.console.setActivity(1);

	return 1;
}

/*
 */
int shutdown() {

	// delete external constructed object
	DeleteMyObject(object_1);

	return 1;
}

/*
 */
int update() {

	/////////////////////////////////
	// first update
	/////////////////////////////////

	log.message("\n");

	// parameters
	object_info(object_0);
	object_info(object_1);

	yield 1;

	/////////////////////////////////
	// second update
	/////////////////////////////////

	log.message("\n");



	yield 1;

	/////////////////////////////////
	// third update
	/////////////////////////////////

	log.message("\n");

	// parameters
	object_info(object_0);
	object_info(object_1);

	yield 1;

	/////////////////////////////////

	return 1;
}

```


### Output


The following result will be printed into the console:


```text
MyObject::MyObject((1,2,3),10): called
MyObject::MyObject((4,5,6),100): called

size is: (1,2,3), mass is: 10
size is: (4,5,6), mass is: 100

Saving "data/serialization" world state to "save/quicksave.save" file

MyObject::saveState(): called
MyObject::savePointer(): called
MyObject::~MyObject(): called
MyObject::~MyObject(): called

Restoring "data/serialization" world state from "save/quicksave.save" file

MyObject::MyObject(): called
MyObject::restoreState(): called
MyObject::MyObject(): called
MyObject::restorePointer(): called

size is: (1,2,3), mass is: 10
size is: (4,5,6), mass is: 100

Unigine~# quit

MyObject::~MyObject(): called
MyObject::~MyObject(): called

```
