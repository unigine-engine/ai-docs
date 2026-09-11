# Unigine::PathWildcards Class (CPP)

**Header:** #include <UniginePathWildcards.h>


This class represents a container of path patterns (***wildcards***) that can be used to check if a given path matches any of the stored patterns. It is commonly used for filtering files and directories based on pattern matching.


> **Notice:** For a comprehensive guide on wildcard syntax, see the **[Path Wildcards](../../../principles/filesystem/wildcards.md)** article.


Supported wildcard characters:


- `*` � matches any sequence of characters except `/`.
- `**` � matches any sequence of directories (including none), allowing patterns to span multiple directory levels.
- `?` � matches exactly one character except `/` (ASCII only).
- `[...]` � matches exactly one character from a set or range (e.g., `[a-z0-9]`, `[abc]`). Also supports POSIX character classes: `[:alnum:]`, `[:alpha:]`, `[:digit:]`, `[:lower:]`, `[:upper:]`, `[:space:]`, `[:punct:]`, `[:xdigit:]`.
- `[!...]` or `[^...]` � matches exactly one character NOT in the set (e.g., `[!0-9]`).


Pattern matching rules:


- A directory separator is a forward slash `/`.
- If there is a directory separator at the beginning or middle of the pattern, then the pattern is relative to the data path root. Otherwise, the pattern may match at any directory level.
- A trailing slash `/` in a pattern means "match this directory and everything inside it".
- Use a backslash to escape `[` or `]` characters in patterns (e.g., `file\[1\].txt` matches `file[1].txt`).
- The `*` and `?` wildcards cannot be escaped as these characters are forbidden in file names on Windows.
- Patterns are case-sensitive.


> **Notice:** The `?` wildcard and character ranges `[...]` do not work correctly with non-ASCII characters (e.g., Unicode). Use `*` for matching non-ASCII characters.


The following code snippet shows a usage example:


<details>
<summary>PathWildcards Usage Example</summary>

```cpp
#include <UniginePathWildcards.h>
#include <UnigineLog.h>
#include <UnigineVector.h>

// Create a filter with multiple patterns using Vector
Vector<String> patterns = {
	"*.tmp",          // Ignore all .tmp files
	"*.bak",          // Ignore all .bak files
	"build/",         // Ignore "build" folder and contents
	"**/cache/",      // Ignore "cache" folder at any depth
	"log_??.txt",     // Ignore log_XX.txt (exactly 2 characters)
	"data[0-9].csv",  // Ignore data0.csv through data9.csv
	"[._]*"           // Ignore files starting with . or _
};
PathWildcards ignore_patterns(patterns);

// Check the filter state
Log::message("Filter is empty: %d\n", ignore_patterns.empty());   // 0 (false)
Log::message("Number of patterns: %d\n", ignore_patterns.size()); // 7

// Iterate through all patterns by index
for (int i = 0; i < ignore_patterns.size(); i++)
{
	Log::message("Pattern[%d]: %s\n", i, ignore_patterns.getPattern(i));
}

// Get all patterns as a vector (two equivalent ways)
Vector<String> all_patterns = ignore_patterns.get();
// or: ignore_patterns.get(all_patterns);

// Test file paths against the filter
Vector<String> files = {
	"src/main.cpp",        // [OK] - no pattern matches
	"build/output.exe",    // [SKIP] - matches "build/"
	"data/cache/temp.dat", // [SKIP] - matches "**/cache/"
	"backup.bak",          // [SKIP] - matches "*.bak"
	"log_01.txt",          // [SKIP] - matches "log_??.txt" (one ? = one char)
	"log_1.txt",           // [OK] - doesn't match (only one char after _)
	"data5.csv",           // [SKIP] - matches "data[0-9].csv"
	"dataX.csv",           // [OK] - doesn't match (X is not 0-9)
	".gitignore",          // [SKIP] - matches "[._]*" (starts with .)
	"_temp_file",          // [SKIP] - matches "[._]*" (starts with _)
	"readme.txt"           // [OK] - no pattern matches
};

for (const String& file : files)
{
	if (ignore_patterns.matchPath(file))
		Log::message("[SKIP] %s\n", file.get());
	else
		Log::message("[OK] %s\n", file.get());
}

// Replace all patterns with a single new one
ignore_patterns.set("*.log");
Log::message("After set(): %d patterns\n", ignore_patterns.size()); // 1

// Remove all patterns from the filter
ignore_patterns.clear();
Log::message("After clear(): empty = %d\n", ignore_patterns.empty()); // 1 (true)

// Normalize a pattern string (removes duplicate slashes, converts backslashes)
StringStack<> normalized = PathWildcards::normalizePattern("folder\\\\subfolder//file.txt");
Log::message("Normalized: %s\n", normalized.get()); // "folder/subfolder/file.txt"

```

