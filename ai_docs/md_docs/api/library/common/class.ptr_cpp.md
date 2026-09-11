# Unigine::Ptr Class (CPP)

**Header:** #include <UniginePtr.h>


***Ptr<Type>*** is a smart pointer template that is used to manage the lifetime of objects.


Not all methods of the Engine's internal C++ classes are exposed to the user, some are used internally by the Engine only. To provide safe access, an interface is used, which stores a pointer to the internal object.


To create an instance of an internal class, declare a smart pointer and call the *create()* method with any necessary construction parameters:


```cpp
// Instantiating an object of an internal class
<Class>Ptr instance = <Class>::create(<construction_parameters>);
// Access object methods through smart pointer
instance->someMethod();

```


### Ownership and Non-Ownership Objects


Objects managed by ***Ptr<Type>*** can be classified as ownership or non-ownership objects:


- **[Ownership Objects](../../../code/fundamentals/smartpointers.md#ownership_object)** These objects are fully managed by ***Ptr<Type>***. The reference count increases or decreases automatically when smart pointers are copied, moved, or destroyed. When the last ***Ptr*** referencing the object is destroyed, the object itself is **deleted automatically**. ```cpp // Creating a new image ImagePtr img = Image::create(); // Now two pointers point to our image (reference counter increment) ImagePtr img2 = img; // Removing the image (as both pointers no longer point to it and reference counter is zero) img2 = img = nullptr; ```
- **[Non-Ownership Objects](../../../code/fundamentals/smartpointers.md#non_ownership_object)** These objects **are not automatically deleted** by smart pointers. To safely delete them, the following methods are provided:

  - *[deleteLater()](#deleteLater_void)* - delayed deletion, the object will be deleted during the next *[swap()](../../../code/fundamentals/execution_sequence/main_loop.md)* stage of the execution sequence; ```cpp // deleteLater() behavior node.deleteLater(); // right after calling deleteLater() if (node.isDeleted())	//true Log::message("node is deleted"); if (node.isNull())		//false Log::message("node is null"); if (node.isValid())		//true Log::message("node is valid"); if (node.get())			//true Log::message("Got the pointer to the object!"); // ... after swap() ... if (node.isDeleted())	//true Log::message("node is deleted"); if (node.isNull())		//true Log::message("node is null"); if (node.isValid())		//false Log::message("node is valid"); if (node.get())			//false Log::message("Got the pointer to the object!"); ```
  - *[deleteForce()](#deleteForce_void)* - immediate deletion. ```cpp // deleteForce() behavior node.deleteForce(); // node is deleted immediately if (node.isDeleted())	//true Log::message("node is deleted"); if (node.isNull())		//true Log::message("node is null"); if (node.isValid())		//false Log::message("node is valid"); if (node.get())			//false Log::message("Got the pointer to the object!"); ```


### See Also


- **[Working with Smart Pointers](../../../code/fundamentals/smartpointers.md)** - an article explaining C++ smart pointer system in UNIGINE.


## Ptr Class

### Members

---

## Ptr ( )

Default constructor that produces a nullptr pointer.
## Ptr ( UnigineBaseObject * obj , bool take_ownership )

Constructor. Creates a smart pointer from a raw **UnigineBaseObject***. Optionally takes ownership of the object, and increments the reference count.
### Arguments

- *UnigineBaseObject ** **obj** - Raw pointer to a **UnigineBaseObject**.
- *bool* **take_ownership** - If true, the pointer owns the object and will release it. If false, the pointer increments the reference count but does not claim ownership.

## Ptr ( const Ptr & pointer )

Constructor. Initializes a new ***Ptr*** instance by copying an existing ***Ptr*** of the same type.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md) &* **pointer** - The smart pointer to copy from.

## Ptr ( Ptr && pointer )

Constructor. Initializes a new ***Ptr*** instance by taking ownership of an existing temporary ***Ptr***. The new instance assumes control of the underlying object, and the source ***Ptr*** is left empty (nullptr).
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md) &&* **pointer** - A smart pointer to transfer ownership from.

## Ptr ( const Ptr <OtherType> & pointer )

Constructor. Creates a new ***Ptr<Type>*** instance by copying another **Ptr<OtherType>** whose underlying type is convertible to Type. The new ***Ptr*** shares ownership of the same object, and the reference count is incremented.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<OtherType> &* **pointer** - A smart pointer of a compatible type to copy from.

## Ptr ( Ptr <OtherType> && pointer )

Constructor. Creates a new ***Ptr<Type>*** instance by taking ownership of another **Ptr<OtherType>** whose type is convertible to Type. The new ***Ptr*** manages the same object, and the source ***Ptr*** is left empty.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<OtherType> &&* **pointer** - A smart pointer of a compatible type to move from.

## explicit Ptr ( Type * pointer )

Constructor. Creates a new ***Ptr<Type>*** from a raw pointer to **Type**.
### Arguments

- *Type ** **pointer** - Pointer of the given type.

## Type * get ( ) const

Returns the internal address (raw pointer) managed by the ***Ptr***.
### Return value

Pointer.
## void clear ( )

Releases the pointer to the managed object and decreases the internal reference counter. If the objects is an *[ownership object](../../../code/fundamentals/smartpointers.md#ownership_object)* and this ***Ptr*** is the last one holding a reference to it, this method will also trigger the actual destruction of the underlying object. For *[non-ownership objects](../../../code/fundamentals/smartpointers.md#non_ownership_object)*, the method only sets the pointer to nullptr, while the object itself continues to be managed by the Engine.
## bool operator bool ( )

Checks if the pointer equals zero.
### Return value

**true** if the pointer is not equal to zero; otherwise, **false**.
## Type * operator-> ( ) const

Provides access to the members of the object managed by the ***Ptr***.
### Return value

A pointer to the managed object.
## Type & operator* ( )

Provides access to the object managed by the ***Ptr***. Dereferences the internal pointer and returns a reference to the underlying object.
### Return value

A reference to the managed object.
## Ptr operator= ( std::nullptr_t nullptr )

Releases ownership of the managed object and sets the ***Ptr*** to empty (nullptr).
### Arguments

- *std::nullptr_t* **nullptr** - Assigns the ***Ptr*** to null.

### Return value

A reference to the current ***Ptr*** object.
## Ptr operator= ( const Ptr & pointer )

Copies ownership from another ***Ptr*** of the same type. The reference count of the shared object is incremented.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md) &* **pointer** - The source smart pointer to copy from.

### Return value

A reference to the current ***Ptr*** object.
## Ptr operator= ( const Ptr && pointer )

Transfers ownership from another ***Ptr*** of the same type. The source ***Ptr*** is left empty.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md) &&* **pointer** - The source smart pointer to move from.

### Return value

A reference to the current ***Ptr*** object.
## Ptr <Type> & operator= ( const Ptr <OtherType> & pointer )

Copies ownership from a ***Ptr*** of a type convertible to ***Type***. Reference count is incremented.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<OtherType> &* **pointer** - Source smart pointer of a compatible type.

### Return value

A reference to the current ***Ptr*** object.
## Ptr <Type> & operator= ( const Ptr <OtherType> && pointer )

Transfers ownership from a ***Ptr*** of a type convertible to ***Type***. The source ***Ptr*** is left empty.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<OtherType> &&* **pointer** - Source smart pointer of a compatible type.

### Return value

A reference to the current ***Ptr*** object.
## Ptr <Type> & operator= ( const OtherType * pointer )

Assigns a raw pointer of a type convertible to ***Type***. The ***Ptr*** takes ownership of the pointer.
### Arguments

- *const OtherType ** **pointer** - Raw pointer to assign.

### Return value

A reference to the current ***Ptr*** object.
## bool isValid ( ) const

Checks whether the ***Ptr*** currently points to a valid, existing object (the pointer value is not nullptr).
### Return value

true if the internal address is not nullptr; otherwise, false.
## bool isNull ( ) const

Checks whether the ***Ptr*** currently stores a nullptr value.
### Return value

true if the value is nullptr; otherwise, false.
## bool isDeleted ( ) const

Checks whether the ***Ptr*** currently refers to a nullptr or scheduled for deletion (e.g. via *[deleteLater()](#deleteLater_void)* or by the Engine).
### Return value

true if the object is deleted; otherwise, false.
## template < typename T >

## T * getInternalObject ( )

Returns an internal object pointed to by the pointer.
## void deleteLater ( )


Performs delayed deletion of the object. The pointed object shall be deleted at the next *[swap()](../../../code/fundamentals/execution_sequence/main_loop.md)* stage of the execution sequence.


> **Notice:** This method can be called **only for [non-ownership objects](../../../code/fundamentals/smartpointers.md#non_ownership_object).**


```cpp
NodePtr node = NodeDummy::create();

// Checking whether the node exists
if (node)
	Log::message("The node is alive!\n");

// Deleting the node
node.deleteLater();

```


## void deleteForce ( )


Performs forced deletion of the object. The pointed object shall be deleted immediately. Calling this method for main-loop-dependent objects (e.g., nodes) is **safe only when performed from the main thread**.


> **Notice:** This method can be called **only for [non-ownership objects](../../../code/fundamentals/smartpointers.md#non_ownership_object).**


```cpp
NodePtr node = NodeDummy::create();

// Checking whether the node exists
if (node)
	Log::message("The node is alive!\n");

// Deleting the node
node.deleteForce();

```
