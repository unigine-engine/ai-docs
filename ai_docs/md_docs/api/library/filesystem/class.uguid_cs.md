# Unigine::UGUID Class (CS)


This class represents a globally unique identifier (a 40-byte hash value). The [SHA1](http://www.faqs.org/rfcs/rfc3174.html) algorithm is used for hash generation.


## UGUID Class

### Members

---

## UGUID ( )

Default constructor. Creates an empty 0-filled UGUID.
## UGUID ( string str )

Constructor. Creates a UGUID from the given source string. UGUID is generated using the [SHA1](http://www.faqs.org/rfcs/rfc3174.html) algorithm.
### Arguments

- *string* **str** - Source string.

## UGUID ( UGUID guid )

Copy constructor. Creates a UGUID by copying a source UGUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Source UGUID.

## void Generate ( )

Generates a new random UGUID value.
## void Generate ( string str )

Generates a UGUID value from the given source string using the [SHA1](http://www.faqs.org/rfcs/rfc3174.html) algorithm.
### Arguments

- *string* **str** - Source string.

## uint GetHashCode ( )

Returns a hash for the UGUID value.
### Return value

Hash generated for the UGUID value.
## void Clear ( )

Clears the UGUID value. All 40 bytes are set to 0.
## bool IsEmpty ( )

Returns a value indicating if the UGUID is empty (all 40 bytes are equal to 0).
### Return value

**true** if the UGUID is empty; otherwise, false.
## bool IsValid ( )

Returns a value indicating if the UGUID has a valid value.
### Return value

**true** if the value is valid; otherwise, false.
## void SetString ( string str )

Sets the UGUID value equal to a given 40-character hexadecimal string.
### Arguments

- *string* **str** - 40-character hexadecimal string representing the UGUID value.

## GUIDString MakeString ( )

Creates a 40-character hexadecimal string representing the GUID value.
### Return value

40-character hexadecimal string representing the GUID value.
