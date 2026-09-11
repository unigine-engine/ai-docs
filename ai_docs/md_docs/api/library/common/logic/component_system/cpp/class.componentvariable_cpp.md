# ComponentVariable Class (CPP)

**Header:** #include <UnigineComponentSystem.h>


This class is used to address the [component parameters](../../../../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md#parameters).


## ComponentVariable Class

---

## const PropertyParameter Ptr & getParameter ( ) const

Returns the pointer to the corresponding property parameter.
### Return value

Pointer to the property parameter.
## int size ( )

Returns the number of elements in the array.
> **Notice:** This method is for the array and array structure component parameters.


### Return value

Number of elements in the array.
## C & operator[] ( int index )

Returns the reference to the requested element.
> **Notice:** This method is for the array and array structure component parameters.


### Arguments

- *int* **index** - Position of the element to return.

### Return value

Reference to the requested element.
