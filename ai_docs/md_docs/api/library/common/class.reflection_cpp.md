# Unigine::Reflection Class (CPP)

**Header:** #include <UnigineInterpreter.h>


This class is used to create reflections for user or extern classes and namespaces. It allows you to get names and custom attribute strings for all variables, arrays, user classes and namespaces within it. Such attributes can be used for smart automatic code generation for GUI or any game logic. For example, it is possible to get attributes, parse them in the required way, and feed them to the [Expression](../../../api/library/common/class.expression_cpp.md) which will compile the resulting code.


## Reflection Class

### Members

---

## Reflection ( void * interpreter , const Variable & v )

### Arguments

- *void ** **interpreter**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v**

## int getNumFunctionDefaultArgs ( int num )

### Arguments

- *int* **num**

## Variable callExternClassFunction ( Variable object , const char * function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 , const Variable & arg5 , const Variable & arg6 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg5**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg6**

## Variable callExternClassFunction ( Variable object , const char * function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 , const Variable & arg5 , const Variable & arg6 , const Variable & arg7 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg5**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg6**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg7**

## Variable callExternClassFunction ( Variable object , const char * function , int num_args , const Variable * args )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *const char ** **function**
- *int* **num_args**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) ** **args**

## Variable callExternClassFunction ( Variable object , int function )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *int* **function**

## Variable callExternClassFunction ( Variable object , int function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**

## Variable callExternClassFunction ( Variable object , const char * function , const Variable & arg0 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**

## Variable callExternClassFunction ( Variable object , int function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 , const Variable & arg5 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg5**

## Variable callExternClassFunction ( Variable object , int function , int num_args , const Vector < Variable > & args )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *int* **function**
- *int* **num_args**
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Variable](../../../api/library/common/class.variable_cpp.md)> &* **args**

## Variable callExternClassFunction ( Variable object , const char * function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**

## Variable callExternClassFunction ( Variable object , const char * function )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *const char ** **function**

## Variable callExternClassFunction ( Variable object , const char * function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**

## Variable callExternClassFunction ( Variable object , int function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 , const Variable & arg5 , const Variable & arg6 , const Variable & arg7 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg5**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg6**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg7**

## Variable callExternClassFunction ( Variable object , int function , const Variable & arg0 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**

## Variable callExternClassFunction ( Variable object , const char * function , const Variable & arg0 , const Variable & arg1 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**

## Variable callExternClassFunction ( Variable object , int function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**

## Variable callExternClassFunction ( Variable object , const char * function , int num_args , const Vector < Variable > & args )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *const char ** **function**
- *int* **num_args**
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Variable](../../../api/library/common/class.variable_cpp.md)> &* **args**

## Variable callExternClassFunction ( Variable object , const char * function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 , const Variable & arg5 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg5**

## Variable callExternClassFunction ( Variable object , int function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 , const Variable & arg5 , const Variable & arg6 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg5**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg6**

## Variable callExternClassFunction ( Variable object , const char * function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**

## Variable callExternClassFunction ( Variable object , const char * function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 , const Variable & arg5 , const Variable & arg6 , const Variable & arg7 , const Variable & arg8 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg5**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg6**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg7**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg8**

## Variable callExternClassFunction ( Variable object , int function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**

## Variable callExternClassFunction ( Variable object , int function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 , const Variable & arg5 , const Variable & arg6 , const Variable & arg7 , const Variable & arg8 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg5**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg6**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg7**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg8**

## Variable callExternClassFunction ( Variable object , int function , int num_args , const Variable * args )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *int* **function**
- *int* **num_args**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) ** **args**

## Variable callExternClassFunction ( Variable object , int function , const Variable & arg0 , const Variable & arg1 )

### Arguments

- *[Variable](../../../api/library/common/class.variable_cpp.md)* **object**
- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**

## Variable callExternFunction ( const char * function , const Variable & arg0 , const Variable & arg1 )

### Arguments

- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**

## Variable callExternFunction ( const char * function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 , const Variable & arg5 , const Variable & arg6 )

### Arguments

- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg5**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg6**

## Variable callExternFunction ( int function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 , const Variable & arg5 , const Variable & arg6 , const Variable & arg7 )

### Arguments

- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg5**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg6**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg7**

## Variable callExternFunction ( const char * function , int num_args , const Vector < Variable > & args )

### Arguments

- *const char ** **function**
- *int* **num_args**
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Variable](../../../api/library/common/class.variable_cpp.md)> &* **args**

## Variable callExternFunction ( int function , int num_args , const Variable * args )

### Arguments

- *int* **function**
- *int* **num_args**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) ** **args**

## Variable callExternFunction ( const char * function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 )

### Arguments

- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**

## Variable callExternFunction ( const char * function )

### Arguments

- *const char ** **function**

## Variable callExternFunction ( int function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 , const Variable & arg5 )

### Arguments

- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg5**

## Variable callExternFunction ( const char * function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 , const Variable & arg5 , const Variable & arg6 , const Variable & arg7 , const Variable & arg8 )

### Arguments

- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg5**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg6**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg7**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg8**

## Variable callExternFunction ( const char * function , const Variable & arg0 )

### Arguments

- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**

## Variable callExternFunction ( const char * function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 )

### Arguments

- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**

## Variable callExternFunction ( const char * function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 )

### Arguments

- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**

## Variable callExternFunction ( int function , const Variable & arg0 )

### Arguments

- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**

## Variable callExternFunction ( int function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 , const Variable & arg5 , const Variable & arg6 , const Variable & arg7 , const Variable & arg8 )

### Arguments

- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg5**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg6**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg7**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg8**

## Variable callExternFunction ( int function , int num_args , const Vector < Variable > & args )

### Arguments

- *int* **function**
- *int* **num_args**
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Variable](../../../api/library/common/class.variable_cpp.md)> &* **args**

## Variable callExternFunction ( int function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 )

### Arguments

- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**

## Variable callExternFunction ( const char * function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 , const Variable & arg5 )

### Arguments

- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg5**

## Variable callExternFunction ( int function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 )

### Arguments

- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**

## Variable callExternFunction ( int function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 )

### Arguments

- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**

## Variable callExternFunction ( const char * function , int num_args , const Variable * args )

### Arguments

- *const char ** **function**
- *int* **num_args**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) ** **args**

## Variable callExternFunction ( int function )

### Arguments

- *int* **function**

## Variable callExternFunction ( const char * function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 , const Variable & arg5 , const Variable & arg6 , const Variable & arg7 )

### Arguments

- *const char ** **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg5**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg6**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg7**

## Variable callExternFunction ( int function , const Variable & arg0 , const Variable & arg1 , const Variable & arg2 , const Variable & arg3 , const Variable & arg4 , const Variable & arg5 , const Variable & arg6 )

### Arguments

- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg2**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg3**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg4**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg5**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg6**

## Variable callExternFunction ( int function , const Variable & arg0 , const Variable & arg1 )

### Arguments

- *int* **function**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg0**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **arg1**

## int reflect ( void * interpreter , const Variable & v )

### Arguments

- *void ** **interpreter**
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v**
