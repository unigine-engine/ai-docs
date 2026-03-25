# Unigine::ExternClass Template (CPP)

**Header:** #include <UnigineInterface.h>


Unigine ExternClass.


## ExternClass Class

### Members

---

## SaveFuncType Definition

### Description

Full declaration:
 *typedef void(* Unigine::ExternClass< Class >::SaveFunc)(const StreamPtr &stream, Class *object)*

Functor for saving the object state.
### Arguments

*stream* -  Write stream for object serialization. *object* -  Pointer to the class object.
### Return value

 void(*
## RestoreFuncType Definition

### Description

Full declaration:
 *typedef Class*(* Unigine::ExternClass< Class >::RestoreFunc)(const StreamPtr &stream)*

Functor for restoring the object state.
### Arguments

*stream* -  Read stream for object serialization.
### Return value

 Class *(* Pointer to the class object.
## DestructorFuncType Definition

### Description

Full declaration:
 *typedef void(* Unigine::ExternClass< Class >::DestructorFunc)(Class *object)*

Functor for deleting the object.
### Arguments

*object* -  Pointer to the class object.
### Return value

 void(*
---

## ExternClass ( SaveFunc save_state , RestoreFunc restore_state , SaveFunc save_pointer , RestoreFunc restore_pointer , DestructorFunc destructor )

Default constructor.
### Arguments

- *SaveFunc* **save_state** - Functor for saving the constructed object state.
- *RestoreFunc* **restore_state** - Functor for restoring the constructed object state.
- *SaveFunc* **save_pointer** - Functor for saving the external constructed object state.
- *RestoreFunc* **restore_pointer** - Functor for restoring the external constructed object state.
- *DestructorFunc* **destructor** - Functor for deleting the constructed object.

## void setDestructor ( DestructorFunc destructor )

Set functor for deleting constructed objects.
### Arguments

- *DestructorFunc* **destructor** - Functor for deleting the constructed object.

## void setSaveRestorePointer ( SaveFunc save , RestoreFunc restore )

Set functors for saving/restoring pointers.
### Arguments

- *SaveFunc* **save** - Functor for saving the external constructed object state.
- *RestoreFunc* **restore** - Functor for restoring the external constructed object state.

## void setSaveRestoreState ( SaveFunc save , RestoreFunc restore )

Set functors for saving/restoring state.
### Arguments

- *SaveFunc* **save** - Functor for saving the constructed object state.
- *RestoreFunc* **restore** - Functor for restoring the constructed object state.

## void addBaseClass ( ExternClassBase * base )

Adds a base class to an external class.
### Arguments

- *ExternClassBase ** **base** - Pointer to the base class.

## void addConstructor ( const char * args )

Adds a constructor to an external class. The constructor can receive up to 9 arguments.
### Arguments

- *const char ** **args** - Default arguments.

## void addConstructor ( Class *(*)() func , const char * args )

Adds a constructor to an external class. The constructor can receive up to 9 arguments.
### Arguments

- *Class *(*)()* **func** - Functor for creating the object.
- *const char ** **args** - Default arguments.

## void addFunction ( const char * name , Ret (Type::*)() __attribute__((thiscall)) func , const char * args )

Adds a member function to an external class. The function can receive up to 9 arguments and return void or value of any supported type. Constant member functions are also supported.
### Arguments

- *const char ** **name** - Name of the member function.
- *Ret (Type::*)() __attribute__((thiscall))* **func** - Pointer to the member function.
- *const char ** **args** - Default arguments.

## void addGetFunction ( const char * name , Type Class::* member )

Adds a getter function to an external class member.
### Arguments

- *const char ** **name** - Name of the getter function.
- *Type Class::** **member** - Class member.

## void addSetFunction ( const char * name , Type Class::* member )

Adds a setter function to an external class member.
### Arguments

- *const char ** **name** - Name of the setter function.
- *Type Class::** **member** - Class member.
