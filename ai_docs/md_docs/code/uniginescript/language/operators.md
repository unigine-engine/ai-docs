# Operators

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Once we know of the existence of variables, we can begin to operate with them. For that purpose, UnigineScript integrates operators. **Operators** are mostly made of signs that are not part of the alphabet but are available in all keyboards.


## Numerical Operators


| Operation | Operator | Type | Description | Operand Types |
|---|---|---|---|---|
| Negation | - | unary | Returns a negated value of the operand (changes its sign to the opposite) | [Scalars](#scalar), [vectors](#vector) |
| Increment | ++ | unary | Increments the operand by 1 (both prefix and postfix notations are supported) | [Scalars](#scalar) |
| Decrement | -- | unary | Decrements the operand by 1 (both prefix and postfix notations are supported) | [Scalars](#scalar) |
| Multiplication | * | binary | Multiplies one operand by another | [Scalars](#scalar), [vectors](#vector) |
| Division | / | binary | Divides the first operand by the second operand | [Scalars](#scalar), [vectors](#vector) |
| Modulo | % | binary | Returns a remainder after numerical division of the first operand by the second operand | [*int*](../../../code/uniginescript/language/data_types.md#int), [*long*](../../../code/uniginescript/language/data_types.md#long), [*float*](../../../code/uniginescript/language/data_types.md#float) and [*double*](../../../code/uniginescript/language/data_types.md#float) |
| Addition | + | binary | Adds one operand to another | [Scalars](#scalar), [vectors](#vector), [string](#string) |
| Subtraction | - | binary | Subtracts the second operand from the first operand | [Scalars](#scalar), [vectors](#vector) |


```cpp
int a = 0, b = 0;
log.message("%d %d\n",++a,b++);
log.message("%d %d\n",++a,b++);
log.message("%d %d\n",a,b);

/* Output:
 * 1 0
 * 2 1
 * 2 2
 */

```


### Scalar Operands


All numerical operators that take two operands of different types perform an [automatic conversion of scalars](../../../code/uniginescript/language/data_types.md#conversion_scalar). The result is always the ***biggest*** type of two.


### Vector Operands


Some of numerical operators are applicable to [vector](../../../code/uniginescript/language/data_types.md#tree_d_data_types) types. All vector types can be added to, subtracted from and multiplied by operands of the same type. However, when performing operations on different types of vector operands or vectors and scalars, only specific combinations of operands are possible, because vector types are mostly [nonconvertible](../../../code/uniginescript/language/data_types.md#conversion_vector).


| First operand | Operator | Second operand | Result |
|---|---|---|---|
| All vector types: vec3 vec4 dvec3 dvec4 ivec3 ivec4 mat4 dmat4 quat | + - * | The same as of the first operand | Type of the operands |
| vec3 vec4 dvec3 dvec4 ivec3 ivec4 | / | The same as of the first operand | Type of the operands |
| All vector types: vec3 vec4 dvec3 dvec4 ivec3 ivec4 mat4 dmat4 quat | * / | int | Type of the first operand |
| vec3 vec4 dvec3 dvec4 mat4 dmat4 quat | * / | long float | Type of the first operand |
| dvec3 dvec4 mat4 dmat4 quat | * / | double | Type of the first operand |
| vec3 | * / | double dvec3 | dvec3 |
| vec4 | * / | double dvec4 | dvec4 |
| vec3 | + - | dvec3 | dvec3 |
| vec4 | + - | dvec4 | dvec4 |
| dvec3 | * / + - | vec3 | dvec3 |
| dvec4 | * / + - | vec4 | dvec4 |
| mat4 | * | vec3 vec4 dvec3 dvec4 dmat4 | Type of the second operand |
| mat4 dmat4 | * | quat | Type of the first operand |
| dmat4 | * | vec3 dvec3 | dvec3 |
| dmat4 | * | vec4 dvec4 | dvec4 |
| dmat4 | * | mat4 | dmat4 |
| quat | * | vec3 vec4 dvec3 dvec4 mat4 dmat4 | Type of the second operand |


### String Operators


These operators take only [*string*](../../../code/uniginescript/language/data_types.md#string) variables as operands.


| Operation | Operator | Type | Description |
|---|---|---|---|
| Concatenation | + | binary | A string into which two operands are joined |


Strings can be concatenated not only with strings but with variables of any base type due to type casting.

```cpp
float a = -3.9;
string str = "there can be a mixture";
str = str + " of integer (" + 56 + ") and floating point values (" + a + ")";
log.message("%s\n", str);

/* Output:
 * there can be a mixture of integer (56) and floating point values (-3.9)
 */

```


## Logical and Bitwise Operators


These operators take only the following types of variables as operands:

- [*int*](../../../code/uniginescript/language/data_types.md#int)
- [*long*](../../../code/uniginescript/language/data_types.md#long)


| Operation | Operator | Type | Description | Operand Types |
|---|---|---|---|---|
| Logical NOT | ! | unary | Negates a boolean expression | [*int*](../../../code/uniginescript/language/data_types.md#int), [*long*](../../../code/uniginescript/language/data_types.md#long) |
| Logical AND | && | binary | *true*, if both operands are *true* | [*int*](../../../code/uniginescript/language/data_types.md#int), [*long*](../../../code/uniginescript/language/data_types.md#long) |
| Logical OR | \|\| | binary | *true*, if one or both operands are *true* | [*int*](../../../code/uniginescript/language/data_types.md#int), [*long*](../../../code/uniginescript/language/data_types.md#long) |
| Bitwise NOT (complement) | ~ | unary | Logical negation of each bit | [*int*](../../../code/uniginescript/language/data_types.md#int), [*long*](../../../code/uniginescript/language/data_types.md#long) |
| Bitwise AND | & | binary | Logical AND operation on each pair of corresponding bits | [*int*](../../../code/uniginescript/language/data_types.md#int), [*long*](../../../code/uniginescript/language/data_types.md#long) |
| Bitwise inclusive OR | \| | binary | Logical OR operation on each pair of corresponding bits | [*int*](../../../code/uniginescript/language/data_types.md#int), [*long*](../../../code/uniginescript/language/data_types.md#long) |
| Bitwise exclusive OR | ^ | binary | Logical XOR operation on each pair of corresponding bits | [*int*](../../../code/uniginescript/language/data_types.md#int), [*long*](../../../code/uniginescript/language/data_types.md#long) |
| Shift left | << | binary | Shift bit pattern in the first operand to the left by the number of bits specified by the second operand | [*int*](../../../code/uniginescript/language/data_types.md#int), [*long*](../../../code/uniginescript/language/data_types.md#long) [*ivec3*](../../../code/uniginescript/language/data_types.md#ivec3) or [*ivec4*](../../../code/uniginescript/language/data_types.md#ivec4) can also be the 1st operand |
| Shift right | >> | binary | Shift bit pattern in the first operand to the right by the number of bits specified by the second operand | [*int*](../../../code/uniginescript/language/data_types.md#int), [*long*](../../../code/uniginescript/language/data_types.md#long) [*ivec3*](../../../code/uniginescript/language/data_types.md#ivec3) or [*ivec4*](../../../code/uniginescript/language/data_types.md#ivec4) can also be the 1st operand |


All non-zero values are equal to *true*, however, if *true* should be returned as a result of some operation, it will be always **1**. *false* is always **0**.


> **Notice:** When expressions with logical operators are evaluated, usually, short-circuit evaluation is used. That is, the second operand is only evaluated if the first operand does not suffice to determine the value of the whole expression. However, if the whole expression is enclosed in parentheses, all operands will be evaluated.


## Comparison Operators


- **Scalars** of different types ([*int*](../../../code/uniginescript/language/data_types.md#int), [*long*](../../../code/uniginescript/language/data_types.md#long), [*float*](../../../code/uniginescript/language/data_types.md#float), [*double*](../../../code/uniginescript/language/data_types.md#double)) can be freely comapared to each other, beacause of the [automatic conversion of scalars](../../../code/uniginescript/language/data_types.md#conversion_scalar).
- **Vectors** ([*vec3*](../../../code/uniginescript/language/data_types.md#vec3), [*vec4*](../../../code/uniginescript/language/data_types.md#vec4), [*dvec3*](../../../code/uniginescript/language/data_types.md#dvec3), [*dvec4*](../../../code/uniginescript/language/data_types.md#dvec4), [*ivec3*](../../../code/uniginescript/language/data_types.md#ivec3), [*ivec4*](../../../code/uniginescript/language/data_types.md#ivec4), [*mat4*](../../../code/uniginescript/language/data_types.md#mat4), [*quat*](../../../code/uniginescript/language/data_types.md#quat)) can only be compared with the ***same*** type.

  - [*vec3*](../../../code/uniginescript/language/data_types.md#vec3) can also be compared with [*dvec3*](../../../code/uniginescript/language/data_types.md#dvec3) and vice versa.
  - [*vec4*](../../../code/uniginescript/language/data_types.md#vec4) can also be compared with [*dvec4*](../../../code/uniginescript/language/data_types.md#dvec3) and vice versa.


> **Notice:** Two [*float*](../../../code/uniginescript/language/data_types.md#float) numbers are considered to be equal, if the difference between their values is less than 1E-6.


| Operation | Operator | Description | Operand Types |
|---|---|---|---|
| Equal to | == | Tests if both operands are equal | Scalars, vectors, string *int(0)* can be compared to an empty *string* and v.v. |
| Not equal to | != | Tests if both operands are not equal | Scalars, vectors, string *int(0)* can be compared to an empty *string* and v.v. |
| Less than | < | Tests if the first operand is less than the second operand | Scalars, string |
| Greater | > | Tests if the first operand is greater than the second operand | Scalars, string |
| Less than or equal to | <= | Tests if the first operand is less than the second operand or equal to it | Scalars, string |
| Greater than or equal to | >= | Tests if the first operand is greater than the second operand or equal to it | Scalars, string |


If the statement is *true*, the operator returns **1**, otherwise **0**.


## Assignment Operators


| Operation | Operator | Type | Description |
|---|---|---|---|
| Assignment | = | binary | Assign a value of the second operand to the first operand |
| "If-then-else" replacement | ? : | ternary | Can be used for conditional assignment, if this whole expression is the second operand of the assignment |


The conditional operator *?:* can be used as a shorthand for what would normally be single-line blocks of the "if-then-else" construction. If used appropriately, this operator can enhance readability of code. Its syntax is the following: *test_expression1 ? then_expression : else_expression*.

```cpp
int a = 10;
int b;
b = (a > 9) ? 100 : 200; // ternary operator usage

// this expression is equal to the previous one
if(a > 9) {
	b = 100;
} else {
	b = 200;
}
log.message("b =" + (b))
/* Output:
 * b = 200
 */

```


It is also possible to use the *?:* operator in expressions. For example:

```cpp
int a = 1;
int b = 2;
int c = 3;
int d = 4;

log.message("%s\n","test 1: " + (a == b) ? "a == b" : "a != b" + " final");
log.message("%s\n","test 2: " + ((c == d) ? "c == d" : "c != d") + " final");
log.message("%s\n","test 3: " + (a == b) ? "a == b and " + ((c == d) ? "c == d" : "c != d") : ("a != b and " + ((c == d) ? "c == d" : "c != d")));

```

 The output of the example is:
```text
test1: a != b final
test2: c != d final
test3: a != b and c != d

```


The assignment operator *=* can be combined with *+*, *-*, ***, */*, *%*, *&*, *|*, and *^*. These combined operators (*+=*, *-=*, **=*, */=*, *%=*, *&=*, *|=*, and *^=*) assign the result of the operation to the first operand (which must be a variable).


> **Notice:** UnigineScript does not support multiple assignments in an expression:
> ```cpp
> int a = 10;
> int b, c;
> a = b = c; // this won't work
> a = b += c; // this won't work either
>
> ```


## Access Operators


| Operation | Operator | Type | Description |
|---|---|---|---|
| Member access | . | binary | Access a member (the second operand) of the first operand. Can be used with: - [Classes](../../../code/uniginescript/language/oop.md#classes) to access member variables and functions - [Vectors](../../../code/uniginescript/language/containers/index.md#vector) and [maps](../../../code/uniginescript/language/containers/index.md#maps) to access member functions - [*vec3*](../../../code/uniginescript/language/data_types.md#vec3), [*vec4*](../../../code/uniginescript/language/data_types.md#vec4), [*dvec3*](../../../code/uniginescript/language/data_types.md#dvec3), [*dvec4*](../../../code/uniginescript/language/data_types.md#dvec4), [*ivec3*](../../../code/uniginescript/language/data_types.md#ivec3), [*ivec4*](../../../code/uniginescript/language/data_types.md#ivec4), [*mat4*](../../../code/uniginescript/language/data_types.md#mat4), [*dmat4*](../../../code/uniginescript/language/data_types.md#dmat4) and [*quat*](../../../code/uniginescript/language/data_types.md#quat) to access their elements via swizzles |
| Scope resolution | :: | - unary - for identifiers with the [global scope](../../../code/uniginescript/language/scope.md#global_scope) - binary - for identifiers with the class or namespace scope (class/namespace members). | Access an identifier outside its scope. For details, see [scope resolution operator](../../../code/uniginescript/language/scope.md#scope_resolution). |
| Access by index | [] | binary | Access an element by it index. Can be used with classes, vectors, maps, *vec3*, *vec4*, *mat4*, and *quat* |


## Type Testing Operator


The type testing operator ***is*** serves to check the type of a given variable. The operator returns1 when:

- A given variable belongs to a specified type
- A given object is an instance of a specified class
- A given object is an instance of a class that derives from a specified class


The syntax of the operator is the following:

```cpp
i is int
```


> **Notice:** The second operand can only be the type or class name, namely:
> - One of the scalar types
> - One of the vector types
> - String
> - User-defined class name
> - External class name


For example, this operator can be used in an [if-else](../../../code/uniginescript/language/control_statements/selection_statements/if_else.md) statement:

```cpp
class Foo { };

class Bar : Foo { };

void check(int v) {
	string s = typeinfo(v);
	// both the is operator and the is_int() function check if v is of the int type
	if(v is int) log.message("%s is int\n",s);
	if(is_int(v)) log.message("%s is int\n",s);
	// check if v is of the float type
	if(v is float) log.message("%s is float\n",s);
	if(is_float(v)) log.message("%s is float\n",s);
	// check if v is an instance of the Stream class or class derived from the Stream
	if(v is Stream) log.message("%s is Stream\n",s);
	// check if v is an instance of the File class
	if(v is File) log.message("%s is File\n",s);
	// check if v is an instance of the Foo or Bar class
	if(v is Foo) log.message("%s is Foo\n",s);
	// check if v is an instance of the Bar class
	if(v is Bar) log.message("%s is Bar\n",s);
}

check(1);
check(1.0f);
check(new File());
check(new Foo());
check(new Bar());

```

 The output is the following:
```text
int: 1 is int
int: 1 is int
float: 1 is int
float: 1 is int
File 000000000E9330E0 internal (5:0:0) is Stream
File 000000000E9330E0 internal (5:0:0) is File
Foo 000000000D06FCD0 (131072:0:0) is Foo
Bar 000000000D06FD00 (196608:0:0) is Foo
Bar 000000000D06FD00 (196608:0:0) is Bar

```


## Operator Precedence


If an expression contains several operators, they will be evaluated in the order shown below, from the top to the bottom.


| Operation | Operator |
|---|---|
| Parentheses | () |
| Access operators | [] . |
| Unary operators | ! - + ++ -- |
| Multiplicative operators | * / |
| Additive operators, string concatenation | + - |
| Bitwise shift | << >> |
| Comparison operators | == != < > <= >= |
| Bitwise NOT | ~ |
| Bitwise AND | & |
| Bitwise exclusive OR | ^ |
| Bitwise OR | \| |
| Logical NOT | ! |
| Logical AND | && |
| Logical OR | \|\| |
| Assignment operators | = += -= *= /= %= &= \|= ^= ?: |


## Operator Overloading


You can read about operator overloading [here](../../../code/uniginescript/language/oop.md#op_overloading).
