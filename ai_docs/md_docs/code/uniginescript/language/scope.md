# Scope. Namespaces

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## Scope


**Scope** is a region of a program that determines accessibility of an identifier (whether a variable, enum, function, class, namespace and so on) that is used in this program.

> **Notice:** For variables, scope determines their accessibility and lifetime. However, lifetime is not limited by a current scope (see details [below](#lifetime)).


How large the scope is depends on where the identifier is declared. For example, if a variable is declared at the top of a class then it will be accessible to all of the class methods. If it�s declared in a method then it can only be used in that method.


A pair of curly braces (**{}**) defines a new scope.


For example:

```cpp
namespace Foo {
    int a = 10;
}
int a = 5;
log.message("Foo::a is %d, a is %d", Foo::a,a);

```


```text
Foo::a is 10, a is 5
```


If an identifier is declared outside all blocks enclosed by curly braces, it will have the *global scope*. It means that such identifier will be accessible anywhere in the program after its declaration.

> **Notice:** If a function is not a class member and it is declared outside all blocks, it will also have the global scope.

 For example:
```cpp
// function foo() is in the global scope
int foo() { log.message("Function in the global scope\n"); }

class Foo {
    Foo (){}
    // function foo() is in the scope of class Foo
    int foo(){ log.message("Class member function\n"); }
};

```


As it was mentioned above, lifetime of a variable is not limited by a current scope. In other words, lifetime of local variables is the same as lifetime of global ones (unless [otherwise](#local_lifetime) specified). For example:

```cpp
int foo() {
    int local_var;
    local_var++;
    log.message("local_var: %d\n",local_var);
}

foo(); // local_var: 1
foo(); // local_var: 2

```

  In this case, lifetime of the variable *local_var* is not limited by the scope of *foo()*. So, when you call *foo()* for the 2nd time, the value that we've got after the previous call is incremented. In terms of C++, it is similar to variables declared with the *static* modifier.
If you want to emulate local lifetime of the *local_var* variable, it should be initialized as follows:

```cpp
int foo() {
    int local_var = 0;
    local_var++;
    log.message("local_var: %d\n",local_var);
}

foo(); // local_var: 1
foo(); // local_var: 1

```


### Scope Resolution Operator


The scope resolution operator **::** is used to specify the context to which an identifier refers. It can be used to access a variable outside a namespace, to access a function outside a class or to resolve the scope of an identifier which is used to represent at the same time, for example, a global variable and a class member.


By prefixing a name of a function (variable, class, namespace and so on) with **::**, you specify that the function from the global scope must be used. This ensures that scope resolution will start from the global scope instead of the current one. For example:

```cpp
namespace Test {
    int a;
    void info() { log.message("a from the scope of the 1st namespace is %d\n",a); }
}

int init () {

    namespace Test {
        int a;
        void info() { log.message("a from the scope of the 2nd namespace is %d\n",a); }
    }
	// access to the members of the global namespace
    ::Test::a = 10;
    ::Test::info();

	// access to the members of the namespace declared in the current scope
    Test::a = 30;
    Test::info();

    return 1;
}

```

 The output is the following:
```text
a from the scope of the 1st namespace is 10
a from the scope of the 2nd namespace is 30

```


> **Notice:** Functions of the UnigineScript library have the global scope. So, the **::** operator ensures that scope resolution for the function of the UnigineScript library will start from the global scope if its name is reused to define a user function inside another scope.


Supposing, there is a user-defined class with a function that has the same name as a function of the UnigineScript library. To call the original UnigineScript function inside the scope where the user function is defined, add the **::** operator as the prefix to its name. For example:

```cpp
class Foo {
    Foo() {}

    // user-defined function in the scope of the Foo class
    void rotate(float angle) {
        // UnigineScript function used to get a matrix of rotation at the given angle around the axis
        mat4 rot = ::rotate(vec3(1.0f, 0.0f, 0.0f), angle);
    }
};

```

 If the **::** operator is not specified, the interpreter will show the following in the console:
```text
NameSpace::getFunctionID(): can't find "rotate" function with 2 arguments
```


## Namespaces


**Namespaces** allow to group entities like classes, objects and functions under a name. This way the global scope can be divided in "sub-scopes", each one with its own name.


The format of namespaces is:


```cpp
namespace identifier {
	// entities
}

```


The example of namespace defining:


```cpp
namespace Foo {
	int a = 10;
}
int a = 5;
log.message("Foo::a is %d, a is %d", Foo::a,a);

// Output: Foo::a is 10, a is 5

```


It is also possible to use ***using*** keyword to introduce a name from a namespace into the current declarative region.


```cpp
namespace Foo::Bar {
	int a = 10;
}

void foo() {
	using Foo::Bar;
	log.message("Foo::Bar::a is %d\n",a);
}
foo();

// Output: Foo::Bar::a is 10

```
