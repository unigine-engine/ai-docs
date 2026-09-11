# Unigine::UlonArg Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to represent a [ULON](../../../code/formats/ulon_format.md) argument - a *name - value* pair. Arguments are additional parameters that can be associated with nodes and used for various purposes (e.g. to define a tooltip or a title for a material parameter declaration). Arguments are enclosed in angle brackets < > and can be separated using *"\t","\n","\r"*, as well as commas and spaces.


**Example:** Node node = value <**arg0** = *value0* **arg1** = *value1*,**arg2** = *value2*>


## UlonArg Class

### Members

## String getName () const

Returns the current ULON argument name.
### Return value

Current ULON argument name.
## UlonValue getValue () const

Returns the current ULON argument [value](../../../api/library/common/class.ulonvalue_usc.md).
### Return value

Current ULON argument [value](../../../api/library/common/class.ulonvalue_usc.md).
---

## static UlonArg ( )

Constructor. Creates a ULON argument.
