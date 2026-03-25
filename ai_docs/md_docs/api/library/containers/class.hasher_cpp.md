# Unigine::Hasher class (CPP)

**Header:** #include <UnigineHash.h>


The Hasher class converts any data types (string, structure, etc.) to indices supported by the hash tables.


## Hasher Class

### Members

---

## HashType create ( const Type & v )

Converts the given value to the type supported by the hash table. For example, hash for the String type will be generated as folows:
```cpp
struct Hasher<String>
{
	using HashType = unsigned int;
	UNIGINE_INLINE static HashType create(const char *v) { return String::hash(v); }
	UNIGINE_INLINE static HashType create(const String &v) { return String::hash(v.get(), v.size()); }
};

```


### Arguments

- *const Type &* **v** - The value to convert from.

### Return value

The converted value supported by the hash table.
