# Unigine::TypeInfo Class (CPP)

**Header:** #include <UnigineType.h>


TypeInfo RTTI class.


## TypeInfo Class

### Members

---

## TypeInfo ( )

Default constructor that produces an empty class.
## TypeInfo ( int id , const char * name )

Constructor.
### Arguments

- *int* **id** - type identifier.
- *const char ** **name** - type name.

## TypeInfo ( const TypeInfo & type )

Copy constructor.
### Arguments

- *const [TypeInfo](../../../api/library/common/class.typeinfo_cpp.md) &* **type** - TypeInfo class.

## int getID ( ) const

Access to the type identifier.
### Return value

Type identifier.
## const char * getName ( ) const

Access to the type name.
### Return value

Type name.
## explicit TypeInfo ( Type type )

Constructor.
### Arguments

- *Type* **type** - TypeID class.
