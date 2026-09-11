# Variable Export

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


To use variables from your C++ code in UnigineScript, you need to export them. After that, they will be available on the script side.


- External variables are **read-only**.
- If a value of a registered variable is changed in the C++ code, it instantly **changes** in the script as well (unlike in case of [constants](../../../../code/cpp/usage/script/constants.md)).


### See also


An example can be found in `<UnigineSDK>/source/samples/Api/Scripts/Variable/` directory.


## Variable Export Example


Let's say, you declared a number of variables on C++ side. To export them, you will need to do the following:


1. Create a pointer to an external variable via *MakeExternVariable()*.
2. Register the variable via *[Unigine::Interpreter::addExternVariable()](../../../../api/library/common/class.interpreter_cpp.md#addExternVariable_const_char_ptr_ExternVariableBase_ptr_int_void)*.
3. All variables are exported into a global namespace. To limit the scope of variable, use [library namespace](../../../../code/cpp/usage/script/namespace.md).


```cpp
#include <UnigineInterpreter.h>
#include <UnigineInterface.h>
using namespace Unigine;

int main(int argc,char **argv) {

	int i = 2;
	float f = 1.5f;
	vec3 v3 = vec3(1.0f,2.0f,3.0f);
	vec4 v4 = vec4(0.1f,0.2f,0.3f,0.4f);
	float m[16] = { 0.0f, 1.0f, 2.0f, 3.0f, 4.0f, 5.0f, 6.0f, 7.0f,\
					8.0f, 9.0f, 10.0f, 11.0f, 12.0f, 13.0f, 14.0f, 15.0f };
	mat4 mat = mat4(m);
	quat q = quat(0.0f,0.0f,1.0f,0.0f);

	// export a variable and specify a name to access it from Unigine scripts
	Interpreter::addExternVariable("integer",MakeExternVariable(&i));
	Interpreter::addExternVariable("float_point",MakeExternVariable(&f));
	Interpreter::addExternVariable("vector3",MakeExternVariable(&v3));
	Interpreter::addExternVariable("vector4",MakeExternVariable(&v4));
	Interpreter::addExternVariable("matrix4",MakeExternVariable(&mat));
	Interpreter::addExternVariable("quaternion",MakeExternVariable(&q));

	Engine *engine = Engine::init(argc,argv);

	// enter the main loop
	while(engine->isDone() == 0) {
		engine->update();
		engine->render();
		engine->swap();
		// if a variable value is changed after it was registered, in scripts the value will be changed as well
		i = 42;
	}

	// engine shutdown
	Engine::shutdown();

}

```


### Access from Scripts


After the registration, you can access variables from a script by their registered names:


```cpp
// my_world.usc
int init() {

	log.message("Integer is %d\nFloat is %f\n",integer,float_point);
	log.message("Vector3 x is %f\nVector3 y is %f\n",vector3.x,vector3.y);
	log.message("Vector4 w is %f\n",vector4.w);
	log.message("Matrix4 m10 is %f\nMatrix4 m11 is %f\n",matrix4.m10,matrix4.m11);

	return 1;
}

```


### Output


The following results will be printed into the console after launching the application:


```text
Integer is 2
Float is 1.500000
Vector3 x is 1.000000
Vector3 y is 2.000000
Vector4 w is 0.400000
Matrix4 m10 is 1.000000
Matrix4 m11 is 5.000000

```


If you reload the world, the integer value that has been changed on the C++ side will appear in the console:


```text
Integer is 42
Float is 1.500000
Vector3 x is 1.000000
Vector3 y is 2.000000
Vector4 w is 0.400000
Matrix4 m10 is 1.000000
Matrix4 m11 is 5.000000

```
