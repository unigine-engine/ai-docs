# Unigine::RegExp Class (CS)


This class provides functionality required to work with regular expressions. In addition to this class, there are several functions, which may be more convenient for you to use, but they are somewhat slower, as each time they are called, a new regular expression is compiled. These functions are:


- *re_match()*
- *re_replace()*
- *re_search()*


Regular expressions are patterns that describe sets of strings. Single characters are main building blocks of regular expressions. However, several operators are used in the expressions to organize characters properly.


**.** (a dot) matches any character.


Each regular expression can be followed by a modifier that specifies a number of repetitions.


* is a modifier that means "from **0** to inf repetitions of a given character or sequence".


+ is a modifier that means "from **1** to inf repetitions of a given character or sequence".


? is a modifier that means "either **0** or **1** repetition of a given character or sequence".


[] specify a class of characters�a set of characters, any of which can be matched. Characters can be listed individually, one by one, or as a range of characters. In the latter case, two outermost characters are separated with a -. Examples: *[abc]*, *[a-c]*. The ^ operator has a special meaning inside classes.


\ starts an escape sequence, if followed by one of operator characters, or starts one of special sequences:


- \w matches any alphanumeric character. Equivalent to [a-zA-Z0-9_].
- \W matches any non-alphanumeric character. Equivalent to [^a-zA-Z0-9_].
- \b matches a word boundary. A word is a sequence of alphanumeric characters, so the end of it is indicated by a whitespace or non-alphanumeric character. This is a zero-width assertion.
- \B matches only inside a word. This is a zero-width assertion.


() mark a group. Groups specify different components of a single pattern. Example: *Mr. (\w+) (\w+)*.


^ specifies the beginning of a string or means a complement, when used as the first character between [ and ].


$ specifies the end of a string.


| specifies alternation. Matches any string that matches either of its operands. Examples: *milk|honey*.


[abcd$] matches any of the following: *"a", "b", "c", "d", "$"*.


[^5] matches any character but "5".


.* matches anything.


home-?brew matches either *"homebrew"* or *"home-brew"*.


bra+in[sz] matches *"brains"* or *"brainz"* or *"braains"*, etc.


(\w+), let's go (.+) matches, for example, *"Andy, let's go for a walk"* and yield two groups, *"Andy"* and *"for a walk"*.


## RegExp Class

### Members

---

## RegExp ( )

Default constructor that creates an empty instance.
## RegExp ( string pattern )

Constructor that creates a regular expression based on a provided pattern.
### Arguments

- *string* **pattern** - Pattern to be used for matching.

## int IsCompiled ( )

Returns a value indicating whether the current pattern is compiled and, therefore, can be used for matching.
### Return value

**1** if the pattern is compiled; otherwise, **0**.
## string GetGroup ( int number )

Returns a partial match corresponding to a specified group. Groups are parts of a pattern that match different components; they are marked by parentheses (**()**) in the pattern. Groups are numbered starting with **0** from left to right.
### Arguments

- *int* **number** - A non-negative number of a desired group. The number should not exceed the value returned by [*getNumGroups()*](#getNumGroups_int).

### Return value

Partial match corresponding to the group.
## int GetNumGroups ( )

Returns a number of groups in the current pattern. Groups are marked by parentheses (**()**) and are numbered starting with **0** from left to right.
### Return value

Number of groups in the current pattern.
## int Compile ( string pattern )

Compiles a provided regular expression pattern. This expression will be used for future matches.
### Arguments

- *string* **pattern** - Pattern to be used for matching, etc.

### Return value

**1** if the pattern is compiled successfully; otherwise, **0**.
## int Match ( string str )

Matches the pattern against a string.
### Arguments

- *string* **str** - String to match.

### Return value

**1** if the whole string is matched; otherwise, **0**.
## string Replace ( string str , string after )

Searches for the pattern in a given string and replaces all its occurrences with another string.
### Arguments

- *string* **str** - String to search and replace in.
- *string* **after** - Replacement string.

### Return value

Modified string.
## int Search ( string str )

Searches for a sub-string matching the pattern in a given string.
### Arguments

- *string* **str** - String to search in.

### Return value

Number of groups in the pattern, if a match is found; otherwise, **0**.
