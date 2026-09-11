# Interface Class

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


An interface is used to describe a behaviour, which is followed by all of the classes deriving from the interface. An interface class does not implement any functionality. It means that such a class contains only functions declaration. Interface class functions must be implemented by derived classes.


The interface is used to provide a polymorphism. It means that several classes can implement the same interface functions in different ways.


## Interface Class


The interface class is declared as any other class in UnigineScript. In the example, the [abstract virtual function declaration](#abstract_declaration) is used.


```cpp
class Interface {
	// functions declaration
	void update() = 0;
	//...;
}

```


Note that the word *Interface* is not reserved. Any class that is inherited from the *Interface* class must contain an implementation for its functions. For example:


```cpp
class Bar : Interface {
	// implementation of the interface function for Bar
	void update() {
		log.message("Bar::update(): called\n");
	}
};
class Baz : Interface {
	// implementation of the interface function for Baz
	void update() {
		log.message("Baz::update(): called\n");
	}
};

```


### Example


Let's suppose that there is an interface class, which describes an object:


```cpp
class Interface {
	void update() = 0;
}

```


It means that each object must be updated. *Bar* and *Baz* classes decribe two different objects. This classes are inherited from the *Interface* class, and also the *Bar* class is derived from the Foo class.


```cpp
class Foo {
	void foo() = 0;
};
class Bar : Foo, Interface {
	void update() {
		log.message("Bar::update(): called\n");
	}
};
class Baz : Interface {
	void update() {
		log.message("Baz::update(): called\n");
	}
};

```


The interface is used to iterate objects of different types that implement that interface. So, you can create an array of the objects and update them all.


The example displays the following:


```text
Bar::update(): called
Baz::update(): called

```


### Abstract virtual function declaration


A virtual function is a function, which can be overridden in a derived class.


> **Notice:** When a user class is inherited from another class, both automatically support virtual methods.


You can declare the virtual function the following way (C++ style):


```cpp
class Foo {
	void foo() = 0;
};

```


In this case, the function has no any implementation, but the derived class must implement it.


> **Notice:** Also you can declare the virtual function by using the virtual keyword, but it's optional.
