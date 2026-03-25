# Unigine::Reflection Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to create reflections for user or extern classes and namespaces. It allows you to get names and custom attribute strings for all variables, arrays, user classes and namespaces within it. Such attributes can be used for smart automatic code generation for GUI or any game logic. For example, it is possible to get attributes, parse them in the required way, and feed them to the [Expression](../../../api/library/common/class.expression_usc.md) which will compile the resulting code.


### Usage Example


The sample below is showing how to create an XML serialization system for any instance classes by simple adding of special attributes to getter and setter functions.


```cpp
#include <unigine.h>

/*
 * Implementation of a MyClass, the user class with special functions for XML serialization
 */

class MyClass {

  private:

    int int_value;
    vec3 vec3_value;

  public:

    [serialize:int_value]
    int getIntValue() {
      return int_value;
    }

    [serialize:int_value]
    void setIntValue(int value) {
      int_value = value;
    }

    [serialize:vec3_value]
    vec3 getVec3Value() {
      return vec3_value;
    }

    [serialize:vec3_value]
    void setVec3Value(vec3 value) {
      vec3_value = value;
    }
};

/*
 * Serialize XML for any class instance
 */

Xml serialize(int instance) {

  // specify only simple types of data to be serialized
  string function_types[] = (
    "int"     : "int",
    "float"   : "float",
    "double"  : "double",
    "vec3"    : "vec3",
    "Vec3"    : "Vec3",
    "vec4"    : "vec4",
    "Vec4"    : "Vec4",
    "string"  : "string",
  );

  // create a reflection class
  Reflection reflection = new Reflection();

  // return NULL value if the instance cannot be reflected
  if(reflection.reflect(instance) == false) return NULL;

  // create an XML class instance
  Xml xml = new Xml();
  xml.setName("instance");

  // write the instance class name as an attribute
  xml.setArg("type",reflection.getName());

  // simple check of an attribute function for serialization
  int is_serialize(string str,string &name) {

    // the attribute string must be like [serialize:%parameter_name]
    string ret[0];
    strsplit(str,":",ret);
    if(ret.size() < 2) return false;
    if(trim(ret[0]) != "serialize") return false;
    name = ret[1];
    return true;
  }

  // a loop for all class functions
  forloop(int i = 0; reflection.getNumFunctions()) {
    string name = "";

    // check function for a "serialize" attribute
    if(is_serialize(reflection.getFunctionAttribute(i),name) == false) continue;

    // specify get and check function types
    string type = function_types.check(reflection.getFunctionType(i),"");
    if(type == "") continue;

    // specify that the parameter "get" function must have zero arguments
    if(reflection.getNumFunctionArgs(i) != 0) continue;

    // add parameter child to XML
    Xml parameter = xml.addChild("parameter");
    parameter.setArg("name",name);
    parameter.setArg("type",type);

    // call the "get" function instance to get a parameter value
    parameter.setData(string(instance.call(reflection.getFunctionID(i))));
  }

  // return the XML with instance parameters data
  return xml;
}

int init() {

  // create MyClass instance
  MyClass instance = new MyClass();

  // set the parameters to the class instance
  instance.setIntValue(33);
  instance.setVec3Value(vec3(1.2f,2.3f,3.1f));

  // create the XML
  Xml xml = serialize(instance);

  // write XML to the file
  if(xml != NULL) {
    xml.save("my_class.xml");
  }

  return 1;
}

```


As a result we will get the XML file with the following content:


```xml
<?xml version="1.0" encoding="utf-8"?>
<instance type="MyClass">
  <parameter name="int_value" type="int">33</parameter>
  <parameter name="vec3_value" type="vec3">1.2 2.3 3.1</parameter>
</instance>

```


## Reflection Class

### Members

---

## Reflection ( )

Constructor. After creating a Reflection instance, a [reflect()](#reflect_void_ptr_const_Variable_ref_int) function should be called.
## string getArrayAttribute ( int num )

Returns the attribute of the given array.
### Arguments

- *int* **num** - Array index.

### Return value

Array attribute.
## string getArrayName ( int num )

Returns the name of the given array.
### Arguments

- *int* **num** - Array index.

### Return value

Array name.
## string getAttribute ( )

Returns the attribute of a namespace or a class.
### Return value

Attribute.
## string getBaseName ( )

Returns a base namespace name used when calling reflection methods.
### Return value

Base namespace name.
## string getClassAttribute ( int num )

Returns the attribute of the given class.
### Arguments

- *int* **num** - Class index.

### Return value

Class attribute.
## string getClassName ( int num )

Returns the name of the argument.
### Arguments

- *int* **num** - Class index.

### Return value

Class name.
## string getFunctionArgName ( int num , int arg )

Returns the name of the function argument.
### Arguments

- *int* **num** - Function index.
- *int* **arg** - Argument index.

### Return value

Argument name.
## string getFunctionArgType ( int num , int arg )

Returns the type of the function argument (INT, LONG, VEC3, etc.).
### Arguments

- *int* **num** - Function index.
- *int* **arg** - Argument index.

### Return value

Argument type.
## string getFunctionAttribute ( int num )

Returns the attribute of the given function.
### Arguments

- *int* **num** - Function index.

### Return value

Function attribute.
## int getFunctionID ( int num )

Returns the ID of the user-defined function.
### Arguments

- *int* **num** - Function index.

### Return value

Function ID.
## string getFunctionName ( int num )

Returns the name of the given function.
### Arguments

- *int* **num** - Function index.

### Return value

Function name.
## string getFunctionType ( int num )

Returns the type of the specified function.
### Arguments

- *int* **num** - The function ID.

### Return value

Function type.
## string getName ( )

Returns a namespace name used when calling reflection methods.
### Return value

Namespace name.
## string getNameSpaceAttribute ( int num )

Returns the attribute of the given namespace.
### Arguments

- *int* **num** - Namespace index.

### Return value

Namespace attribute.
## string getNameSpaceName ( int num )

Returns the name of the given namespace.
### Arguments

- *int* **num** - Namespace index.

### Return value

Namespace name.
## int getNumArrays ( )

Returns the total number of arrays in the namespace or a class.
### Return value

Number of arrays.
## int getNumClasses ( )

Returns the total number of classes in the namespace.
### Return value

Number of classes.
## int getNumFunctionArgs ( int num )

Returns the number of arguments of the function.
### Arguments

- *int* **num** - Function index.

### Return value

Number of function arguments.
## int getNumFunctions ( )

Returns the total number of functions in the namespace or a class.
### Return value

Number of functions.
## int getNumNameSpaces ( )

Returns the total number of namespaces in the namespace or a class.
### Return value

Number of namespaces.
## int getNumVariables ( )

Returns the total number of variables in the namespace or a class.
### Return value

Number of variables.
## string getVariableAttribute ( int num )

Returns the attribute of the given variable.
### Arguments

- *int* **num** - Variable index.

### Return value

Variable attribute.
## string getVariableName ( int num )

Returns the name of the given variable.
### Arguments

- *int* **num** - Variable index.

### Return value

Variable name.
