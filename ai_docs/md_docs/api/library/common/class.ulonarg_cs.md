# Unigine::UlonArg Class (CS)


This class is used to represent a [ULON](../../../code/formats/ulon_format.md) argument - a *name - value* pair. Arguments are additional parameters that can be associated with nodes and used for various purposes (e.g. to define a tooltip or a title for a material parameter declaration). Arguments are enclosed in angle brackets < > and can be separated using *"\t","\n","\r"*, as well as commas and spaces.


**Example:** Node node = value <**arg0** = *value0* **arg1** = *value1*,**arg2** = *value2*>


## UlonArg Class

### Properties

## 🔒︎ string Name

The ULON argument name.
## 🔒︎ UlonValue Value

The ULON argument [value](../../../api/library/common/class.ulonvalue_cs.md).
### Members

---

## UlonArg ( )

Constructor. Creates a ULON argument.
