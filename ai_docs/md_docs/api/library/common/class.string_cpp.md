# Unigine::String class (CPP)

**Header:** #include <UnigineString.h>


Provides an interface to work with input and output data packed into the internal (not C++ standard) *String* class. Strings are stored in a heap, so they are slower than *[StringStack](../../../api/library/common/class.stringstack_cpp.md)* strings.


Such strings are typically used in the following cases:


- When you create a string to be passed to a container. ```cpp #include <UnigineString.h> #include <UnigineVector.h> using namespace Unigine; String AppWorldLogic::get_title() { String s = WindowManager::getMainWindow()->getTitle(); s += " Window"; return s; } int AppWorldLogic::init() { Vector<String> v; // create a string String s = "Modifier "; s += get_title(); // add it to the vector v.append(std::move(s)); // do something with the vector // ... return 1; } ```
- When you create a string to be used as the return value of the function. ```cpp String AppWorldLogic::get_title() { String s = WindowManager::getMainWindow()->getTitle(); s += " Window"; return s; } ```
- When you store a string that represents the function return value, and you don't intend to modify it. ```cpp void AppWorldLogic::log_file_guid(const UGUID &guid) { // string that stores an external function return value const String str = FileSystem::getAbsolutePath(guid); Log::message("Path: %s\n", str.get()); } ``` > **Notice:** Pay attention to the type of the function return value to optimally use it. It may help you to avoid addressing the cleared memory or another issue. ```cpp // String returned by this function will be automatically deleted const char *s = FileSystem::getAbsolutePath(guid); // and the s pointer will now point to the freed memory Log::message("Path: %s\n", s); 		// the application may crash ```
- When you store large texts (for example, read from a file).


Strings support *Small String Optimization (SSO)*: you can store *7* characters along with the *null termination symbol*. It means that the following code will not cause dynamic memory allocation:


```cpp
String s = �1234567�;

```


## String Class

### Members

---

## String ( )

Default constructor that creates an empty string.
## String ( const String & s )

Copy constructor.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s** - String to be copied.

## String ( const char * s )

Copy constructor.
### Arguments

- *const char ** **s** - Pointer to the null-terminated string.

## String ( const wchar_t * s )

Explicit constructor for a wide-character string.
### Arguments

- *const wchar_t ** **s** - Pointer to the wide-character null-terminated string.

## String ( const unsigned int * s )

Explicit constructor for a string from unsigned characters.
### Arguments

- *const unsigned int ** **s** - Pointer to the null-terminated string from unsigned characters.

## String ( String && s )

Constructor. Creates a string by copying a source string.
### Arguments

- *[String](../../../api/library/common/class.string_cpp.md) &&* **s** - Source string.

## String ( const char * s , int size )

Constructor. Creates a string of a defined size from the array of symbols.
### Arguments

- *const char ** **s** - Pointer to the null-terminated string.
- *int* **size** - Size of the string.

## const char * get ( )

Returns the pointer to the null-terminated string.
### Return value

The null-terminated string.
## char get ( int index )

Returns an *n*-th character of the string.
### Arguments

- *int* **index** - index of a character in range [0;string_length - 1]. > **Notice:** If the given index is out of the range bounds, the engine assertion will occur.

### Return value

An *n*-th character.
## char & get ( int index )

Returns an *n*-th character of the string.
### Arguments

- *int* **index** - index of a character in range [0;string_length - 1]. > **Notice:** If the given index is out of the range bounds, the engine assertion will occur.

### Return value

An *n*-th character.
## static bool isalpha ( int code )

Checks whether *code* is an alphabetic letter.
### Arguments

- *int* **code** - Character to be checked, cast to an int.

### Return value

true if the *code* is an alphabetic character; otherwise, false.
## static bool isdigit ( int code )

Checks whether *code* is a decimal digit character.
### Arguments

- *int* **code** - Character to be checked, cast to an int.

### Return value

true if the *code* is a decimal digit character; otherwise, false.
## double getDouble ( )

Returns the current string as a *double* value.
### Return value

The value of the variable.
## float getFloat ( )

Returns the current string as a *float* value.
### Return value

The value of the variable.
## int getInt ( )

Returns the current string as an *integer* value.
### Return value

The value of the variable.
## long long getLong ( )

Returns the current string as a *long long* value.
### Return value

The value of the variable.
## StringStack <> getLower ( )

Returns the string stack with all letters being lower-case.
### Return value

Lower-cased string stack.
## StringStack <> getUpper ( )

Returns the string stack with all letters being upper-case.
### Return value

Upper-cased string stack.
## static bool islower ( int code )

Checks whether *code* is a lower-case letter.
### Arguments

- *int* **code** - Character to be checked, cast to an int.

### Return value

true if the *code* is a lower-case character; otherwise, false.
## static bool isspace ( int code )

Checks whether *code* is a space or a horizontal tab character.
### Arguments

- *int* **code** - Character to be checked, cast to an int.

### Return value

true if the *code* is a space a horizontal tab character; otherwise, false.
## static bool isupper ( int code )

Checks whether *code* is an upper-case letter.
### Arguments

- *int* **code** - Character to be checked, cast to an int.

### Return value

true if the *code* is an upper-case character; otherwise, false.
## static StringStack <> absname ( const char * path , const char * str )

Returns an absolute path for given paths.
### Arguments

