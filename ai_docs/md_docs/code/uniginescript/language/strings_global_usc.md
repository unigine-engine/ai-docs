# String Global Functions (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## String Global Functions Class

### Members

---

## string addslashes ( string str )

Returns a string with backslashes before characters that need to be escaped. These characters are double quote (**"**), backslash (**\**), tabulation symbol (**\t**), new line symbol (**\n**), carriage return symbol (**\r**).
### Arguments

- *string* **str** - String to be escaped.

### Return value

Escaped string.
## int crc32 ( string string )

Returns a control sum for a given string.
### Arguments

- *string* **string** - String to calculate a control sum for.

### Return value

Control sum.
## Variable extension ( string str )

Returns an extension of a given file.
### Arguments

- *string* **str** - File name (or a full path to it) with the extension.

### Return value

File extension.
## Variable extension ( string str , string ext )

Changes file extension to the specified one.
### Arguments

- *string* **str** - File name or path.
- *string* **ext** - Extension to be set.

### Return value

New file name or file path.
## string format ( string str , ... )

Returns a string produced according to the formatting string. The formatting string is composed of zero or more ordinary characters (excluding **%**) that are copied directly to the result string and control sequences, each of which results in fetching its own parameter. Each control sequence consists of a percent sign (**%**) followed by one or more of these elements, in order:
- An optional number, a width specifier, that says how many characters (minimum) this conversion should result in.
- An optional precision specifier that says how many decimal digits should be displayed for floating-point numbers.
- A type specifier that says what type the argument data should be treated as. Possible types:

  - **c**: the argument is treated as an integer and presented as a character with that ASCII value.
  - **d** or **i**: the argument is treated as an integer and presented as a (signed) decimal number.
  - **o**: the argument is treated as an integer and presented as an octal number.
  - **u**: the argument is treated as an integer and presented as an unsigned decimal number.
  - **x**: the argument is treated as an integer and presented as a hexadecimal number (with lowercase letters).
  - **X**: the argument is treated as an integer and presented as a hexadecimal number (with uppercase letters).
  - **f**: the argument is treated as a float and presented as a floating-point number.
  - **g**: the same as **e** or **f**, the shortest one is selected.
  - **G**: the same as **E** or **F**, the shortest one is selected.
  - **e**: the argument is treated as using the scientific notation with lowercase 'e' (e.g. 1.2e+2).
  - **E**: the argument is treated as using the scientific notation with uppercase 'E' (e.g. 1.2E+2).
  - **s**: the argument is treated as and presented as a string.
  - **p**: the argument is treated as and presented as a pointer address.
  - **%**: a literal percent character. No argument is required.


### Arguments

- *string* **str** - Formatting string.
- *...*  - Arguments, multiple allowed.

### Return value

A formatted string.
### Examples


```cpp
string str = format("string: %s, int: %d and float: %.4e","some words",10, 1.2e-2);
// str now is "string: some words, int: 10 and float: 1.2000e-02"

```


## string lower ( string str )

Makes a string lowercase.
### Arguments

- *string* **str** - String to modify.

### Return value

Input string with all alphabetic characters converted to lowercase.
## int match ( string pattern , string str )

Simple string matching, which is faster than RegExp-based ones. Some wildcards are supported in the *pattern*:
- **?**: any single symbol.
- *****: any string of arbitrary length.
- **|**: *OR* statement; e.g.: *"red|white"* pattern matchs both *"red"* and *"white"* strings.


### Arguments

- *string* **pattern** - A pattern.
- *string* **str** - A target string.

### Return value

**1** if match is found, **0** otherwise.
## Variable memory ( int size )

Converts a given number of bytes to KB (kilobytes), MB (megabytes) or GB (gigabytes) and represents them as a string.
### Arguments

- *int* **size** - Number of bytes.

### Return value

The result of conversion. If the ***size*** value is less that1024, it won't be converted.
### Examples


```cpp
log.message("The result is: %s\n",memory(2048));

// The result is: 2.0 KB

```


## void printf ( string str , ... )

Prints a formatted string. See the [formatting string description](#format_string).
### Arguments

- *string* **str** - Formatting string.
- *...*  - Arguments, multiple allowed.

## int re_match ( string str , string regexp )

Performs a regular expression match. See the [RegExp class](../../../api/library/common/class.regexp_usc.md) documentation for more information on the syntax of regular expressions.
> **Notice:** This function is an analog of the [RegExp.match()](../../../api/library/common/class.regexp_usc.md#match_cstr_int) method.


### Arguments

- *string* **str** - String to search in.
- *string* **regexp** - Pattern.

### Return value

Length of the matched part, or **-1**, if the pattern could not be matched, and **-2**, if an error is encountered.
## string re_replace ( string str , string regexp , string after )

Performs a regular expression search and replace. See the [RegExp class](../../../api/library/common/class.regexp_usc.md) documentation for more information on the syntax of regular expressions.
> **Notice:** This function is an analog of the [RegExp.replace()](../../../api/library/common/class.regexp_usc.md#replace_cstr_cstr_String) method.


### Arguments

- *string* **str** - String to modify.
- *string* **regexp** - Pattern.
- *string* **after** - Replacement.

### Return value

Modified string.
## int re_search ( string str , string regexp , int id = [] )

Searches for a sub-string matching a given regular expression and returns a set of matches. See the [RegExp class](../../../api/library/common/class.regexp_usc.md) documentation for more information on the syntax of regular expressions.
> **Notice:** This function is an analog of the [RegExp.search()](../../../api/library/common/class.regexp_usc.md#search_cstr_int) method.


### Arguments

- *string* **str** - String to search in.
- *string* **regexp** - Pattern.
- *int* **id** - Reference to a [vector](../../../code/uniginescript/language/containers/index.md#vector).

### Return value

Size of a vector with matches.
## string replace ( string str , string before , string after )

Replaces all occurrences of a search string with a replacement string. If you don't need advanced replacing rules (like regular expressions), use this function instead of [re_replace()](#re_replace_string_string_string).
### Arguments

- *string* **str** - String to modify.
- *string* **before** - Search string.
- *string* **after** - Replacement sub-string.

### Return value

A string with replaced fragments.
## int sscanf ( string str , string format , int id = [] )

Parses a string according to a format. See the [formatting string description](#format_string).
### Arguments

- *string* **str** - String to parse.
- *string* **format** - Formatting string.
- *int* **id** - Reference to a [vector](../../../code/uniginescript/language/containers/index.md#vector).

### Return value

Size of a vector with parsed objects.
### Examples


```cpp
int res[10];
printf("%d\n",sscanf("10 20.32 string","%d %f %s",res));
printf("%s\n%s\n%s\n",typeinfo(res[0]),typeinfo(res[1]),typeinfo(res[2]));

```


```text
3
int: 10
float: 20.32
string: "string"

```


## int strchr ( string str , int c )

Finds the first occurrence of a given character in a string.
### Arguments

- *string* **str** - String to search in.
- *int* **c** - Character to search for.

### Return value

Position of the first character occurrence.
## int strcmp ( string s0 , string s1 )

Binary-safe string comparison.
### Arguments

- *string* **s0** - First string.
- *string* **s1** - Second string.

### Return value


- **0** if compared strings are the same.
- **-1** if the first different character in *s0* is less than that in *s1*.
- **1** if the first different character in *s0* is greater than that in *s1*.


### Examples


```cpp
string s0 = "abcd";
string s1 = "abaa";

int result = strcmp(s0, s1);

if(result == 0) {
    log.message("The strings are the same!");
} else {
    log.message("Comparison result: %d\n", result);
}

```


```text
Comparison result: 1
```


## string stripslashes ( string str )

Un-escapes a string quoted with [addslashes()](#addslashes_string).
### Arguments

- *string* **str** - String to be un-escaped.

### Return value

Un-escaped string.
## int strlen ( string str )

Gets a string length. (For UTF-8 encoded string, see [utf8strlen()](#utf8strlen_string) method.)
### Arguments

- *string* **str** - String to measure.

### Return value

Length of the given string.
## int strncmp ( string s0 , string s1 , int n )

Binary-safe string comparison of the first *n* characters.
### Arguments

- *string* **s0** - First string.
- *string* **s1** - Second string.
- *int* **n** - Number of characters to compare.

### Return value


- **0** if compared substrings are the same.
- Negative value if the first different character in *s0* is less than that in *s1*.
- Positive value if the first different character in *s0* is greater than that in *s1*.


### Examples


```cpp
string s0 = "abcd";
string s1 = "abacus";

int result = strncmp(s0, s1, 4);

if(result == 0) {
    log.message("The substrings are the same!");
} else {
    log.message("Comparison result: %d\n", result);
}

```


```text
Comparison result: 2
```


## int strrchr ( string str , int c )

Finds the last occurrence of a given character in a string.
### Arguments

- *string* **str** - String to search in.
- *int* **c** - Character to search for.

### Return value

Position of the last character occurrence.
## int strrstr ( string s0 , string s1 )

Searches the last occurence of a given sub-string in a string.
### Arguments

- *string* **s0** - String to search in.
- *string* **s1** - Sub-string to search for.

### Return value

Position of the last occurrence of the *needle* in the *haystack*.
## int strsplit ( string str , string delimiters , int id = [] )

Splits a string into a vector.
### Arguments

- *string* **str** - String to split.
- *string* **delimiters** - List of delimiters. If an empty string is passed, "**\t\n\r** " will be used by default.
- *int* **id** - Reference to a [vector](../../../code/uniginescript/language/containers/index.md#vector).

### Return value

Size of a vector with string parts.
## int strstr ( string haystack , string needle )

Searches a given sub-string in a string.
### Arguments

- *string* **haystack** - String to search in.
- *string* **needle** - Sub-string to search for.

### Return value

Position of the first occurrence of the *needle* in the *haystack*.
## string substr ( string str , int pos , int len = -1 )

Returns a specified part of a string. (For UTF-8 encoded string, see [utf8substr()](#utf8substr_string_int_int) method.)
### Arguments

- *string* **str** - String to truncate.
- *int* **pos** - Starting position of a sub-string.
- *int* **len** - Sub-string length.

### Return value

A sub-string.
## string trim ( string str , string symbols = 0 )

Removes from the string the specified leading and trailing characters.
> **Notice:** If no symbols are passed as an argument, white-space characters will be removed in the beginning or the end of the string, if found.


### Arguments

- *string* **str** - String to remove symbols from.
- *string* **symbols** - Symbols to be removed from the beginning or the end of the string.

### Return value

Trimmed string.
### Examples


```cpp
string s = "a b cd b b d b ab bba";
log.message("%s\n",trim(s," ab"));

```


```text
cd b b d
```


## Variable unicodeToUtf8 ( int src = [] )

Converts an array of Unicode characters into the UTF-8 encoded string.
### Arguments

- *int* **src** - Source array ID.

### Return value

UTF-8 string.
## string upper ( string str )

Makes a string uppercase.
### Arguments

- *string* **str** - String to modify.

### Return value

Input string with all alphabetic characters converted to uppercase.
## Variable utf8strlen ( string str )

Gets a length of the string in UTF-8 encoding. Unlike a simple [strlen()](#strlen_string) method, it returns the correct number of UTF-8 encoded characters.
### Arguments

- *string* **str** - String to measure.

### Return value

Length of the given string.
## Variable utf8substr ( string str , int pos , int len = -1 )

Returns a specified part of a string in UTF-8 encoding. Unlike a simple [substr()](#substr_string_int_int) method, it correctly counts UTF-8 encoded characters.
### Arguments

- *string* **str** - String to truncate.
- *int* **pos** - Starting position of a sub-string.
- *int* **len** - Sub-string length.

### Return value

A sub-string.
## Variable utf8ToUnicode ( string src , int size = [] )

Converts an encoded UTF-8 string into the array of Unicode characters.
### Arguments

- *string* **src** - Source string.
- *int* **size** - Return array ID.

### Return value

Unicode encoded character array.
