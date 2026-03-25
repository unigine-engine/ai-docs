# CigiSymbolClone Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiSymbolClone Class

### Members

---

## int getSymbolID ( ) const

Returns the **Symbol ID** specified in the packet. The identifier of the symbol that is being defined.
### Return value

Symbol ID parameter value.
## int getSourceID ( ) const

Returns the **Source ID** specified in the packet. Determines whether the new symbol will be a copy of an existing symbol or an instance of an IG-defined symbol template.
### Return value

Source ID parameter value.
## int getSourceType ( ) const

Returns the value of the **Source Type** parameter specified in the packet. Defines whether the type of the source symbol is Symbol Template or Symbol.
### Return value

Source Type parameter value: 1 if source type is the Symbol Template; otherwise, 0.