- *const char ** **path** - A working directory path.
- *const char ** **str** - A destination path.

### Return value

An absolute pathname.
### Examples


```cpp
String path = String::absname(engine.engine->getDataPath().get(), "bake_lighting/");
//path: C:/Projects/Sample/data/bake_lighting/

```


## static StringStack <> addslashes ( const char * str )

Modifies a string by putting backslashes before control characters that need escaping.
### Arguments

- *const char ** **str** - A string with control characters that need escaping.

### Return value

The modified str string with escaped control characters.
## void allocate ( int size )

Allocates the required memory.
### Arguments

- *int* **size** - Size of the allocated memory in bytes.

## String & append ( const String & s , int size )

Appends a given string to the end of the string.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s** - String to append.
- *int* **size** - Length of the string to be appended.

### Return value

Resulting string.
## String & append ( char c )

Appends a given symbol to the end of the string.
### Arguments

- *char* **c** - Symbol to append.

### Return value

Resulting string.
## String & append ( int pos , char c )

Inserts a given symbol at the specified position.
### Arguments

- *int* **pos** - Insertion position.
- *char* **c** - Symbol to insert.

### Return value

Resulting string.
## String & append ( const char * s , int size )

Appends a given null-terminated string to the end of the string.
### Arguments

- *const char ** **s** - Null-terminated string to append.
- *int* **size** - Length of the null-terminated string to be appended.

### Return value

Resulting string.
## String & append ( int pos , const char * s , int size )

Inserts a given null-terminated string at the specified position.
### Arguments

- *int* **pos** - Insertion position.
- *const char ** **s** - Null-terminated string to insert.
- *int* **size** - Length of the null-terminated string to be inserted.

### Return value

Resulting string.
## String & append ( int pos , const String & s , int size )

Inserts a given string at the specified position.
### Arguments

- *int* **pos** - Insertion position.
- *const [String](../../../api/library/common/class.string_cpp.md) &* **s** - String to insert.
- *int* **size** - Length of the string to be inserted.

### Return value

Resulting string.
## String & append ( String && s , int size )

Appends a given string to the end of the string.
### Arguments

- *[String](../../../api/library/common/class.string_cpp.md) &&* **s** - String to append.
- *int* **size** - Length of the string to be appended.

### Return value

Resulting string.
## static double atod ( const char * str )

Parses the str string and returns it as a *double* value.
### Arguments

- *const char ** **str** - A string.

### Return value

*Double* value of the str string.
## static float atof ( const char * str )

Parses the str string and returns it as a *float* value.
### Arguments

- *const char ** **str** - A string.

### Return value

*Float* value of the str string.
## static int atoi ( const char * str )

Parses the str string and returns it as an *integer* value.
### Arguments

- *const char ** **str** - A string.

### Return value

*Integer* value of the str string.
## static long long atol ( const char * str )

Parses the str string and returns it as a *long long* value.
### Arguments

- *const char ** **str** - A string.

### Return value

*Long long* value of the str string.
## String basename ( )

