# Class Export

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Unigine API supports class export from C++ into UnigineScript along with their:


- Constructors
- Member functions (up to eight arguments are supported)


> **Notice:** Member variables cannot be exported. Since it is not possible to access them directly, you need to create accessor methods for them.


### See also


A simple application with C++ class implementation and export can be found in the `<UnigineSDK>/source/samples/Api/Scripts/Classes/` directory.


## Exporting a Class


In order to export a C++ class into UnigineScript you need to implement a *static* method that:


1. Creates an external C++ class via the *MakeExternClass()* function.
2. Adds constructors to the external class via the [*Unigine::ExternClass<Class>::addConstructor()*](../../../../api/library/common/class.externclass_cpp.md#addConstructor_const_char_ptr_void) function.
3. Adds methods to the external class via the [*Unigine::ExternClass<Class>::addFunction()*](../../../../api/library/common/class.externclass_cpp.md#addFunction_const_char_ptr_methodptr_const_char_ptr_void) function. If the method receives an array as an argument, you should specify the array declaration as the last argument of the *addFunction()* as follows: ```cpp my_object->addFunction("my_array",&MyExternObject::my_array,"[]"); ``` If the target method has more than one argument, specify the array declaration on the corresponding position: ```cpp // the my_array() method receives an array as the second argument my_object->addFunction("my_array",&MyExternObject::my_array,",[],"); ``` See also the [Default Argument Values](../../../../code/cpp/usage/script/functions.md#args) chapter of the Function Export article and the article on [UnigineScript Containers](../../../../code/cpp/usage/script/arrays.md) for more details.
4. Registers the external class via *[Unigine::Interpreter::addExternClass()](../../../../api/library/common/class.interpreter_cpp.md#addExternClass_const_char_ptr_ExternClassBase_ptr_int_void)*.
5. Exports functions of the external class via the [*Interpreter::addExternFunction()*](../../../../api/library/common/class.interpreter_cpp.md#addExternFunction_const_char_ptr_ExternFunctionBase_ptr_int_void) function.


> **Notice:** Note that static methods of classes are exported as [pure functions](../../../../code/cpp/usage/script/functions.md).


For example:


```cpp
class MyExternObject {

	public:

		// constructors
		MyExternObject() : mass(0.0f) {
		Log::warning("MyExternObject::MyExternObject(): called\n");
		}

		MyExternObject(const vec3 &size, float mass) : size(size), mass(mass) {
			Log::warning("MyExternObject::MyExternObject((%g,%g,%g),%g): called\n", size.x, size.y, size.z, mass);
		}

		// destructor
		~MyExternObject() {
			Log::warning("MyExternObject::~MyExternObject(): called\n");
		}

		// export class to script
		static void registerClass();

		// size
		void setSize(const vec3 &s) {
			Log::warning("MyExternObject::setSize((%g,%g,%g)): called\n",s.x,s.y,s.z);
			size = s;
		}
		const vec3 &getSize() const {
			return size;
		}

		// mass
		void setMass(float m) {
			Log::warning("MyExternObject::setMass(%g): called\n",m);
			mass = m;
		}
		float getMass() const {
			return mass;
		}

	private:

		vec3 size;
		float mass;
};

/*
*/
MyExternObject *MakeMyExternObject(const vec3 &size,float mass) {
	return new MyExternObject(size,mass);
}

void DeleteMyExternObject(MyExternObject *object) {
	delete object;
}

/*
 */
void MyExternObjectSetSize(MyExternObject *object,const vec3 &size) {
	object->setSize(size);
}

const vec3 &MyExternObjectGetSize(MyExternObject *object) {
	return object->getSize();
}

// export the external class
void registerClass() {

	ExternClass<MyExternObject> *my_object = MakeExternClass<MyExternObject>();
	my_object->addConstructor();
	my_object->addConstructor<const vec3&, float>();
	my_object->addFunction("setSize",&MyExternObject::setSize);
	my_object->addFunction("getSize",&MyExternObject::getSize);
	my_object->addFunction("setMass",&MyExternObject::setMass);
	my_object->addFunction("getMass",&MyExternObject::getMass);
	Interpreter::addExternClass("MyExternObject",my_object);

	// export external class functions
	Interpreter::addExternFunction("DeleteMyExternObject",MakeExternFunction(&DeleteMyExternObject));
	Interpreter::addExternFunction("MakeMyExternObject",MakeExternFunction(&MakeMyExternObject));
	Interpreter::addExternFunction("MyExternObjectSetSize",MakeExternFunction(&MyExternObjectSetSize));
	Interpreter::addExternFunction("MyExternObjectGetSize",MakeExternFunction(&MyExternObjectGetSize));

}

```


Then the implemented method *registerClass()* can be called as follows:


- In the *main()* function before Engine initialization: ```cpp #ifdef _WIN32 int wmain(int argc,wchar_t *argv[]) { #else int main(int argc,char *argv[]) { #endif // export the class MyExternObject::registerClass(); AppSystemLogic system_logic; AppWorldLogic world_logic; AppEditorLogic editor_logic; Unigine::EnginePtr engine(argc,argv); // Enter main loop. engine->main(&system_logic,&world_logic,&editor_logic); return 0; } ``` If the class uses the Engine and/or graphics resources, they should be processed properly in the main loop: If, for example, the class creates the Engine resource in the constructor, and you export this class in the *main()* function, the Engine resource may be created before Engine initialization, resulting in Engine crash.

  - If the Engine resources are used (e.g. *Texture, Image, Mesh, Node*, etc.), the class should implement the *init()* and *shutdown()* methods, at least. Here creating and deleting of the resources should be done.
- In the constructor of the *[WorldLogic](../../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic)/[SystemLogic](../../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic)*. For example: ```cpp class MyWorldLogic : public WorldLogic { // export the class MyExternObject::registerClass(); public: virtual int init(); virtual int shutdown(); }; int MyWorldLogic::init() { Log::message("MyWorldLogic::init(): called\n"); return 1; } int MyWorldLogic::shutdown() { Log::message("MyWorldLogic::shutdown(): called\n"); return 1; } ``` > **Notice:** If you call the *registerClass()* method in the *init()* function of the WorldLogic, the class won't be available in the world script *init()* function, as it is called before the WorldLogic initialization according to the execution sequence. The same is true for the SystemLogic.


### Access from Scripts


After the registration, the exported class can be used in UnigineScript just like any other classes.


```cpp
// my_world.usc

/*
*/
void extern_object_info(MyExternObject object) {

	// call object methods to get its parameters
	vec3 size = object.getSize();
	float mass = object.getMass();

	log.message("size is: (%g,%g,%g), mass is: %g\n",size.x,size.y,size.z,mass);
}

/*
*/
int init() {

	/* ... code ... */
	/////////////////////////////////

	log.message("\n");

	// create an external object using a default constructor
	MyExternObject extern_object = new MyExternObject();
	extern_object_info(extern_object);

	// set parameters of the external object
	extern_object.setSize(vec3(10.0f,20.0f,30.0f));
	extern_object_info(extern_object);

	// delete the object
	delete extern_object;

	/////////////////////////////////

	log.message("\n");

	// create an object using another constructor
	extern_object = new MyExternObject(vec3(1.0f,2.0f,3.0f),10.0f);
	extern_object_info(extern_object);

	// set object parameters
	MyExternObjectSetSize(extern_object,vec3(10.0f,20.0f,30.0f));
	vec3 size = MyExternObjectGetSize(extern_object);
	log.message("size is: (%g,%g,%g)\n",size.x,size.y,size.z);

	// delete the object
	delete extern_object;

	/////////////////////////////////

	log.message("\n");

	// create an object using the external class function
	extern_object = MakeMyExternObject(vec3(4.0f,5.0f,6.0f),10.0f);
	extern_object_info(extern_object);

	// set object parameters.
	extern_object.setMass(100.0f);
	extern_object_info(extern_object);

	// delete the object using the external class function
	DeleteMyExternObject(extern_object);

	/////////////////////////////////

	return 1;
}

```


### Output


The following results will be printed to the console:


```text
MyExternObject::MyExternObject(): called
size is: (0,0,0), mass is: 0
MyExternObject::setSize((10,20,30)): called
size is: (10,20,30), mass is: 0
MyExternObject::~MyExternObject(): called

MyExternObject::MyExternObject((1,2,3),10): called
size is: (1,2,3), mass is: 10
MyExternObject::setSize((10,20,30)): called
size is: (10,20,30)
MyExternObject::~MyExternObject(): called

MyExternObject::MyExternObject((4,5,6),10): called
size is: (4,5,6), mass is: 10
MyExternObject::setMass(100): called
size is: (4,5,6), mass is: 100
MyExternObject::~MyExternObject(): called

```


## Exporting a Singleton Class


The general approach to C++ class exporting described above is common for all types of classes. However, exporting of *singleton classes* has several peculiarities.


A singleton class can be exported to the script:


- As a *library*. ```cpp class Singleton { public: // get a singleton instance static Singleton *get(); // export the class static void registerClass(); // create and delete engine and GPU resources (if any) int init(); int shutdown(); // class methods void setData(float data) { Log::message("singleton.setData() called\n"); }; float getData() const { Log::message("singleton.getData() called\n"); return 1.0f; } private: float data; static Singleton *instance; TexturePtr texture; }; // initialize a singleton instance Singleton *Singleton::instance = nullptr; // get a singleton instance Singleton *Singleton::get() { if (instance == nullptr) return new Singleton(); return instance; } // export the singleton class as a library named "singleton" void Singleton::registerClass() { Singleton *instance = Singleton::get(); // add a library Interpreter::addExternLibrary("singleton"); // add methods to the library Interpreter::addExternFunction("singleton.getData", MakeExternObjectFunction(instance, &Singleton::getData)); Interpreter::addExternFunction("singleton.setData", MakeExternObjectFunction(instance, &Singleton::setData)); } int Singleton::init() { // initialize a Texture return 1; } int Singleton::shutdown() { // delete a Texture return 1; } ```
- As a class with the *get()* method that returns a singleton instance. ```cpp class Singleton { public: // get a singleton instance static Singleton *get(); // export the class static void registerClass(); // create and delete engine and GPU resources (if any) int init(); int shutdown(); // class methods void setData(float data) { Log::message("singleton.setData() called\n"); }; float getData() const { Log::message("singleton.getData() called\n"); return 1.0f; } private: float data; static Singleton *instance; TexturePtr texture; }; // initialize a singleton instance Singleton *Singleton::instance = nullptr; // get a singleton instance Singleton *Singleton::get() { if (instance == nullptr) return new Singleton(); return instance; } // export the singleton class as an external class with getter void Singleton::registerClass() { // create an external class ExternClass<Singleton> *singleton_bindings = MakeExternClass<Singleton>(); singleton_bindings->addFunction("setData", &Singleton::setData); singleton_bindings->addFunction("getData", &Singleton::getData); Interpreter::addExternClass("Singleton", singleton_bindings); // add getter that returns a singleton instance Interpreter::addExternFunction("get_singleton", MakeExternFunction(&Singleton::get)); } int Singleton::init() { // initialize a Texture return 1; } int Singleton::shutdown() { // delete a Texture return 1; } ```


Then you can export the class to the script in one of the ways described [above](#export_classes). For example:


```cpp
#ifdef _WIN32
	int wmain(int argc,wchar_t *argv[]) {
#else
	int main(int argc,char *argv[]) {
#endif

	// export the class
	Singleton::registerClass();

	AppSystemLogic system_logic;
	AppWorldLogic world_logic;

	Unigine::EnginePtr engine(argc,argv);

	// Enter main loop.
	engine->main(&system_logic,&world_logic);

	return 0;
}

```


### Access from Script


- If the class has been exported as a library: ```cpp int init() { float data = singleton.getData(); return 1; } ```
- If the class has been exported with getter that returns the singleton instance: ```cpp int init() { Singleton singleton = get_singleton(); float data = singleton.getData(); return 1; } ```


## Exporting a Class with a Protected Constructor


If necessary, you can make a protected constructor of a C++ class available from scripts. To export it, you need to declare *Unigine::ExternClassConstructor<Class,List,Type>* template as a class friend.


> **Notice:** Up to 9 arguments are supported.


You can find the declaration of the template in the `<UnigineSDK>/include/UnigineInterpreter.h` header file.


> **Notice:** Protected class members cannot be exported.


```cpp
#include <UnigineEngine.h>
#include <UnigineInterpreter.h>

using namespace Unigine;

/******************************************************************************\
*
* User defined class
*
\******************************************************************************/

/*
*/
class MyClass {

	protected:

		 // declare the template as the friend of the MyClass
		template <class,typename,typename> friend class Unigine::ExternClassConstructor;

		// define the first constructor (without arguments)
		MyClass() {
			Log::warning("MyClass::MyClass() is called\n");
		}

		// define the second constructor with one argument
		MyClass(int v) {
			Log::warning("MyClass::MyClass(%d) is called\n",v);
		}
};

/******************************************************************************\
*
* Main
*
\******************************************************************************/

/*
 */
int main(int argc,char **argv) {

	// export a class.
	ExternClass<MyClass> *my_object = MakeExternClass<MyClass>();
	// add a default constructor without arguments
	my_object->addConstructor();
	// add a constructor with one argument
	my_object->addConstructor<int>();
	// register the exported class.
	Interpreter::addExternClass("MyExternObject",my_object);

	// Initialize the engine.
	Engine *engine = Engine::init(argc,argv);

	// Enter the main loop.
	engine->main();

	// Shut down the engine.
	Engine::shutdown();

	return 0;
}

```


You can also declare the corresponding template as the class friend for each of the protected constructors as follows:


```cpp
class MyClass {

	protected:

		// declare the templates as the friends of the MyClass
		// one to add the constructor without arguments
		friend class Unigine::ExternClassConstructor<MyClass,MakeTypeList<>::Type>;
		// and another to add the constructor with one argument
		friend class Unigine::ExternClassConstructor<MyClass,MakeTypeList<int>::Type>;

		// define the first constructor (without arguments)
		MyClass() {
			Log::warning("MyClass::MyClass() is called\n");
		}

		// define the second constructor with one argument
		MyClass(int v) {
			Log::warning("MyClass::MyClass(%d) is called\n",v);
		}
};

```


### Access from Scripts


After that, you can use the exported class in UnigineScript.


```cpp
// my_world.usc

int init() {

	// create an instance of the exported class
	MyExternObject object_0 = new MyExternObject();
	MyExternObject object_1 = new MyExternObject(1);

	return 1;
}

```


### Output


```text
MyClass::MyClass() is called
MyClass::MyClass(1) is called

```


## Exporting Inherited Classes


You can export C++ classes inherited from other C++ classes into UnigineScript and use them like other classes. Both base and derived classes are exported as it was described [above](#export_classes). For each derived class you should add a base class using the [*Unigine::ExternClass<Class>::addBaseClass()*](../../../../api/library/common/class.externclass_cpp.md#addBaseClass_ExternClassBase_ptr_void) function.


```cpp
my_derived_class->addBaseClass(my_base_class);
```


In this example we declare and export the following classes:


- **MyBase** - a base class
- **MyNode** - a class inherited from the MyBase class
- **MyObject** - a class inherited from the MyNode class


```cpp
#include <UnigineEngine.h>
#include <UnigineInterpreter.h>
#include <UnigineInterface.h>

#include "AppSystemLogic.h"
#include "AppWorldLogic.h"

using namespace Unigine;

//////////////////////////////////////////////////////////////////////////
// User defined class
//////////////////////////////////////////////////////////////////////////

class MyBase
{
public:
	MyBase()
	{
		Log::warning("MyBase::MyBase(): called\n");
	}
	virtual ~MyBase()
	{
		Log::warning("MyBase::~MyBase(): called\n");
	}

	void function()
	{
		Log::warning("MyBase::function(): called\n");
	}

	virtual const char *getName() = 0;

	static void registerClasses();
};

class MyNode : public MyBase
{
public:
	MyNode()
	{
		Log::warning("MyNode::MyNode(): called\n");
	}
	virtual ~MyNode()
	{
		Log::warning("MyNode::~MyNode(): called\n");
	}

	void function()
	{
		Log::warning("MyNode::function(): called\n");
	}

	virtual const char *getName()
	{
		return "MyNode";
	}

	static void registerNode(ExternClass<MyBase> *my_base);

};

class MyObject : public MyNode
{
public:
	MyObject()
	{
		Log::warning("MyObject::MyObject(): called\n");
	}
	virtual ~MyObject()
	{
		Log::warning("MyObject::~MyObject(): called\n");
	}

	void function()
	{
		Log::warning("MyObject::function(): called\n");
	}

	virtual const char *getName()
	{
		return "MyObject";
	}

	static void registerObject(ExternClass<MyNode> *my_node);
};

void MyBase::registerClasses() {

	// make a base class
	ExternClass<MyBase> *my_base = MakeExternClass<MyBase>();

	// add functions
	my_base->addFunction("function", &MyBase::function);
	my_base->addFunction("getName", &MyBase::getName);

	// register the MyBase class.
	Interpreter::addExternClass("MyBase", my_base);

	MyNode::registerNode(my_base);

}

void MyNode::registerNode(ExternClass<MyBase> *my_base) {

	// make a class inherited from the MyBase
	ExternClass<MyNode> *my_node = MakeExternClass<MyNode>();

	// add a default constructor without arguments
	my_node->addConstructor();
	my_node->addFunction("function", &MyNode::function);

	// add base class for MyNode class
	my_node->addBaseClass(my_base);

	// register the MyNode class.
	Interpreter::addExternClass("MyNode", my_node);

	MyObject::registerObject(my_node);
}

void MyObject::registerObject(ExternClass<MyNode> *my_node) {

	// Make a class inherited from the MyNode
	ExternClass<MyObject> *my_object = MakeExternClass<MyObject>();

	// add a default constructor without arguments
	my_object->addConstructor();

	// add a function
	my_object->addFunction("function", &MyObject::function);

	// add base class for MyObject class
	my_object->addBaseClass(my_node);

	// register the MyObject class.
	Interpreter::addExternClass("MyObject", my_object);
}

#ifdef _WIN32
int wmain(int argc, wchar_t *argv[])
#else
int main(int argc, char *argv[])
#endif
{

	MyBase::registerClasses();

	// init engine
	Unigine::EnginePtr engine(argc, argv);

	// UnigineLogic
	AppSystemLogic system_logic;
	AppWorldLogic world_logic;

	// enter main loop
	engine->main(&system_logic, &world_logic);

	return 0;
}

```


### Access from Scripts


After the registration, the exported classes can be used in UnigineScript just like any other classes.


```cpp
// my_world.usc

/*
*/

int init() {
	/////////////////////////////////

	log.message("\n");

	// object class
	MyObject object = new MyObject();
	object.function();
	log.message("%s\n", object.getName());

	// node class
	MyNode node = object;
	node.function();
	log.message("%s\n", node.getName());

	// base class
	MyBase base = node;
	base.function();
	log.message("%s\n", base.getName());

	// delete object
	delete object;

	/////////////////////////////////

	// show console
	engine.console.setActivity(1);

}

```


### Output


The following results will be printed to the console:


```text
MyBase::MyBase(): called
MyNode::MyNode(): called
MyObject::MyObject(): called
MyObject::function(): called
MyObject
MyNode::function(): called
MyObject
MyBase::function(): called
MyObject
MyObject::~MyObject(): called
MyNode::~MyNode(): called
MyBase::~MyBase(): called

```


## Memory Management for External Classes


By both creating and deleting variables that refer to the external classes, the corresponding scope should be set (world / system / editor). You should use pointers to the corresponding interpreter that are obtained via the following functions in order to set the required scope:


- [*Unigine::Engine::getWorldInterpreter()*](../../../../api/library/engine/class.engine_cpp.md#getWorldInterpreter_void_ptr)
- [*Unigine::Engine::getSystemInterpreter()*](../../../../api/library/engine/class.engine_cpp.md#getSystemInterpreter_void_ptr)
- [*Unigine::Engine::getEditorInterpreter()*](../../../../api/library/engine/class.engine_cpp.md#getEditorInterpreter_void_ptr)


Also you can use pointer to the current interpreter obtained via the [*Unigine::Interpreter::get()*](../../../../api/library/common/class.interpreter_cpp.md#get_void_ptr) function. If this function is called by the world interpreter, the current interpreter will be the world interpreter.


```cpp
Interpreter *interpreter = Unigine::Interpreter::get();
```


> **Notice:** If a C++ function is called from the script (world, system and editor), it means the current scope is already set and there is no need to call functions listed above.


If the corresponding scope is not set, memory leaks can occur when creating or deleting a variable.


For example, if you have a function defined on the script side and want to call it from the C++ code with a variable of the external class as an argument, you should set the script  runtime:


```cpp
#include <UnigineEngine.h>
#include <UnigineInterpreter.h>
#include <UnigineInterface.h>

#include <string>

using namespace Unigine;

class MyExternClass {

    public:

        MyExternClass() {}
        MyExternClass(const std::string &m) { my_member = m; }
        MyExternClass(const MyExternClass &other) { my_member = other.my_member; }
        ~MyExternClass() {}

    private:

        std::string my_member;

};

void my_update() {

    MyExternClass mec("hello!!!\n");
    Engine *engine = Engine::get();
	// get a pointer to the world interpreter
	Interpreter *world = (Interpreter*)engine->getWorldInterpreter();
	// create a variable of the external class
	Unigine::Variable v(world,TypeInfo(TypeID<MyExternClass*>()),new MyExternClass(mec),1,1);
	// specify the name of the function to call
	Unigine::Variable name("onMyUpdate");
	// run the world script function with the variable of the MyExternClass as the argument
   	engine->runWorldFunction(name,v);

}

int main(int argc,char **argv) {

    ExternClass<MyExternClass> *mec = MakeExternClass<MyExternClass>();
    Interpreter::addExternClass("MyExternClass",mec);

    Engine *engine = Engine::init(argc,argv);
    while(engine->isDone() == 0) {
		engine->update();
		engine->postUpdate();
		engine->swap();

        my_update();
    }

    Engine::shutdown();
    return 0;
}

```


> **Notice:** In the example above *Variable v* is a static variable, that is why when leaving the scope of its visibility, it is necessary to reset the context.


```cpp
// the world script function which receives a variable referring to the external class
void onMyUpdate(MyExternClass v) {
	// some code
}

int init() {
	// some code
	return 1;
}

int shutdown() {
	// some code
	return 1;
}

int update() {
	// some code
	return 1;
}

```
