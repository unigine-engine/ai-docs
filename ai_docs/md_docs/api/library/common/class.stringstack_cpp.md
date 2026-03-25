# Unigine::StringStack class (CPP)

**Header:** #include <UnigineString.h>


A string that is stored in a stack. By default, a StringStack variable reserves 256 bytes on the stack. Memory is allocated dynamically only when the data size exceeds the specified *[capacity](#StringStacktmplargs_StringStacktmplargs_rvref_void)*.


> **Notice:** If you know in advance that the data size will be large (for example, when reading a text from a file), use [String](../../../api/library/common/class.string_cpp.md) instead.


Such strings are typically used in the following cases:


- When you construct a string and use it only once. ```cpp #include "AppWorldLogic.h" #include <UnigineString.h> #include <UnigineVector.h> #include <UnigineFileSystem.h> using namespace Unigine; StringStack<> AppWorldLogic::get_first_string() { return "This is a "; } StringStack<> AppWorldLogic::get_second_string() { return "string"; } void AppWorldLogic::my_file_write(FilePtr file, const char *s) { file->writeString("Sample Text\n"); file->writeString(s); } int AppWorldLogic::init() { // get a string StringStack<> str = get_first_string(); // construct the string str += get_second_string(); // somehow use the constructed string FilePtr file = File::create(); file->open("file.txt", "wb"); if (file->isOpened()) { my_file_write(file, str); file->close(); } return 1; } ```
- When you perform operations on strings, the results are always stored in the stack. ```cpp const char *one = "one"; const String two = get_second_string(); // add one string to another StringStack<> s0 = one + two; StringStack<> s1 = two + two; const String file_name = file->getName(); // get an extension if any StringStack<> ext = file_name.extension(); ``` > **Notice:** Pay attention to the type of the operation result to optimally use it and avoid issues.


## StringStack Class

### Members

---

## static StringStackPtr create ( )

Default constructor that creates an empty string of the default size (256 characters).
## static StringStackPtr create ( const String & s )

Copy constructor. Creates a string that stores a given string.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s** - String to be copied.

## static StringStackPtr create ( const StringStack <Capacity> & s )

Copy constructor.
### Arguments

- *const [StringStack](../../../api/library/common/class.stringstack_cpp.md)<Capacity> &* **s** - String stack of a specified size.

## static StringStackPtr create ( const char * s )

Copy constructor.
### Arguments

- *const char ** **s** - Pointer to a null-terminated string.

## void destroy ( )

Destroys the string.
## void StringStack<Capacity> ( StringStack <OtherCapacity> && s )

Copies a given string to the current string.
### Arguments

- *[StringStack](../../../api/library/common/class.stringstack_cpp.md)<OtherCapacity> &&* **s** - String of a given size to be copied.

## StringStack <Capacity> & operator= ( const StringStack <Capacity> & s )

Assignment operator for the string.
### Arguments

- *const [StringStack](../../../api/library/common/class.stringstack_cpp.md)<Capacity> &* **s** - String.

## StringStack <Capacity> & operator= ( const char * s )

Assignment operator for the string.
### Arguments

- *const char ** **s** - Pointer to a null-terminated string.

## StringStack <Capacity> & operator= ( StringStack <OtherCapacity> && s )

Assignment operator for the string.
### Arguments

- *[StringStack](../../../api/library/common/class.stringstack_cpp.md)<OtherCapacity> &&* **s** - String of the given size.

## StringStack <Capacity> & operator= ( const String & s )

Assignment operator for the string.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s** - String.
