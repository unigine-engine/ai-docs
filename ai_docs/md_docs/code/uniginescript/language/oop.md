# Object Oriented Programming

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


UnigineScript lets the user define new types using user classes.


## Classes


A **class** is an expanded concept of a data structure: instead of holding only data, it can hold both data and functions.


An object is an instantiation of a class. In terms of variables, a class would be the type, and an object would be the variable.


Classes are generally declared using the keyword class, with the following format:


```cpp
class class_name {
	access_specifier_1:
	member1;
	access_specifier_2:
	member2;
	// ...
} object_names;

// class_name - valid identifier for the class
// object_names - an optional list of names for objects of this class
```


The body of the declaration can contain members, that can be either data or function declarations, and optionally access specifiers.

> **Notice:** There is no protected access level modifier, there are only public and private ones. All class members are public by default.


### UnigineScript Class Types


There are 3 types of classes applicable in UnigineScript:

1. [Engine Classes](../../../api/index.md)
2. User-Defined Classes
3. External Classes (exported from the C++ by a script)


#### Engine Classes


You can see the list of available **Engine Classes** [here](../../../api/index.md).


#### User-Defined Classes


**User-Defined Classes** are classes defined by user. [Inheritance](#inheritance_user) is supported.


```cpp
/* user-defined class
 */
class Foo {
	// member variables
	int a;
	int b;
	// constructor
	Foo(int a,int b) {
		this.a = a;
		this.b = b;
	}
	// destructor
	~Foo() {}
	// member function (method)
	void print() {
		log.message("a is %d, b is %d\n",a,b);
	}
};

// create a new instance of the Foo class
Foo foo = new Foo(10,20);
// call a method of that instance
foo.print(); // Output: a is 10, b is 20
// force object destruction
delete foo;

```


Note that you always manipulate with references to objects but not with the objects themselves. That is why when you assign one object to another, it means that you simply copy the reference. Once the object is destroyed, its references aren't functional anymore.

```cpp
Foo f0 = new Foo();
Foo f1 = f0;
f1.print();
delete f0;
f1.print(); // run-time error: the object is null

```


Methods are set up at the compile-time, therefore:

```cpp
Foo foo = new Foo();
foo.print(); // ok
foo = 10;
foo.print(); // run-time error
int i = new Foo();
i.print(); // compile-time error

```


#### External Classes


**External classes** are classes exported from C++. You can read how to export a class from C++ [here](../../../code/cpp/usage/script/classes.md#export_classes).


### Access Specifiers


**Access pecifiers** modify the access rights that the members following them acquire. UnigineScript provides two different specifiers for accessing class members:

- **public** means that a member can be accessed from the outside of the class instance.
- **private** means that such member is accessible from within other members of the same class and members of the inherited classes.


> **Notice:** All class members are **public** by default.


```cpp
class Foo {
	int public_i;
	void public_foo() { log.message("Public (no access specifier)\n"); }
	private:
		int private_i;
        void private_foo() { log.message("Private\n"); }
	public:
        int public_j;
        void public_bar() { log.message("Public\n"); }
};

```


For example, in case if a class is inherited from *Foo*:

```cpp
class Bazz : Foo {
	void foo() {
		Foo::public_foo();
		Foo::private_foo();
	}
};

Bazz b = new Bazz();
b.foo();

```

 The result will be:
```text
Public (no access specifier)
Private

```


## Constructors and Destructors


### Constructors and new


For a class to be used, it should be instantiated. This is done using constructors. A constructor creates an instance of a class and returns it. Here is how a constructor can be defined:

```cpp
class Foo {
	// member variable
	int a;
	// constructor
	Foo(int a) {
		// do something here
	}
// other functions

};

```

 The constructor is a method that:
- Has the same name as the class to which it belongs.
- Does not have a return type specifier in its declaration and does not use the [*return*](../../../code/uniginescript/language/control_statements/jump_statements/return.md) or [*yield*](../../../code/uniginescript/language/control_statements/other_statements/yield.md) statement.


If the constructor is defined outside the class declaration, it should be done like this:

```cpp
class Foo {
	// constructor declaration
	Foo();
	// other stuff
	...
};

// constructor definition
void Foo::__Foo__() {
	// do something here
}

```


To invoke a constructor, use the *new* operator as follows:

```cpp
Foo fooInstance = new Foo(5);
```


Also the *new* operator can receive a string:

```cpp
Foo fooInstance = new("Foo",5);
```


### Destructors and delete


If a class instance is no longer needed and it's time for it to pass away, it should be properly freed. That is why a destructor is called before the occupied memory is marked as free. Here is how a destructor can be defined:

```cpp
class Foo {
	// member variable
	int a;
	// destructor
	~Foo() {
		// do something here
	}
	// other functions
	...
};

```

 The destructor is a method, which:
- Has the same name as the class to which it belongs.
- Has a prefix **~** before its name.
- Does not have a return type specifier in its declaration and does not use the [*return*](../../../code/uniginescript/language/control_statements/jump_statements/return.md) or [*yield*](../../../code/uniginescript/language/control_statements/other_statements/yield.md) statement.


If the destructor is defined outside the class declaration, it should be done like this:

```cpp
class Foo {
	// destructor declaration
	~Foo();
	// other stuff
	...
};

// destructor definition
void Foo::__~Foo__() {
// do something here
...
}

```


To invoke a destructor explicitly, you need to write something like this:

```cpp
delete fooInstance;
```


## Overloading


**Overloading** allows functions and operators to have the same name but with different parameters.


### Function Overloading


UnigineScript allows **Function Overloading**.

```cpp
int foo(int a,int b) {
	return a * b;
}

int foo(int a,int b,int c) {
	return a + b + c;
}

log.message("%d\n",foo(2,3)); // the result is: 2*3=6
log.message("%d\n",foo(2,3,4)); // the result is: 2+3+4=9

```


### Operator Overloading


**Operator overloading** allows operators to have different implementations depending on their arguments. You can provide your own operator to a class by overloading the built-in operator to perform some specific computation when the operator is used on objects of that class.


The name of an overloaded operator is *operator* **x**, where **x** is the operator, available for overloading in UnigineScript:


- *operator+*
- *operator-*
- *operator**
- *operator/*
- *operator%*
- *operator<*
- *operator>*
- *operator==*
- *operator<=*
- *operator>=*
- *operator!=*
- *__set__* (for [])
- *__get__* (for [])


The following example represents overloading of the *operator+, operator-* and *operator** for the class *Vec3*:

```cpp
class Vec3 {

	float x,y,z;

	Vec3(float x,float y,float z) {
		this.x = x; this.y = y; this.z = z;
	}

	Vec3 operator+(Vec3 v0,Vec3 v1) {
		return new Vec3(v0.x + v1.x,v0.y + v1.y,v0.z + v1.z);
	}

	Vec3 operator-(Vec3 v0,Vec3 v1) {
		return new Vec3(v0.x - v1.x,v0.y - v1.y,v0.z - v1.z);
	}

	Vec3 operator*(Vec3 v,float f) {
		return new Vec3(v.x * f,v.y * f,v.z * f);
	}
};

Vec3 v0 = new Vec3(1,2,3);
Vec3 v1 = new Vec3(4,5,6);

Vec3 res = (v0 + v1) * 13.13 + (v1 - v0) * 31.31 + v0 * 0.5;
log.message("%f %f %f\n",res.x,res.y,res.z);

// the result is: 160.080002 186.839996 213.600006

```

 The example of *operator<* overloading:
```cpp
class Class {
	string name;
	Class(string name) {
		this.name = name;
	}
	int operator<(Class c0,Class c1) {
		return (c0.name < c1.name);
	}
};

Class classes[0];
forloop(int i = 0; 8) {
	classes.append(new Class(string(rand(0,100))));
}

classes.sort();
foreach(Class c; classes) {
	log.message("%s ",c.name);
}
log.message("\n");

// the result is: 15 35 77 83 86 86 92 93

```

 Overload *operator[]* in user-defined class:
```cpp
class Foo {
    mat4 m;
    void __set__(Foo f,int index,int value) {
        f.m[index] = value;
    }
    int __get__(Foo f,int index) {
        return f.m[index];
    }
};

Foo f = new Foo();
f[0] = 10;
f[1] = f[0];
log.message("%g %g\n",f[0],f[1]);

// the result is: 10 10

```


## Keywords


### this Keyword


Sometimes it is important to reference the object, for which a method is invoked. In such a situation, *this* keyword is helpful; it is reference to an object itself, available for member functions of the class.


```cpp
class Foo {
	int a;
	int b;
	// usage in a constructor
	Foo(int a,int b) {
		this.a = a;
		this.b = b;
	}
	// usage in a method
	void print() {
		log.message("a is %d, b is %d, object is %s\n",a,b,typeinfo(this));
	}
};

Foo foo = new Foo(10,20);
foo.print();

```


```text
a is 10, b is 20, object is Foo (0:0)
```

 Here 0:0 means "class ID is 0, object ID is 0"
### super Keyword


Base class functions can be overridden in the derived class. However, you can call such functions from the derived class by using the *super* keyword.  For example, the foo() function is overridden in the Bar class, so, the foo() function of the Foo class can be called using *super*.


```cpp
class Foo {
  void foo() { log.message("base\n"); }
};
class Bar : Foo{
  void foo() { log.message("derived\n"); }
  void bar() {
    super.foo();   // prints "base"
    this.foo();    // prints "derived"
  }
};
Bar bar = new Bar();
bar.bar();

```


The result will be:


```text
base
derived

```


## Inheritance


In UnigineScript, derived classes can inherit all public methods and data members from one or multiple base classes.


There is a peculiarity of the class inheritance in UnigineScript:

- When a user class is inherited from another class, both automatically support virtual methods. > **Notice:** You can declare the virtual function by using the *virtual* keyword, but it's optional.


```cpp
class Foo {
	int f = -13;
	int array[2] = ( 0, 1 );

	Foo(int i) { f = i; }
	void foo() { log.message("Foo::foo %d: %d %d\n",f,array[0],array[1]); }
};

class Bar : Foo {
	// f is initialized in the base class
	int b = 2;
	int array[2] = ( 2, 3 );

	Bar(int i) { b = i; }
	void bar() { log.message("Bar::bar %d %d: %d %d\n",f,b,array[0],array[1]); }
	void foo() { log.message("Bar::foo %d %d: %d %d\n",f,b,array[0],array[1]); }
};

class Bazz : Bar {
	// f is initialized in the base class
	int b = -23;
	int array[2] = ( 4, 5 );

	Bazz(int i) { b = i; }
	void foo() { log.message("Bazz::foo %d %d: %d %d\n",f,b,array[0],array[1]); }
};

Foo f = new Foo(13);
Bar b = new Bar(133);
Bazz bz = new Bazz(1333);

void foo(Foo f) {
	f.foo();
	f.call("foo");
}

foo(f);
foo(b);
foo(bz);

```


The result will be:

```text
Foo::foo 13: 0 1
Foo::foo 13: 0 1
Bar::foo -13 133: 2 3
Bar::foo -13 133: 2 3
Bazz::foo -13 1333: 4 5
Bazz::foo -13 1333: 4 5

```


### Calling the Base Class Constructor


It is also possible to call the base class constructor in the inherited class.

```cpp
class Foo {
        Foo(int a,int b) { log.message("Foo::Foo(): %d %d\n",a,b); }
};

class Bar : Foo {
        Bar(int a,int b) : Foo(a + 3,b + 5) { }
};

Bar b = new Bar(1,2);
delete b;

```


And the result will be:

```text
Foo::Foo(): 4 7
```


### Accessing the Overridden Base Class Function


If in the inherited class a method is overridden, you can still access this member function as it is implemented in the base class using the following syntax:
 `<base class name>::<overridden function name>`

```cpp
class Foo {
	void foo(int a) {
		log.message("Foo::foo(): %d\n",a);
	}
};

class Bar : Foo {
	void foo(int a) {
		// Overridden method implementation
		log.message("Bar::foo(): %d\n",a + 3);
		// Accessing the base class method implementation
		Foo::foo(a);
   }
};

Bar b = new Bar();
b.foo(2);
delete b;

```


And the result will be:

```text
Bar::foo(): 5
Foo::foo(): 2

```


### Creating Abstract Methods in a Base Class


You can create an abstract method in the base class and implement it in the derived one. However, in the base class method an error or, if necessary, an exception should be thrown. It is used to indicate that a method implementation is lacking in the derived class.


```cpp
class Foo {
	void foo(int a) {
		log.error("Foo::foo(): pure virtual function call\n");
	}
};

class Bar : Foo {
	void foo(int a) {
		int num = a + 5;
		log.message("Bar::foo(): %d\n",num);
   }
};

Bar b = new Bar();
b.foo(2);
delete b;

```


And the result will be:


```text
Bar::foo(): 7
```


### Casting


An object of a parent polymorphic class can be cast to a child one, so as to access all its member functions.

```cpp
class Foo {
    void foo() { }
};
int foo = new Foo();
Foo(foo).foo();  // changes a variable type
foo.foo();       // this is invalid

```


### Class Based Branching


The fast class based branching can be implemented by using the *[switch-case](../../../code/uniginescript/language/control_statements/selection_statements/switch_case.md)* conditional statement.


If you have several classes defined in the script and their instances require to be processed differently, you can use the *classid()* function as a constant for the *case* within the *switch* to check if the passed value is an instance of the particular class.

```cpp
class Foo { };
class Bar { };
void foo(int a) {
  switch(classid(a)) {
    case classid(Foo): log.message("Foo\n"); break;
    case classid(Bar): log.message("Bar\n"); break;
    case classid(File): log.message("File\n"); break;
  }
}
foo(new Foo());
foo(new Bar());
foo(new File());

```


```text
Foo
Bar
File

```

 To check that the *classid()* function returns the same ID for class and its instance, perform the following:
```cpp
log.message("%d %d\n",classid(new Foo()),classid(Foo));
log.message("%d %d\n",classid(new Bar()),classid(Bar));
log.message("%d %d\n",classid(new File()),classid(File));

```

 The example produces the following output:
```text
0 0
65536 65536
-6 -6

```


## Inheritance from C++ Classes


User classes can not only be inherited from other user classes, but also from C++ classes:

- Engine base classes (any classes from the core and UnigineScript libraries)
- Extern C++ classes accessed via C++ API


In both of these cases, class inheritance is performed in the same way (see an example below).


### Inheritance from Engine Classes


Here is an example how to create `MyObjectMesh` class which inherits from the base engine [`ObjectMeshStatic`](../../../api/library/objects/class.objectmeshstatic_cpp.md) class.

- Objects of the derived class can call methods of base class directly.
- When passing object of the derived class to function that takes an object of the base class, inherited class cannot be automatically converted to the base class. Upcasting should be done explicitly via accessing `extern` member of the derived class.
- To downcast the instance of base class to your custom derived class, use `cast()` function. This function is created automatically for all inherited classes and needs not to be implemented manually.


```cpp
// Custom class inherited from base engine class.
class MyObjectMesh : ObjectMesh {
	int number;

	// Constructor.
	MyObjectMesh(string name, int a) : ObjectMesh(name) {
		number = a;
		log.message("MyObjectMesh object constructed\n");
	}
};

void foo(MyObjectMesh mesh) {
	// Check if the argument is an instance of MyObjectMesh.
	if(is_base_class("MyObjectMesh",mesh) == 0) log.message("Object is not MyObjectMesh\n");
	else log.message("Object is MyObjectMesh\nNumber = %d\n", mesh.number);

	return;
};

/*
*/
MyObjectMesh mesh = new MyObjectMesh("samples/common/meshes/box.mesh",42);

// You can call functions of base class.
log.message("Mesh name: %s\n",mesh.getMeshName());

// To upcast the object to the base class, use "extern".
// It's necessary when passing MyObjectMesh to a function that takes a base ObjectMesh or Node.
engine.world.isNode(mesh.extern));

// To downcast the object back to its derived class, use cast() function.
foo(MyObjectMesh::cast(mesh.extern));

```


The result will be:

```text
MyObjectMesh object constructed
Mesh name: samples/common/meshes/box.mesh
Object is MyObjectMesh
Number = 42

```


### Using Callbacks in Inherited Classes


To use callbacks in the inherited class, you need to pass a reference to this class ( `this`) as an additional argument for the callback function.


For example, a callback in the class inherited from [WidgetButton](../../../api/library/gui/class.widgetbutton_cpp.md):

```cpp
class MyButton : WidgetButton {
  private:

    void on_click(MyButton button) {
      log.message("on_click: %s\n",typeinfo(button));
    }

  public:

    MyButton(Gui gui) {
      extern = new WidgetButton(gui);
      extern.setCallback(GUI_CLICKED,"::MyButton::on_click",this);
    }
};

```


Here is another example with a class inherited from [WorldTrigger](../../../api/library/worlds/class.worldtrigger_cpp.md):

```cpp
class MyTrigger : WorldTrigger {
  private:

    void on_enter(Node node,MyTrigger trigger) {
      log.message("on_enter: %s %s\n",typeinfo(node),typeinfo(trigger));
    }

    void on_leave(Node node,MyTrigger trigger) {
      log.message("on_leave: %s %s\n",typeinfo(node),typeinfo(trigger));
    }

  public:

    MyTrigger(vec3 size) {
      extern = new WorldTrigger(size);
      extern.setEnterCallback("::MyTrigger::on_enter",this);
      extern.setLeaveCallback("::MyTrigger::on_leave",this);
    }
};

```


## Function Chaining


In UnigineScript, *function chaining* enables to call a chain of functions in one statement. The return value of the first function is used to call the second function.  Such approach is useful when there is no need to store intermediate objects. For example:

```cpp
mesh.getBoundBox().getMin();
```

 First the *mesh.getBoundBox()* is executed and an instance of the *BoundBox* class is returned. On this returned value the *getMin()* member function is called.
> **Notice:** The type of the return variable is equal to the return type of the last executed function.


Function chaining can also be used when calling functions of user-defined classes. For example:

```cpp
// the 1st user defined class
class Foo {
    void print() { log.message(__FUNC__ + ": called\n"); }
};

// the 2nd user defined class
class Bar {
    Foo get_foo() { return new Foo(); }
};

int init() {
    // create an instance of the 2nd class
    Bar b = new Bar();
    // chain the function calls: call the get_foo() member function for the instance of the Bar class
	// and then call the member function of the Foo class
	b.get_foo().print();
}
// Output: Foo::print(): called

```