Returns a [filename with extension](#basename_const_char_ptr_StringStacktmplargs) extracted from the current string.
### Return value

A string containing filename with extension.
## static StringStack <> basename ( const char * str )

Extracts filename with extension from the str string and returns it.
### Arguments

- *const char ** **str** - Path to file.

### Return value


Filename with extension.


> **Notice:** If the input string does not contain a full stop ('**.**'), the same value as the str value will be returned.


### Examples


```cpp
String base = String::basename("C:/Projects/Sample/data/textures/albedo.png");
//base: albedo.png

```


## void clear ( )

Clears the string.
## static int compare ( const char * str0 , const char * str1 )

Compares the string *str0* to the string *str1* character by character.
### Arguments

- *const char ** **str0** - a string to be compared.
- *const char ** **str1** - a string to be compared.

### Return value


A value indicating the relationship between the strings:


- 0 � the contents of both strings are equal.
- other value � the contents of strings do not coincide.


## static int compare ( const char * str0 , const char * str1 , int case_sensitive )

Compares the string *str0* to the string *str1* character by character taking into account the character case � upper or lower.
### Arguments

- *const char ** **str0** - a string to be compared.
- *const char ** **str1** - a string to be compared.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise, case is ignored.

### Return value


A value indicating the relationship between the strings:


- 0 � the contents of both strings are equal.
- another value � the contents of strings do not coincide.


## int contains ( const char * s , int case_sensitive )

Checks whether the current string contains the **s** substring.
### Arguments

- *const char ** **s** - A string.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.

### Return value

1 if the current string contains the **s** substring; otherwise, **0**.
## int contains ( const String & s , int case_sensitive )

Checks whether the current string contains the **s** substring.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s** - A string.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.

### Return value

1 if the current string contains the **s** substring; otherwise, **0**.
## int contains ( char c , int case_sensitive )

Checks whether the current string contains the **c** character.
### Arguments

- *char* **c** - A character.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.

### Return value

1 if the current string contains the **c** character; otherwise, **0**.
## void copy ( const char * s , int size )

Copies *size* characters from the **s** string to the current string.
### Arguments

- *const char ** **s** - A source string.
- *int* **size** - Number of characters to be copied.

## void copy ( const String & s , int size )

Copies *size* characters from the **s** string to the current string.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s** - A source string.
- *int* **size** - Number of characters to be copied.

## void destroy ( )

Destroys the string.
## String dirname ( )

Returns a [parent directory's path](#dirname_const_char_ptr_StringStacktmplargs) from the current string.
### Return value

The directory's path without filename and extension.
## static StringStack <> dirname ( const char * str )

Returns a parent directory's path extracted from the str string.
### Arguments

- *const char ** **str** - Path to file

### Return value


The directory's path without filename and extension.


> **Notice:** If the str string does not meet path syntax, an empty value will be returned.


### Examples


```cpp
String dir = String::dirname("C:/Projects/Sample/data/textures/albedo.png");
// dir: C:/Projects/Sample/data/textures/

```


## void do_append ( char c )

Appends a given symbol to the end of the current string.
### Arguments

- *char* **c** - Symbol to append.

## void do_append ( int pos , char c )

Inserts a given symbol at the specified position of the current string.
### Arguments

- *int* **pos** - Insertion position.
- *char* **c** - Symbol to insert.

## void do_append ( int pos , const char * s , int size )

Inserts a given null-terminated string at the specified position of the current string.
### Arguments

- *int* **pos** - Insertion position.
- *const char ** **s** - Null-terminated string to insert.
- *int* **size** - Length of the null-terminated string to be inserted.

## void do_append ( const char * s , int size )

Appends a given null-terminated string to the end of the string.
### Arguments

- *const char ** **s** - Null-terminated string to append.
- *int* **size** - Length of the null-terminated string to be appended.

## void do_assign ( const char * s , int size )

Assigns a new value to the string, replacing its current contents with first *size* characters pointed by *s*.
### Arguments

- *const char ** **s** - The null-terminated string.
- *int* **size** - Number of characters.

## void do_copy ( const char * s , int size )

Copies *size* characters from the *s* string to the current string.
### Arguments

- *const char ** **s** - A source null-terminated string.
- *int* **size** - Number of characters to be copied.

## static StringStack <> dtoa ( double value , int precision , int use_inf )

Converts a double value to a string using specified precision.
### Arguments

- *double* **value** - An input value.
- *int* **precision** - Precision in the range **[-1; 17]**. Data is represented the following way: | Precision | Representation | Example | |---|---|---| | -1 | The shortest representation: decimal floating point or scientific notation (mantissa/exponent). | 2.6265e+2 | | 0-8 | Decimal floating point. | 262.65 | | 9-17 | The shortest representation: decimal floating point or scientific notation (mantissa/exponent) with the *precision* digits to be printed after the decimal point. | 2.6264999e+2 |
- *int* **use_inf** - A flag indicating whether to use -inf and inf values if the input value is out of the range (-1e9; 1e9).

### Return value

A string representation of the *value*.
## int empty ( )

Returns an empty flag.
### Return value

1 if the string is empty; otherwise, 0.
## int endsWith ( const char * s , int case_sensitive , int size )

Checks whether the current string ends with *size* characters of the **s** substring.
### Arguments

- *const char ** **s** - A string.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.
- *int* **size** - Number of characters to be checked starting from the beginning.

### Return value

1 if the current string ends with the specified substring; otherwise, 0.
## int endsWith ( const String & s , int case_sensitive , int size )

Checks whether the current string ends with *size* characters of the **s** substring.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s** - A string.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.
- *int* **size** - Number of characters to be checked starting from the beginning.

### Return value

1 if the current string ends with the specified substring; otherwise, 0.
## static int endsWith ( const char * data , const char * str , int case_sensitive , int data_size , int str_size )

Checks whether the **data** string ends with the str substring.
### Arguments

- *const char ** **data** - A string.
- *const char ** **str** - A substring.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.
- *int* **data_size** - Size of the string to be checked.
- *int* **str_size** - Number of substring characters to be checked starting from the beginning.

### Return value

1 if the string ends with the specified substring; otherwise, 0.
## String extension ( )

Parses the current string as a path and returns a [filename extension](#extension_const_char_ptr_StringStacktmplargs).
### Return value

Extension name if there is one in the current string; otherwise, empty string.
## static StringStack <> extension ( const char * str )

Parses a given string as a path and returns a filename extension.
### Arguments

- *const char ** **str** - A string to be parsed.

### Return value

Extension name if there is one in the given string; otherwise, empty string.
### Examples


```cpp
String ext = String::extension("C:/Projects/Sample/data/textures/albedo.png");
// ext: png

```


## static StringStack <> extension ( const char * str , const char * ext )

Modifies a given path by replacing a file extension with a specified one.
### Arguments

- *const char ** **str** - A path.
- *const char ** **ext** - An extension.

### Return value

A modified path.
### Examples


```cpp
String ext = String::extension("/textures/albedo.png", "tif");
// ext: /textures/albedo.tif

```


## String filename ( )

Returns a [filename](#filename_const_char_ptr_StringStacktmplargs) extracted from the current string without extension.
### Return value

A string containing filename without extension.
## static StringStack <> filename ( const char * str )


Extracts filename from the str string and returns it without extension.


> **Notice:** If the input string does not contain a full stop, an empty string will be returned.


### Arguments

- *const char ** **str** - Path to file.

### Return value

Filename without extension.
### Examples


```cpp
String filename = String::filename("/textures/albedo.png");
// filename: albedo

```


## int find ( char c , int case_sensitive )

Searches the string for the first occurrence of *c* character and returns its index.
### Arguments

- *char* **c** - A character.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.

### Return value

*Index* of a specified character if at least one match was found; otherwise, -1.
## int find ( const String & s , int case_sensitive )

Searches the string for the first occurrence of *s* substring and returns its index.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s** - A substring.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.

### Return value

*Index* of the first character of a specified string if at least one match was found; otherwise, -1.
## int find ( const char * s , int case_sensitive )

Searches the string for the first occurrence of *s* substring and returns its index.
### Arguments

- *const char ** **s** - A substring.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.

### Return value

*Index* of the first character of a specified string if at least one match was found; otherwise, -1.
## char first ( )

Returns the first character of the current string.
### Return value

The first character.
## char & first ( )

Returns the first character of the current string.
### Return value

The first character.
## static StringStack <> format ( const char * format , va_list argptr )


Returns a stack of formatted strings. A format string is composed of zero or more ordinary characters (excluding %) that are copied directly to the result string and control sequences, each of which results in fetching its own parameter. Each control sequence consists of a percent sign (%) followed by one or more of these elements, in order:


- An optional number, a width specifier, that says how many characters (minimum) this conversion should result in.
- An optional precision specifier that says how many decimal digits should be displayed for floating-point numbers.
- A type specifier that says what type the argument data should be treated as. Possible types:

  - **c**: the argument is treated as an integer and presented as a character with that ASCII value.
  - **d** or **i**: the argument is treated as an integer and presented as a (signed) decimal number.
  - **o**: the argument is treated as an integer and presented as an octal number.
  - **u**: the argument is treated as an integer and presented as an unsigned decimal number.
  - **x**: the argument is treated as an integer and presented as a hexadecimal number (with lower-case letters).
  - **X**: the argument is treated as an integer and presented as a hexadecimal number (with upper-case letters).
  - **f**: the argument is treated as a float and presented as a floating-point number.
  - **g**: the same as e or f, the shortest one is selected.
  - **G**: the same as E or F, the shortest one is selected.
  - **e**: the argument is treated as using the scientific notation with lower-case 'e' (e.g. 1.2e+2).
  - **E**: the argument is treated as using the scientific notation with upper-case 'E' (e.g. 1.2E+2).
  - **s**: the argument is treated as and presented as a string.
  - **p**: the argument is treated as and presented as a pointer address.
  - **%**: a literal percent character. No argument is required.


### Arguments

- *const char ** **format** - Format string.
- *va_list* **argptr** - Arguments pointer.

### Return value

[Stack](../../../api/library/common/class.stringstack_cpp.md) of formatted strings.
## StringStack <> format ( const char * format )


Returns a stack of formatted strings. A format string is composed of zero or more ordinary characters (excluding %) that are copied directly to the result string and control sequences, each of which results in fetching its own parameter. Each control sequence consists of a percent sign (%) followed by one or more of these elements, in order:


- An optional number, a width specifier, that says how many characters (minimum) this conversion should result in.
- An optional precision specifier that says how many decimal digits should be displayed for floating-point numbers.
- A type specifier that says what type the argument data should be treated as. Possible types:

  - **c**: the argument is treated as an integer and presented as a character with that ASCII value.
  - **d** or **i**: the argument is treated as an integer and presented as a (signed) decimal number.
  - **o**: the argument is treated as an integer and presented as an octal number.
  - **u**: the argument is treated as an integer and presented as an unsigned decimal number.
  - **x**: the argument is treated as an integer and presented as a hexadecimal number (with lower-case letters).
  - **X**: the argument is treated as an integer and presented as a hexadecimal number (with upper-case letters).
  - **f**: the argument is treated as a float and presented as a floating-point number.
  - **g**: the same as e or f, the shortest one is selected.
  - **G**: the same as E or F, the shortest one is selected.
  - **e**: the argument is treated as using the scientific notation with lower-case 'e' (e.g. 1.2e+2).
  - **E**: the argument is treated as using the scientific notation with upper-case 'E' (e.g. 1.2E+2).
  - **s**: the argument is treated as and presented as a string.
  - **p**: the argument is treated as and presented as a pointer address.
  - **%**: a literal percent character. No argument is required.


### Arguments

- *const char ** **format** - Format string.

### Return value

[Stack](../../../api/library/common/class.stringstack_cpp.md) of formatted strings.
## static StringStack <> ftoa ( float value , int precision )

Converts a float value to a string using specified precision.
### Arguments

- *float* **value** - An input value.
- *int* **precision** - Precision in the range **[-1; 17]**. Data is represented the following way: | Precision | Representation | Example | |---|---|---| | -1 | The shortest representation: decimal floating point or scientific notation (mantissa/exponent). | 2.6265e+2 | | 0-8 | Decimal floating point. | 262.65 | | 9-17 | The shortest representation: decimal floating point or scientific notation (mantissa/exponent) with the *precision* digits to be printed after the decimal point. | 2.6264999e+2 |

### Return value

A string representation of the *value*.
## int grow_to ( int new_length )

Returns the actual length of a string corresponding to amount of memory which is enough to contain at least the specified number of items.
### Arguments

- *int* **new_length** - Minimum string length.

### Return value

String length.
## static unsigned int hash ( const char * str , int size )

Returns a hash value of a given string.
### Arguments

- *const char ** **str** - A string.
- *int* **size** - Length of string to be hashed.

### Return value

Hash value.
## static StringStack <> itoa ( int value , int radix )

Returns string representation of a given decimal value.
### Arguments

- *int* **value** - An input decimal value.
- *int* **radix** - Numerical base used to represent the value as a string, between 2 and 16, where 10 means *decimal* base, 16 *hexadecimal*, 8 *octal*, and 2 *binary*.

### Return value

String representation of a specified integer.
## static StringStack <> joinPaths ( const char * p0 , const char * p1 )

Concatenates two paths and returns [normalized](#normalizePath_const_char_ptr_StringStacktmplargs) result.
### Arguments

- *const char ** **p0** - First part of the path (mainly a directory path).
- *const char ** **p1** - Second part of the path.

### Return value

Resulting path.
## static StringStack <> joinPaths ( const char * p0 , const String & p1 )

Concatenates two paths and returns a [normalized](#normalizePath_const_char_ptr_StringStacktmplargs) result.
### Arguments

- *const char ** **p0** - the first part of the path.
- *const [String](../../../api/library/common/class.string_cpp.md) &* **p1** - the second part of the path.

### Return value

Resulting path.
## static StringStack <> joinPaths ( const String & p0 , const char * p1 )

Concatenates two paths and returns a [normalized](#normalizePath_const_char_ptr_StringStacktmplargs) result.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **p0** - the first part of the path.
- *const char ** **p1** - the second part of the path.

### Return value

Resulting path.
## static StringStack <> joinPaths ( const String & p0 , const String & p1 )

Concatenates two paths and returns [normalized](#normalizePath_const_char_ptr_StringStacktmplargs) result.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **p0** - the first part of the path.
- *const [String](../../../api/library/common/class.string_cpp.md) &* **p1** - the second part of the path.

### Return value

Resulting path.
## static String & joinPaths ( String & ret , const char * p0 , const char * p1 , int size0 , int size1 )

Concatenates two paths of a defined size and returns a [normalized](#normalizePath_String_ref_const_char_ptr_int_String_ref) result.
### Arguments

- *[String](../../../api/library/common/class.string_cpp.md) &* **ret** - a string to store the result.
- *const char ** **p0** - the first part of the path (a directory path).
- *const char ** **p1** - the second part of the path.
- *int* **size0** - the size of the first part of the path.
- *int* **size1** - the size of the second part of the path.

### Return value

Resulting path.
## char last ( )

Returns the last character of the current string.
### Return value

The current character.
## char & last ( )

Returns the last character of the current string.
### Return value

The current character.
## String & lower ( )

Returns a lower-case equivalent of the current string. Non-alphabetic characters remain unchanged.
### Return value

A lower-cased string.
## static StringStack <> ltoa ( long long value , int radix )

Returns string representation of a given long long value.
### Arguments

- *long long* **value** - An input long long value.
- *int* **radix** - Numerical base used to represent the value as a string, between 2 and 16, where 10 means *decimal* base, 16 *hexadecimal*, 8 *octal*, and 2 *binary*.

### Return value

String representation of a specified long long value.
## static int match ( const char * pattern , const char * str )

Checks whether a str string matches a **pattern**.

> **Notice:** Only the following symbols are supported: ****, ?, +***

### Arguments

- *const char ** **pattern** - A string with a [Regular expression](../../../api/library/common/class.regexp_cpp.md#intro) of limited functionality (****, ?, +***).
- *const char ** **str** - A string to be checked.

### Return value

1 if *str* matches *pattern*; otherwise, 0.
## static StringStack <> memory ( size_t memory )

Returns a stack of strings containing information on memory consumption for the string.
### Arguments

- *size_t* **memory** - Amount of memory.

### Return value

Stack of strings containing information on memory consumption for the string.
## static StringStack <> normalizeDirPath ( const char * path )

Returns [normalized](#normalizePath_const_char_ptr_StringStacktmplargs) path string and ensures that it is a path to a directory (ends with a forward slash).
### Arguments

- *const char ** **path** - An input path string.

### Return value

Normalized path to a directory.
## static String & normalizeDirPath ( String & ret , const char * path , int size )

Returns [normalized](#normalizePath_const_char_ptr_StringStacktmplargs) path string and ensures that it is a path to a directory (ends with a forward slash).
### Arguments

- *[String](../../../api/library/common/class.string_cpp.md) &* **ret** - a string to store the result.
- *const char ** **path** - an input path string.
- *int* **size** - the size of the resulting string.

### Return value

Normalized path to a directory.
## static StringStack <> normalizePath ( const char * path )

Returns a de-escaped path string where all double backslashes are replaced with forward ones.
### Arguments

- *const char ** **path** - A string.

### Return value

Normalized path string.
## static String & normalizePath ( String & ret , const char * path , int size )

Returns a de-escaped path string where all double backslashes are replaced with forward ones.
### Arguments

- *[String](../../../api/library/common/class.string_cpp.md) &* **ret** - a string to store the result.
- *const char ** **path** - a path to the file to be normalized.
- *int* **size** - the size of the resulting string.

### Return value

Normalized path string.
## const char * operator const char * ( )

Returns the pointer to the current string.
### Return value

The pointer to the current string.
## const void * operator const void * ( )

Returns the pointer to the current string.
## String & operator+= ( const String & s )

String addition.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s** - The second string.

## String & operator+= ( const char * s )

Symbol addition.
### Arguments

- *const char ** **s** - The symbol.

## String & operator+= ( char c )

Symbol addition.
### Arguments

- *char* **c** - The symbol.

## String & operator= ( const char * s )

Assignment operator for the string.
### Arguments

- *const char ** **s** - The null-terminated string.

## String & operator= ( const String & s )

Assignment operator for the string.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s** - The value of the string.

## String & operator= ( String && s )

Move assignment operator for the string.
### Arguments

- *[String](../../../api/library/common/class.string_cpp.md) &&* **s** - The string reference.

## char & operator[] ( int index )

Array access.
### Arguments

- *int* **index** - Array item index.

### Return value

The array item.
## char operator[] ( int index )

Constant array access.
### Arguments

- *int* **index** - Array item index.

### Return value

The array item.
## String pathname ( )

Parses the current string and returns [path to a directory](#pathname_const_char_ptr_StringStacktmplargs).
### Return value

Directory name.
## static StringStack <> pathname ( const char * str )


Parses an input string and returns path to a directory.


> **Notice:** Unlike the *[dirname](#dirname_const_char_ptr_StringStacktmplargs)* function, the pathname is able to process the path syntax with parent directories ("../").


### Arguments

- *const char ** **str** - A path string.

### Return value

Directory name.
> **Notice:** If the str string does not meet path syntax, an empty value will be returned.


### Examples


```cpp
String pathname = String::pathname("C:/Projects/Sample/data/../../textures/albedo.png");
// pathname: C:/Projects/textures/

```


## void printf ( const char * format , ... )

Initializes a formatted string.
### Arguments

- *const char ** **format** - Format string.

## static StringStack <> relname ( const char * path , const char * str )

Returns a relative path for str relatively to path. Both paths can be either absolute or relative.
### Arguments

- *const char ** **path** - The path of a working directory.
- *const char ** **str** - A destination path.

### Return value

A relative pathname.
### Examples


```cpp
String path = "C:/projects/sample/data/";
String str = "C:/projects/sample/data/textures/albedo.png";
String result = String::relname(path, str);
// result: textures/albedo.png

String path = "C:/projects/sample/data/textures/";
String str = "C:/projects/sample/";
String result = String::relname(path, str);
// result: ../../

String path = "data/";
String str = "data/textures/albedo.png";
String result = String::relname(path, str);
// result: textures/albedo.png

```


## String & remove ( )

Removes the last symbol of the string.
### Return value

Resulting string.
## String & remove ( int pos , int size )

Removes the specified number of symbols at the given position from the string.
### Arguments

- *int* **pos** - Position.
- *int* **size** - Number of symbols to remove.

### Return value

Resulting string.
## static StringStack <> removeExtension ( const char * str )

Returns an input string without the file extension name.
### Arguments

- *const char ** **str** - A path string.

### Return value

Pathname without an extension.
## String replace ( const char * before , const char * after , int case_sensitive )

Replaces all occurrences of a substring in the current string with the specified new string.
### Arguments

- *const char ** **before** - String to be replaced.
- *const char ** **after** - String to replace the old one.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the replacement is case-sensitive; otherwise case is ignored.

### Return value

Resulting string.
## static StringStack <> replace ( const char * str , const char * before , const char * after , int case_sensitive )

Replaces all occurrences of a substring in a given string with the specified new string.
### Arguments

- *const char ** **str** - An original string.
- *const char ** **before** - String to be replaced.
- *const char ** **after** - String to replace the old one.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.

### Return value

Resulting string.
## static StringStack <> replace ( const char * str , char before , char after , int case_sensitive )

Replaces all occurrences of a character in a given string with the specified new string.
### Arguments

- *const char ** **str** - An original string.
- *char* **before** - A character to be replaced.
- *char* **after** - A character to replace the old one.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.

### Return value

Resulting string.
## String replace ( char before , char after , int case_sensitive )

Replaces all occurrences of a character in the current string with the specified new string.
### Arguments

- *char* **before** - A character to be replaced.
- *char* **after** - A character to replace the old one.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.

### Return value

Resulting string.
## void reserve ( int size )

Requests that the string capacity be adapted to a planned change in size to a length of up to *n* characters. The function has no effect on the length or content of the string.
### Arguments

- *int* **size** - Planned length for the string, in characters.

## void resize ( int size )

Resizes the string to a length of *n* characters.
### Arguments

- *int* **size** - New string length, in characters.

## static void reverseUtf8BiDirectional ( String & string )

Reverses the order of the characters in the bi-directional string containing mixed left-to-right and right-to-left scripts.
### Arguments

- *[String](../../../api/library/common/class.string_cpp.md) &* **string** - An input string.

## int rfind ( const String & s , int case_sensitive )

Searches the string for the last occurrence of *s* substring and returns the index of its last character.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s** - A substring to be located.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.

### Return value

An *index* of the first symbol of a substring if at least one match was found; otherwise, -1.
## int rfind ( char c , int case_sensitive )

Searches the string for the last occurrence of *c* character and returns its index.
### Arguments

- *char* **c** - A character to be located.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.

### Return value

An *index* of the character if at least one match was found; otherwise, -1.
## int rfind ( const char * s , int case_sensitive )

Searches the string for the last occurrence of *s* substring and returns the index of its last character.
### Arguments

- *const char ** **s** - A substring to be located.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.

### Return value

An *index* of the first symbol of a substring if at least one match was found; otherwise, -1.
## int scanf ( const char * format , ... )

Scans a formatted string.
### Arguments

- *const char ** **format** - Format string.

### Return value

Number of arguments successfully read, or EOF, if failure occurs.
## void shrink ( )

Requests the string to reduce its capacity to fit its size.
## int size ( )

Returns the size of the string.
### Return value

The size of the string.
## int space ( )

Returns the capacity of the string.
### Return value

The capacity of the string.
## static StringArray <> split ( const char * str , const char * delimiters )

Splits an input string into an array of substrings using a specified set of separator characters.
### Arguments

- *const char ** **str** - A string.
- *const char ** **delimiters** - A string each character of which is a separator denoting a point at which a split should occur.

### Return value

An array of substrings.
## static int sscanf ( const char * str , const char * format )

Scans a formatted string.
### Arguments

- *const char ** **str** - An input string.
- *const char ** **format** - Format string.

### Return value

Number of arguments successfully read, or EOF, if failure occurs.
## static int startsWith ( const char * data , const char * str , int case_sensitive , int data_size , int str_size )

Checks whether a given string starts with a specified substring.
### Arguments

- *const char ** **data** - A string.
- *const char ** **str** - A substring.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.
- *int* **data_size** - Length of the string.
- *int* **str_size** - Length of the substring.

### Return value

1 if the string starts with the specified substring; otherwise, 0.
## int startsWith ( const String & s , int case_sensitive , int size )

Checks whether the current string starts with a specified substring.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s** - A substring.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.
- *int* **size** - Length of the substring.

### Return value

1 if the string starts with the specified substring; otherwise, 0.
## int startsWith ( const char * s , int case_sensitive , int size )

Checks whether the current string starts with a specified substring.
### Arguments

- *const char ** **s** - A substring.
- *int* **case_sensitive** - Case sensitivity flag. If set to 1, the operation is case-sensitive; otherwise case is ignored.
- *int* **size** - Length of the substring.

### Return value

1 if the string starts with the specified substring; otherwise, 0.
## static StringStack <> stripslashes ( const char * str )

Removes backslashes from a string.
### Arguments

- *const char ** **str** - A string.

### Return value

Unquoted (de-escaped) string.
## String substr ( int pos , int size )

Returns the substring of the current string.
### Arguments

- *int* **pos** - Starting position.
- *int* **size** - Substring length.

### Return value

A Substring.
## static StringStack <> substr ( const char * str , int pos , int size )

Returns the substring of a given string.
### Arguments

- *const char ** **str** - A string.
- *int* **pos** - Starting position.
- *int* **size** - Substring length.

### Return value

A Substring.
## static StringStack <> substr ( const String & str , int pos , int size )

Returns the substring of a given string.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **str** - A string.
- *int* **pos** - Starting position.
- *int* **size** - Substring length.

### Return value

A Substring.
## static char toLower ( char c )

Returns a lower-case equivalent of a character, if possible. If not, the character is returned unchanged.
### Arguments

- *char* **c** - A character.

### Return value

A lower-cased character.
## static char toUpper ( char c )

Returns an upper-case equivalent of a character, if possible. If not, the character is returned unchanged.
### Arguments

- *char* **c** - A character.

### Return value

An upper-cased character.
## String trim ( const char * symbols )

Removes the specified symbols from the beginning and the ending of the current string.
### Arguments

- *const char ** **symbols** - A string with symbols to remove. > **Notice:** If the symbols argument is not specified, the function removes white spaces from the string.

### Return value

Resulting string.
### Examples


```cpp
// Example 1
const String string("     My Important String           ");
string.trim() // will return "My Important String" without spaces

// Example 2
const String string("%c$abc%%cbaMy Important String%c$baacbb%$a");
string.trim("abc$%") // will return "My Important String" without the specified symbols at the begging and the end

```


## static StringStack <> trim ( const char * str , const char * symbols )

Removes the specified symbols from the beginning and the ending of a given string.
### Arguments

- *const char ** **str** - A string.
- *const char ** **symbols** - A string with symbols to remove. > **Notice:** If the symbols argument is not specified, the function removes white spaces from the string.

### Return value

Resulting string.
## static String trimFirst ( const char * symbols )

Removes the specified symbols only from the beginning of the current string.
### Arguments

- *const char ** **symbols** - A string with symbols to remove. > **Notice:** If the symbols argument is not specified, the function removes white spaces from the string.

### Return value

Resulting string.
### Examples


```cpp
// Example 1
const String string("     My Important String     ");
string.trim() // will return "My Important String     " without spaces at the beggining

// Example 2
const String string("%c$abc%%cbaMy Important String%c$baacbb%$a");
string.trim("abc$%") // will return "My Important String%c$baacbb%$a" without the specified symbols at the begging

```


## static StringStack <> trimFirst ( const char * str , const char * symbols )

Removes the specified symbols only from the beginning of a given string.
### Arguments

- *const char ** **str** - A string.
- *const char ** **symbols** - A string with symbols to remove. > **Notice:** If the symbols argument is not specified, the function removes white spaces from the string.

### Return value

Resulting string.
## String trimLast ( const char * symbols )

Removes the specified symbols only from the end of the current string.
### Arguments

- *const char ** **symbols** - A string with symbols to remove. > **Notice:** If the symbols argument is not specified, the function removes white spaces from the string.

### Return value

Resulting string.
### Examples


```cpp
// Example 1
const String string("     My Important String     ");
string.trim() // will return "     My Important String" without spaces at the end

// Example 2
const String string("%c$abc%%cbaMy Important String%c$baacbb%$a");
string.trim("abc$%") // will return "%c$abc%%cbaMy Important String" without the specified symbols at the end

```


## static StringStack <> trimLast ( const char * str , const char * symbols )

Removes the specified symbols only from the end of a given string.
### Arguments

- *const char ** **str** - A string.
- *const char ** **symbols** - A string with symbols to remove. > **Notice:** If the symbols argument is not specified, the function removes white spaces from the string.

### Return value

Resulting string.
## static String::Direction unicodeGetDirection ( unsigned int code )

Returns the type of a unicode character.
### Arguments

- *unsigned int* **code** - A unicode character.

### Return value


An item of the *String::Direction* enumerator. The following types are possible:


- LTR - left-to-right characters.
- RTL - right-to-left characters.
- Neutral - non-directional characters.
- Digit - numeric characters.


## static int unicodeToUtf8 ( unsigned int code , char * dest )

Converts a unicode character to UTF-8.
### Arguments

- *unsigned int* **code** - A unicode character.
- *char ** **dest** - A destination pointer.

### Return value

Length of the wide-character string.
## static StringStack <> unicodeToUtf8 ( const wchar_t * src )

Converts a string to UTF-8.
### Arguments

- *const wchar_t ** **src** - A string.

### Return value

Resulting string.
## static StringStack <> unicodeToUtf8 ( const unsigned int * src )

Converts a set of unicode characters to a UTF-8-encoded string.
### Arguments

- *const unsigned int ** **src** - A set of characters.

### Return value

Resulting string.
## static StringStack <> unicodeToUtf8 ( unsigned int code )

Converts a unicode character to a UTF-8-encoded string.
### Arguments

- *unsigned int* **code** - A unicode character.

### Return value

Resulting string.
## String & upper ( )

Returns an upper-case equivalent of the current string. Non-alphabetic characters remain unchanged.
### Return value

An upper-cased string.
## int utf8strlen ( )

Returns the wide-character length of the current string.
### Return value

Length of the wide-character string.
## static int utf8strlen ( const char * str )

Returns the wide-character length of a string.
### Arguments

- *const char ** **str** - A string.

### Return value

Length of the wide-character string.
## String utf8substr ( int pos , int size )

Returns the wide-character substring.
### Arguments

- *int* **pos** - Starting position.
- *int* **size** - Substring length.

### Return value

The substring.
## static StringStack <> utf8substr ( const char * str , int pos , int size )

Returns the wide-character substring of a given string.
### Arguments

- *const char ** **str** - An input string.
- *int* **pos** - Starting position.
- *int* **size** - Substring length.

### Return value

The substring.
## int utf8ToUnicode ( wchar_t * dest , int size )

Converts a string into the wide-character string.
### Arguments

- *wchar_t ** **dest** - Pointer to the wide-character string.
- *int* **size** - Size of wide-character string in symbols.

### Return value

Length of the wide-character string.
## int utf8ToUnicode ( unsigned int * dest , int size )

Converts a string into the wide-character string.
### Arguments

- *unsigned int ** **dest** - Pointer to the wide-character string.
- *int* **size** - Size of wide-character string in symbols.

### Return value

Length of the wide-character string.
## static int utf8ToUnicode ( const char * src , wchar_t * dest , int size )

Converts a string into the wide-character string.
### Arguments

- *const char ** **src** - A source string.
- *wchar_t ** **dest** - Pointer to the wide-character string.
- *int* **size** - Size of wide-character string in symbols.

### Return value

Length of the wide-character string.
## static int utf8ToUnicode ( const char * src , unsigned int & code )

Converts a string into the wide-character string.
### Arguments

- *const char ** **src** - A source string.
- *unsigned int &* **code** - A character.

### Return value

Length of the wide-character string.
## static int utf8ToUnicode ( const char * src , unsigned int * dest , int size )

Converts a string into the wide-character string.
### Arguments

- *const char ** **src** - A source string.
- *unsigned int ** **dest** - Pointer to the set of characters.
- *int* **size** - Size of wide-character string in symbols.

### Return value

Length of the wide-character string.
## void vprintf ( const char * format , va_list argptr )

Initializes a formatted string.
### Arguments

- *const char ** **format** - Format string.
- *va_list* **argptr** - Arguments pointer.

## int vscanf ( const char * format , va_list argptr )

Scans a formatted string.
### Arguments

- *const char ** **format** - Format string.
- *va_list* **argptr** - Arguments pointer.

### Return value

Number of arguments successfully read, or EOF if failure occurs.
## static int vsscanf ( const char * str , const char * format , va_list argptr )

Scans a formatted string.
### Arguments

- *const char ** **str** - An input string.
- *const char ** **format** - Format string.
- *va_list* **argptr** - Arguments pointer.

### Return value

Number of arguments successfully read, or EOF if failure occurs.
