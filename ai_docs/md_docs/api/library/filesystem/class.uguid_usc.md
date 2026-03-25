# Unigine::UGUID Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


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

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - Source UGUID.

## void generate ( )

Generates a new random UGUID value.
## void generate ( string str )

Generates a UGUID value from the given source string using the [SHA1](http://www.faqs.org/rfcs/rfc3174.html) algorithm.
### Arguments

- *string* **str** - Source string.

## void clear ( )

Clears the UGUID value. All 40 bytes are set to 0.
## int isEmpty ( )

Returns a value indicating if the UGUID is empty (all 40 bytes are equal to 0).
### Return value

**1** if the UGUID is empty; otherwise, **0**.
## int isValid ( )

Returns a value indicating if the UGUID has a valid value.
### Return value

**1** if the value is valid; otherwise, **0**.
## void setString ( string str )

Sets the UGUID value equal to a given 40-character hexadecimal string.
### Arguments

- *string* **str** - 40-character hexadecimal string representing the UGUID value.