</details>


## PathWildcards Class

### Members

---

## PathWildcards ( )

Default constructor. Creates an empty **PathWildcards** instance with no patterns.
## PathWildcards ( const char* pattern )

Constructor. Creates a **PathWildcards** instance and adds the specified pattern.
### Arguments

- *const char** **pattern** - Initial pattern to add.

## PathWildcards ( const Vector < String >& patterns )

Constructor. Creates a **PathWildcards** instance and adds all patterns from the specified vector.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)>&* **patterns** - Vector of patterns to add.

## bool empty ( ) const

Returns a value indicating whether the **PathWildcards** instance contains no patterns.
### Return value

true if there are no patterns stored; otherwise, false.
## int size ( ) const

Returns the number of patterns stored in the **PathWildcards** instance.
### Return value

The number of patterns.
## void clear ( )

Removes all patterns from the **PathWildcards** instance.
## void add ( const char* pattern )

Adds a single pattern to the **PathWildcards** instance. The pattern is normalized internally (duplicate slashes are removed, backslashes are converted to forward slashes except when escaping brackets).
### Arguments

- *const char** **pattern** - The pattern to add.

## void add ( const Vector < String >& patterns )

Adds multiple patterns from the specified vector to the **PathWildcards** instance.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)>&* **patterns** - Vector of patterns to add.

## void set ( const char* pattern )

Clears all existing patterns and sets a single new pattern.
### Arguments

- *const char** **pattern** - The pattern to set.

## void set ( const Vector < String >& patterns )

Clears all existing patterns and sets new patterns from the specified vector.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)>&* **patterns** - Vector of patterns to set.

## void get ( Vector < String >& patterns ) const

Appends all stored patterns to the specified vector.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)>&* **patterns** - Output vector to receive the patterns. Patterns are appended to this vector.

## Vector < String > get ( ) const

Returns a vector containing all stored patterns.
### Return value

A vector containing all stored patterns.
## const char* getPattern ( int i ) const

Returns the pattern at the specified index.
### Arguments

- *int* **i** - The index of the pattern to retrieve. Must be in the range [0, size()).

### Return value

The pattern at the specified index.
## bool matchPath ( const char* path ) const

Checks if the specified path matches any of the stored patterns. The path is normalized internally before matching.
### Arguments

- *const char** **path** - The path to check.

### Return value

true if the path matches any of the stored patterns; otherwise, false.
## bool matchNormalizedPath ( const char* normalized_path ) const

Checks if the specified pre-normalized path matches any of the stored patterns. Use this method for better performance when the path is already normalized.
### Arguments

- *const char** **normalized_path** - The normalized path to check. The path should be pre-normalized using *[String::normalizePath()](../../../api/library/common/class.string_cpp.md#normalizePath_const_char_ptr_StringStacktmplargs)* or *[String::normalizeDirPath()](../../../api/library/common/class.string_cpp.md#normalizeDirPath_const_char_ptr_StringStacktmplargs)*.

### Return value

true if the path matches any of the stored patterns; otherwise, false.
## static StringStack <> normalizePattern ( const char* pattern )

Normalizes a pattern by removing duplicate slashes and converting backslashes to forward slashes (except when escaping bracket characters). This is a static utility method.
### Arguments

- *const char** **pattern** - The pattern to normalize.

### Return value

The normalized pattern.
