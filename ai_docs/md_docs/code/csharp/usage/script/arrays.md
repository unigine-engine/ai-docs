# UnigineScript Containers

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


You can work with UnigineScript [containers](../../../../code/uniginescript/language/containers/index.md) from C# side via Unigine API, that is, with:


- [Vectors](../../../../code/uniginescript/language/containers/index.md#vector)
- [Maps](../../../../code/uniginescript/language/containers/index.md#maps)


### See also


An example can be found in `<UnigineSDK>/source/csharp/samples/Api/Scripts/Arrays/` directory.


## Container Export Example


Unigine vectors and maps can be accessed via:

- *ArrayVector* class and the *ArrayVector.Get()* function for vectors. The *[ArrayVector::get()](../../../../api/library/containers/class.arrayvector_cpp.md#get_void_ptr_const_Variable_ref_ArrayVector)* C++�API function and the�*[ArrayVector](../../../../api/library/containers/class.arrayvector_cpp.md)* C++ API class have the same behavior.
- *ArrayMap* class and the *ArrayMap.Get()* function for maps. The *[ArrayMap](../../../../api/library/containers/arraymap/class.arraymap_cpp.md)* C++�API class and the�*[ArrayMap::get()](../../../../api/library/containers/arraymap/class.arraymap_cpp.md#get_void_ptr_const_Variable_ref_ArrayMap)* C++ API function have the same behavior.


### C# Side


Create setter and getter functions that receive Unigine containers and handle their elements. Then, export the created functions in order to use them in the script.


> **Notice:** You should specify the array declaration as the last argument of the Function if your array functions receive an array as an argument.
>
>
> ```csharp
> Function(my_array_vector_set,"[]")
> ```
>
>
> The postfix of Function shows the number of arguments (up to **8** arguments) and the type of return value:
>
>
> - **no postfix** - void.
> - **i** - int.
> - **d** - double.
> - **f** - float.
> - **s** - string.
> - **v** - Unigine.Variable (the same class as the [C++ API Unigine::Variable](../../../../api/library/common/class.variable_cpp.md) class).


```csharp
using System;
using Unigine;

/*
*/
class UnigineApp {

	/*
	*/
	private static void my_array_vector_set(Variable id,Variable index,Variable val) {
		ArrayVector vector = ArrayVector.Get(Interpreter.get(),id);
		vector.Set(index.GetInt(),val);
	}

	private static Variable my_array_vector_get(Variable id,Variable index) {
		ArrayVector vector = ArrayVector.Get(Interpreter.get(),id);
		return vector.Get(index.GetInt());
	}

	/*
	 */
	private static void my_array_map_set(Variable id,Variable key,Variable val) {
		ArrayMap map = ArrayMap.Get(Interpreter.get(),id);
		map.Set(key,val);
	}

	private static Variable my_array_map_get(Variable id,Variable key) {
		ArrayMap map = ArrayMap.Get(Interpreter.get(),id);
		return map.Get(key);
	}

	/*
	 */
	private static void my_array_vector_generate(Variable id) {
		ArrayVector vector = ArrayVector.Get(Interpreter.get(),id);
		vector.Clear();
		for(int i = 0; i < 4; i++) {
			vector.Append(new Variable(i * i));
		}
		vector.Remove(0);
		vector.Append(new Variable("128"));
	}

	private static void my_array_map_generate(Variable id) {
		ArrayMap map = ArrayMap.Get(Interpreter.get(),id);
		map.Clear();
		for(int i = 0; i < 4; i++) {
			map.Append(new Variable(i * i),new Variable(i * i));
		}
		map.Remove(new Variable(0));
		map.Append(new Variable(128),new Variable("128"));
	}

	/*
	 */

	private static void my_array_vector_enumerate(Variable id) {
		ArrayVector vector = ArrayVector.Get(Interpreter.get(),id);
		for(int i = 0; i < vector.Size; i++) {
			Log.Message("{0}: {1}\n",i,vector.Get(i).TypeInfo);
		}
	}

	/* entry point
	*/
	[STAThread]
	static void Main(string[] args) {

		// export functions
		Interpreter.AddExternFunction("my_array_vector_set",new Interpreter.Function3(my_array_vector_set),"[]");
		Interpreter.AddExternFunction("my_array_vector_get",new Interpreter.Function2v(my_array_vector_get),"[]");
		Interpreter.AddExternFunction("my_array_map_set",new Interpreter.Function3(my_array_map_set),"[]");
		Interpreter.AddExternFunction("my_array_map_get",new Interpreter.Function2v(my_array_map_get),"[]");
		Interpreter.AddExternFunction("my_array_vector_generate",new Interpreter.Function1(my_array_vector_generate),"[]");
		Interpreter.AddExternFunction("my_array_map_generate",new Interpreter.Function1(my_array_map_generate),"[]");
		Interpreter.AddExternFunction("my_array_vector_enumerate",new Interpreter.Function1(my_array_vector_enumerate),"[]");

		// init engine
		Engine engine = Engine.Init(Engine.VERSION,args);

		// enter main loop
		engine.Main();

		// shutdown engine
		Engine.Shutdown();
	}
}

```


### Access from Script


And here is how the exported custom functions can be used back in UnigineScript:


```cpp
// array.cpp

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

```
