# Templates

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


*Templates* are used to generate different code chunks, functions and classes. Each template starts with the *template* keyword and sets an identifier and a code chunk, a function or a class, by which this identifier will be replaced when using the template.


The templates should be used instead of the [*#define*](../../../code/uniginescript/language/preprocessor.md#define) preprocessor directive. The main differences from [*#define*](../../../code/uniginescript/language/preprocessor.md#define) are the following:

- The templates support syntax highlighting.
- The templates work relative to a [scope](../../../code/uniginescript/language/scope.md#scope) (while *#define* has the global scope).


### See Also


- Description of the [*#define*](../../../code/uniginescript/language/preprocessor.md#define) and [*#*](../../../code/uniginescript/language/preprocessor.md#hash) preprocessor directives
- Samples located in `data/samples/systems/noise_02.cpp` and `data/samples/widgets/ui_01.cpp`


## Generating Code Chunks


A template that is used to generate a code chunk has the following syntax:

```cpp
template template_name<ARG_NAME> {
	code_chunk
}

```

 The *ARG_NAME* argument is used in the code chunk. It will be replaced by a value that is specified when using the template.
> **Notice:** You can specify several arguments for the template, if it is required.

 The following example demonstrates how to declare the template with 2 arguments and then generate a code from it:
```cpp
template print<STRING,DIGIT> {
	log.message("%s, ",STRING);
	log.message("%d\n",DIGIT);
}

// generate a code chunk
print<typeinfo(12),17>;
print<"12",17>;

// The following code is generated:
// log.message("%s, ","int: 12");
// log.message("%d\n",17);
// log.message("%s, ","12");
// log.message("%d\n",17);

```


To turn a template argument into a string, use [***#***](../../../code/uniginescript/language/preprocessor.md#hash) before the argument:

```cpp
template print<DIGIT> {
	log.message("%d\n",DIGIT);
	log.message("text_%s",#DIGIT);
}

print<17>;

// Output:
// 17
// text_17

```


## Generating Functions


Also it is possible to create a template that generates a function instead of the [code chunk](#template_code). This function will replace the identifier that is set by a template. The syntax of the function template is the following:

```cpp
template template_name<ARG_NAME> void ARG_NAME {
	function_code
}

```

 By using such template, you can generate functions with any names.
To declare several functions in one template, simply enclose the functions in curly braces:

```cpp
template template_name<ARG_NAME> {
	void func1_ ## ARG_NAME { function_code; }
	void func2_ ## ARG_NAME { function_code; }
}

```

 Here the ***##*** operator is used to concatenate 2 parts of a function name, so you cannot put it as the first or the last token in the function declaration.
> **Notice:** The white spaces before and after the ***##*** operator are required.


The following examples demonstrate how to:

- Declare a template with 3 arguments and then generate a function from it: ```cpp template sum_template<NAME,A0,A1> void NAME() { log.message("%s\n",typeinfo(A0 + A1)); } // generate the sum() function that adds 1 to 2 sum_template<sum,1,2>; // call the generated function sum(); // Output: int: 3 ```
- Declare several functions in one template and then use this template in the code in order to generate class member functions: ```cpp template setget<TYPE,NAME,VALUE> { void set ## NAME(TYPE v) { VALUE = v; } TYPE get ## NAME() { return VALUE; } } class Foo { int a,b,c; // generate the following functions: // void setA(int v) { a = v; } // int getA() { return a; } setget<int,A,a>; // void setB(int v) { b = v; } // int getB() { return b; } setget<int,B,b>; // void setC(string v) { c = v; } // string getC() { return c; } setget<string,C,c>; void info() { log.message("%d %d %s\n",a,b,c); } }; Foo f = new Foo(); // call the generated member functions f.setA(12); f.setB(13); f.setC("Sample string"); f.info(); // Output: 12 13 Sample string ```


## Generating Classes


The syntax of the template that generates a class is the following:

```cpp
template template_name<ARG_NAME> {
	class ARG_NAME {
		class_members
	};
}

```

 By using such template, you can generate classes with any names.  Also you can use the ***##*** operator to construct a class name, for example:
```cpp
template my_class<NAME> {
    class My ## NAME {
        My ## NAME() {
            log.message(__FUNC__ + ": called\n");
        }
        ~My ## NAME() {
            log.message(__FUNC__ + ": called\n");
        }
    };
}

// generate the Foo class
my_class<Foo>;

MyFoo f = new MyFoo();
delete f;

```
