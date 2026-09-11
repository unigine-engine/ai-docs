# Switch-Case

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The *switch-case* conditional statement is an alternative to the [*if-else* statement](../../../../../code/uniginescript/language/control_statements/selection_statements/if_else.md). It consists of a*switch* part, which holds an expression that should evaluate to an integer result, and several *case* blocks, which define possible integer results and corresponding actions. This statement is more efficient than the *if-else* statement and should be preferred, if the tested expression returns an integer and there will be multiple branches based on its result.


### Syntax


```cpp
switch(expression) {
	case constant:
		// some_code;
		break;
	// �;
	default:
		// some_code;
		break;
}

```


### Parts


- *expression* is a condition.
- *constant* can be an integer or an [enumeration member](../../../../../code/uniginescript/language/data_types.md#enum) or an [exported variable](../../../../../code/cpp/usage/script/variables.md). It can also be *typeid(type)* statement (see the example below
- *default* is a label that specifies a code block which will be executed when none of the constants listed are matched. The *default* block is optional.


### Example


```cpp
enum {
	THREE = 3,
};

switch(6 * 1) {
	case 1:
		log.message("one\n");
		break;
	case 2:
		log.message("two\n");
		break;
	case THREE:
		log.message("three\n");
		break;
	case 4:
	case 5:
		log.message("four, five\n");
		break;
	default:
		log.message("default\n");
		break;

```


Note that if there is no *break* at the end of a *case* block, script execution "falls through" to the next *case* block, as if its value also matched the result of the tested expression.


> **Notice:** - There should be no whitespace between the word "default" and the following colon. Also, there should be no other labels with the name "default" within the script.
> - Values for *case* comparisons are pre-compiled. Therefore, if an exported variable is used as a constant in such a comparison, and if its value is changed in the C++ code, the old value will be used nevertheless.


It is possible to use *typeid(variable_type)* as a constant for a case within a switch. This function checks if the variable belongs to a specified type and performs a corresponding action.


```cpp
Variable data = node.getData();
switch(typeid(data)) {
	case typeid(int):
		log.message("int\n");
		break;
	case typeid(float):
		log.message("float\n");
		break;
	case typeid(vec3):
		log.message("vec3\n");
		break;
	case typeid(vec4):
		log.message("vec4\n");
		break;
	case typeid(string):
		log.message("string\n");
		break;
}

```
