# Data Structure Export

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Data structures (together with their constructors and accessors, if necessary) can be exported into UnigineScript.


### See Also


An example located in the `<UnigineSDK>/source/samples/Api/Scripts/Structures/` folder.


## Data Structure Export Example


Data structures are exported in the same way as C++ [classes](../../../../code/cpp/usage/script/classes.md):


1. Create an external class based on your C++ data structure via *MakeExternClass()*.
2. Add constructors to the external class.
3. Add methods to the external class.
4. Register the external class via *[Unigine::Interpreter::addExternClass()](../../../../api/library/common/class.interpreter_cpp.md#addExternClass_const_char_ptr_ExternClassBase_ptr_int_void)*.


Here is how different data structures can be exported from C++ into UnigineScript:


```cpp
#include <string>
#include <map>

#include <UnigineEngine.h>
#include <UnigineInterpreter.h>
#include <UnigineInterface.h>

/*
*/
using namespace Unigine;

/******************************************************************************\
*
* Data structure
*
\******************************************************************************/

/*
 */
typedef struct mydata{
	std::string name;
	Unigine::Math::ivec3 vec;
	const char *getName() const { return name.c_str(); }
} mydata;

std::map<std::string, mydata> mymap;

/*
 */
void get_data(const Variable &id) {

	void *interpreter = Interpreter::get();
	ArrayMap map = ArrayMap::get(interpreter,id);
	for(std::map<std::string,mydata>::iterator it = mymap.begin(); it != mymap.end(); ++it) {
		map.append(Variable(it->first.c_str()),Variable(interpreter,TypeInfo(TypeID<mydata*>()),&it->second));
	}
}

/*
 */
struct MyVector {

	MyVector() : x(0.0f), y(0.0f), z(0.0f), w(0.0f) {

	}

	float x;
	float y;
	float z;
	float w;
};

/******************************************************************************\
*
* Main
*
\******************************************************************************/

/*
*/
int main(int argc,char **argv) {

	// export a data structure as an extern class
	ExternClass<mydata> *mydata_export = MakeExternClass<mydata>();
	// add a default constructor
	mydata_export->addConstructor();
	// export structure accessor
	mydata_export->addFunction("getName",&mydata::getName);
	// register the exported class
	Interpreter::addExternClass("mydata",mydata_export);
	// register the external function
	Interpreter::addExternFunction("get_data2",MakeExternFunction(&get_data,"[]"));

	// Fill a map
	mydata data;

	data.name = std::string("map_data_0");
	mymap[std::string("key_0")] = data;

	data.name = std::string("map_data_1");
	mymap[std::string("key_1")] = data;

	// export a data structure as an extern class
	ExternClass<MyVector> *my_vector = MakeExternClass<MyVector>();
	// add the constructor
	my_vector->addConstructor();
	// register structure accessors
	my_vector->addSetFunction("setX",&MyVector::x);
	my_vector->addGetFunction("getX",&MyVector::x);
	my_vector->addSetFunction("setY",&MyVector::y);
	my_vector->addGetFunction("getY",&MyVector::y);
	my_vector->addSetFunction("setZ",&MyVector::z);
	my_vector->addGetFunction("getZ",&MyVector::z);
	my_vector->addSetFunction("setW",&MyVector::w);
	my_vector->addGetFunction("getW",&MyVector::w);
	// register the external class
	Interpreter::addExternClass("MyVector",my_vector);

	// Initialize the engine.
	Engine *engine = Engine::init(0,argc,argv);

	// Enter the main loop and call update() function in the loaded world script.
	engine->main();

	// Shut down the engine and call shutdown() function in the loaded world script.
	Engine::shutdown();

	return 0;
}

```


### Access from Scripts


After registration, the exported data structure can be used in UnigineScript just like a usual class.


```cpp
// my_world.usc

int init() {

	// Get data from a map.
	mydata data2[];
	get_data2(data2);
	foreachkey(string key; data2) {
		log.message("%s: %s\n",key,data2[key].getName());
	}

	log.message("\n");

	// make extern struct
	MyVector vector = new MyVector();

	// set members
	vector.setX(1.0f);
	vector.setY(2.0f);
	vector.setZ(4.0f);
	vector.setW(8.0f);

	// get members
	log.warning("MyVector: (%g,%g,%g,%g)\n",vector.getX(),vector.getY(),vector.getZ(),vector.getW());

	// delete extern struct
	delete vector;

	// show console
	engine.console.setActivity(1);

	return 1;
}

```


### Output


The following result will be printed into the console:


```text
key_0: map_data_0
key_1: map_data_1

MyVector: (1,2,3,4,8)

```
