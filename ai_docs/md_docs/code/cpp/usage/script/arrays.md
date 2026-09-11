# UnigineScript Containers

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


You can work with UnigineScript [containers](../../../../code/uniginescript/language/containers/index.md) from C++ side via Unigine API, that is, with:


- [Vectors](../../../../code/uniginescript/language/containers/index.md#vector)
- [Maps](../../../../code/uniginescript/language/containers/index.md#maps)


### See also


An example can be found in `<UnigineSDK>/source/samples/Api/Scripts/Arrays/` directory.


## Container Export Example


Unigine vectors and maps can be accessed via:


- *[ArrayVector](../../../../api/library/containers/class.arrayvector_cpp.md)* class and the *[ArrayVector::get()](../../../../api/library/containers/class.arrayvector_cpp.md#get_void_ptr_const_Variable_ref_ArrayVector)* function for vectors.
- *[ArrayMap](../../../../api/library/containers/arraymap/class.arraymap_cpp.md)* and the *[ArrayMap::get()](../../../../api/library/containers/arraymap/class.arraymap_cpp.md#get_void_ptr_const_Variable_ref_ArrayMap)* function for maps.


> **Notice:** To enumerate all of the *ArrayMap* elements, use the special *[ArrayMap::Iterator](../../../../api/library/containers/arraymap/class.arraymap.iterator_cpp.md)* class.


### C++ Side


Create setter and getter functions that receive Unigine containers and handle their elements. Then, export the created functions in order to use them in the script.


> **Notice:** You should specify the array declaration as the last argument of the *MakeExternFunction()* if your array functions receive an array as an argument.
> ```cpp
> MakeExternFunction(&my_array_vector_set,"[]")
> ```


```cpp
#include <string>
#include <UnigineInterpreter.h>
#include <UnigineEngine.h>

/*
*/
using namespace Unigine;

/******************************************************************************\
*
* User defined array functions
*
\******************************************************************************/

/*
*/
void my_array_vector_set(const Variable &id,int index,const Variable &v) {
	ArrayVector vector = ArrayVector::get(Interpreter::get(),id);
	vector.set(index,v);
}

Variable my_array_vector_get(const Variable &id,int index) {
	ArrayVector vector = ArrayVector::get(Interpreter::get(),id);
	return vector.get(index);
}

/*
 */
void my_array_map_set(const Variable &id,const Variable &key,const Variable &v) {
	ArrayMap map = ArrayMap::get(Interpreter::get(),id);
	map.set(key,v);
}

Variable my_array_map_get(const Variable &id,const Variable &key) {
	ArrayMap map = ArrayMap::get(Interpreter::get(),id);
	return map.get(key);
}

/*
 */
void my_array_vector_generate(const Variable &id) {
	ArrayVector vector = ArrayVector::get(Interpreter::get(),id);
	vector.clear();
	for(int i = 0; i < 4; i++) {
		vector.append(Variable(i * i));
	}
	vector.remove(0);
	vector.append(Variable("128"));
}

void my_array_map_generate(const Variable &id) {
	ArrayMap map = ArrayMap::get(Interpreter::get(),id);
	map.clear();
	for(int i = 0; i < 4; i++) {
		map.append(Variable(i * i),Variable(i * i));
	}
	map.remove(Variable(0));
	map.append(Variable(128),Variable("128"));
}

/*
 */

void my_array_vector_enumerate(const Variable &id) {
	ArrayVector vector = ArrayVector::get(Interpreter::get(),id);
	for(int i = 0; i < vector.size(); i++) {
		Log::message("%d: %s\n",i,vector.get(i).getTypeInfo().get());
	}
}

void my_array_map_enumerate_forward(const Variable &id) {
	ArrayMap map = ArrayMap::get(Interpreter::get(),id);
	ArrayMap::Iterator end = map.end();
	for(ArrayMap::Iterator it = map.begin(); it != end; ++it) {
		Log::message("%d: %s\n",it.key().getInt(),it.get().getTypeInfo().get());
	}
}

void my_array_map_enumerate_backward(const Variable &sid) {
	ArrayMap map = ArrayMap::get(Interpreter::get(),id);
	ArrayMap::Iterator end = map.end();
	for(ArrayMap::Iterator it = map.back(); it != end; --it) {
		Log::message("%d: %s\n",it.key().getInt(),it.get().getTypeInfo().get());
	}
}

/******************************************************************************\
*
* Main
*
\******************************************************************************/

/*
*/
int main(int argc,char **argv) {

	// export functions
	Interpreter::addExternFunction("my_array_vector_set",MakeExternFunction(&my_array_vector_set,"[]"));
	Interpreter::addExternFunction("my_array_vector_get",MakeExternFunction(&my_array_vector_get,"[]"));
	Interpreter::addExternFunction("my_array_map_set",MakeExternFunction(&my_array_map_set,"[]"));
	Interpreter::addExternFunction("my_array_map_get",MakeExternFunction(&my_array_map_get,"[]"));
	Interpreter::addExternFunction("my_array_vector_generate",MakeExternFunction(&my_array_vector_generate,"[]"));
	Interpreter::addExternFunction("my_array_map_generate",MakeExternFunction(&my_array_map_generate,"[]"));
	Interpreter::addExternFunction("my_array_vector_enumerate",MakeExternFunction(&my_array_vector_enumerate,"[]"));
	Interpreter::addExternFunction("my_array_map_enumerate_forward",MakeExternFunction(&my_array_map_enumerate_forward,"[]"));
	Interpreter::addExternFunction("my_array_map_enumerate_backward",MakeExternFunction(&my_array_map_enumerate_backward,"[]"));

	// init engine
	Engine *engine = Engine::init(argc,argv);

	// enter main loop
	engine->main();

	// shutdown engine
	Engine::shutdown();

	return 0;
}

```


### Access from Script


And here is how the exported custom functions can be used back in UnigineScript:


```cpp
// my_world.usc

/*
*/
int init() {

	/////////////////////////////////

	log.warning("\naccess to vector\n\n");

	int vector[] = ( 0, 1 );

	for(int i = 0; i < 2; i++) {
		log.message("vector %d: %s\n",i,typeinfo(my_array_vector_get(vector,i)));
		my_array_vector_set(vector,i,string(i));
		log.message("vector %d: %s\n",i,typeinfo(my_array_vector_get(vector,i)));
	}

	/////////////////////////////////

	log.warning("\naccess to map\n\n");

	int map[] = ( 0 : 0, 1 : 1 );

	for(int i = 0; i < 2; i++) {
		log.message("map %d: %s\n",i,typeinfo(my_array_map_get(map,i)));
		my_array_map_set(map,i,string(i));
		log.message("map %d: %s\n",i,typeinfo(my_array_map_get(map,i)));
	}

	/////////////////////////////////

	log.warning("\nvector generation\n\n");

	my_array_vector_generate(vector);

	foreachkey(int i; vector) {
		log.message("vector %d: %s\n",i,typeinfo(vector[i]));
	}

	/////////////////////////////////

	log.warning("\nmap generation\n\n");

	my_array_map_generate(map);

	foreachkey(int i; map) {
		log.message("map %d: %s\n",i,typeinfo(map[i]));
	}

	/////////////////////////////////

	log.warning("\nvector enumeration\n\n");

	my_array_vector_enumerate(vector);

	/////////////////////////////////

	log.warning("\nmap forward enumeration\n\n");

	my_array_map_enumerate_forward(map);

	/////////////////////////////////

	log.warning("\nmap backward enumeration\n\n");

	my_array_map_enumerate_backward(map);

	/////////////////////////////////

	// show console
	engine.console.setActivity(1);

	return 1;
}

```


### Output


The following result will be printed into the console:


```text
access to vector

vector 0: int: 0
vector 0: string: "0"
vector 1: int: 1
vector 1: string: "1"

access to map

map 0: int: 0
map 0: string: "0"
map 1: int: 1
map 1: string: "1"

vector generation

vector 0: int: 1
vector 1: int: 4
vector 2: int: 9
vector 3: string: "128"

map generation

map 1: int: 1
map 4: int: 4
map 9: int: 9
map 128: string: "128"

vector enumeration

0: int: 1
1: int: 4
2: int: 9
3: string: "128"

map forward enumeration

1: int: 1
4: int: 4
9: int: 9
128: string: "128"

map backward enumeration

128: string: "128"
9: int: 9
4: int: 4
1: int: 1

```
