# Unigine::UlonNode Class (CPP)

**Header:** #include <UnigineUlon.h>


This class is used to represent a [ULON](../../../code/formats/ulon_format.md) node.


Each ULON node has a **type**, a **name**, and a **value**. It can also have child ULON nodes and a parent node, thus forming a hierarchy.


A node is declared as follows:


```text
NodeType node_name = node_value
```


ULON nodes can be of the following types:


- ***Boolean*** *Node node = true*
- ***Integer number*** *Node node = 1234*
- ***Floating-point number*** *Node node = 3.1459*
- ***String***

  - Quoted string with standard escape characters: *Node node = "word word"*
  - Bare word, beginning with a lower case letter, containing only letters, digits, and underscores "_": *Node node = word1_word2*
  - Heredoc string enclosed in *#{ ... #}* (used for code fragments): *Node node = #{C++ C# USC HLSL USSL#}*
- ***Array*** containing a finite number of *integer, float*, and *string* elements *Node node = [100, 0.2, str str "str str str", #{vec4 asd = vec4_zero;#}]* This array has the following **6** elements:

  - 100
  - 0.2
  - str
  - str
  - str str str
  - vec4 asd = vec4_zero;


### Conditions


For each node a condition can be specified, if the condition fails the ULON node with all its children is ignored. Thus you can dynamically build the hierarchy of ULON nodes with a great degree of flexibility.


> **Notice:** Conditions are not parsed and executed automatically, processing of conditions is the responsibility of the user of the ULON format (e.g. in case of materials [UnigineScript](../../../code/uniginescript/index.md) and [UUSL](../../../code/uusl/index.md) are used).


Conditions are specified after the node's name, starting with the **if** keyword, the condition itself is enclosed in brackets **[ ... ]**.


Condition of the parent node is added to the condition of the child: **(parent_conditon) && (child_conditon)**


**Example:**


```text
Node parent if[var == 10 || var == 5]
{
    Node child_0  if[var == 3]
    Node child_1  if[var == 4]
    {
        Node child_2 if[var != 11]
        Node child_3 if[var != 25]
	}
}

```


The resulting conditions for each node are as follows:


- **parent** condition: (var1 == 10 || var1 == 5)
- **child_0** condition: (var1 == 10 || var1 == 5) && (var2 == 3)
- **child_1** condition: (var1 == 10 || var1 == 5) && (var2 == 4)
- **child_2** condition: (var1 == 10 || var1 == 5) && (var2 == 4) && (var3 != 11)
- **child_3** condition: (var1 == 10 || var1 == 5) && (var2 == 4) && (var3 != 25)


## UlonNode Class

### Members

## const char * getType () const

Returns the current type of the ULON node.
### Return value

Current ULON node type.
## const char * getName () const

Returns the current name of the ULON node.
### Return value

Current ULON node name.
## const char * getCondition () const

Returns the current [condition](#conditions) set for the ULON node.
> **Notice:** Conditions are not parsed and executed automatically, processing of conditions is the responsibility of the user of the ULON format (e.g. in case of materials [UnigineScript](../../../code/uniginescript/index.md) and [UUSL](../../../code/uusl/index.md) are used).

### Return value

Current [condition](#conditions) set for the ULON node.
## Ptr < UlonValue > getValue () const

Returns the current [value](../../../api/library/common/class.ulonvalue_cpp.md) of the ULON node.
### Return value

Current ULON node [value](../../../api/library/common/class.ulonvalue_cpp.md).
---

## static UlonNodePtr create ( )

Constructor. Creates a ULON node.
## bool load ( const char * path )

Loads ULON-data from the specified file and sets the current ULON node to be the root of the parsed hierarchy.
### Arguments

- *const char ** **path** - Path to the file containing ULON description.

### Return value

**true** if ULON-data from the specified file is read successfully; otherwise, **false**.
## bool parse ( const char * str )

Parses a given string into the ULON node.
### Arguments

- *const char ** **str** - String to parse.

### Return value

true if the string was parsed successfully; otherwise, false.
## Vector < Ptr < UlonNode > > getChildren ( ) const

Returns the list of all children of the ULON node.
### Return value

List of all ULON node's children.
## Vector < Ptr < UlonArg > > getArgs ( ) const

Returns the list of all [arguments](../../../api/library/common/class.ulonarg_cpp.md) of the ULON node.
### Return value

List of all [arguments](../../../api/library/common/class.ulonarg_cpp.md) of the ULON node.
## bool isArg ( const char * name ) const

Checks whether an [argument](../../../api/library/common/class.ulonarg_cpp.md) with a given name exists.
### Arguments

- *const char ** **name** - Name of the argument to be checked.

### Return value

true if an argument with the specified name exists; otherwise, false.
## float getArgFloat ( const char * name , float ret = 0 ) const


Returns the value of the ULON node [argument](../../../api/library/common/class.ulonarg_cpp.md) with the specified name as a float.


> **Notice:** To check, if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Argument name.
- *float* **ret** - Default value to be returned if a ULON node argument with the specified name is not found.

### Return value

Float value of the ULON node argument, if it exists; otherwise a default value set via the *ret* parameter.
## int getArgInt ( const char * name , int ret = 0 ) const


Returns the value of the ULON node [argument](../../../api/library/common/class.ulonarg_cpp.md) with the specified name as an integer.


> **Notice:** To check, if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Argument name.
- *int* **ret** - Default value to be returned if a ULON node argument with the specified name is not found.

### Return value

Integer value of the ULON node argument, if it exists; otherwise a default value set via the *ret* parameter.
## long long getArgLong ( const char * name , long long ret = 0 ) const


Returns the value of the ULON node [argument](../../../api/library/common/class.ulonarg_cpp.md) with the specified name as a 64-bit long long.


> **Notice:** To check, if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Argument name.
- *long long* **ret** - Default value to be returned if a ULON node argument with the specified name is not found.

### Return value

64-bit long long value of the ULON node argument, if it exists; otherwise a default value set via the *ret* parameter.
## bool getArgBool ( const char * name , bool ret = false ) const


Returns the value of the ULON node [argument](../../../api/library/common/class.ulonarg_cpp.md) with the specified name as a boolean.


> **Notice:** To check, if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Argument name.
- *bool* **ret** - Default value to be returned if a ULON node argument with the specified name is not found.

### Return value

Boolean value of the ULON node argument, if it exists; otherwise a default value set via the *ret* parameter.
## char getArgChar ( const char * name , char ret = 0 ) const


Returns the value of the ULON node [argument](../../../api/library/common/class.ulonarg_cpp.md) with the specified name as a char.


> **Notice:** To check, if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Argument name.
- *char* **ret** - Default value to be returned if a ULON node argument with the specified name is not found.

### Return value

Char value of the ULON node argument, if it exists; otherwise a default value set via the *ret* parameter.
## const char * getArgStr ( const char * name , const char * ret = "" ) const


Returns the value of the ULON node [argument](../../../api/library/common/class.ulonarg_cpp.md) with the specified name as a string.


> **Notice:** To check, if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Argument name.
- *const char ** **ret** - Default value to be returned if a ULON node argument with the specified name is not found.

### Return value

String value of the ULON node argument, if it exists; otherwise a default value set via the *ret* parameter.
## Vector < String > getArgArray ( const char * name ) const


Returns the value of the ULON node [argument](../../../api/library/common/class.ulonarg_cpp.md) with the specified name as an array of strings.


> **Notice:** To check, if an argument exists, use the [*isArg()*](#isArg_cstr_int) method.


### Arguments

- *const char ** **name** - Argument name.

### Return value

Array of strings representing elements of the array value, if it exists; otherwise an empty string array.
## void printUnusedData ( const char * name ) const

Prints warnings of unused data (node [values](../../../api/library/common/class.ulonvalue_cpp.md) and [arguments](../../../api/library/common/class.ulonarg_cpp.md)) for the file with the specified name to the Console for debugging.
### Arguments

- *const char ** **name** - File name.

## void clearUnusedData ( ) const

Clears all unused node data (node [values](../../../api/library/common/class.ulonvalue_cpp.md) and [arguments](../../../api/library/common/class.ulonarg_cpp.md)).
