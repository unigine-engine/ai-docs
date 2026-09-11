# CigiSymbolShortControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiSymbolShortControl Class

### Enums

## CIGI_SYMBOL

| Name | Description |
|---|---|
| **CIGI_SYMBOL_NONE** = 0 | Attribute Select None in Short Symbol Control. |
| **CIGI_SYMBOL_SURFACE_ID** = 1 | Attribute Select ID in Short Symbol Control. |
| **CIGI_SYMBOL_PARENT_SYMBOL_ID** = 2 | Attribute Select Parent Symbol ID in Short Symbol Control. |
| **CIGI_SYMBOL_LAYER** = 3 | Attribute Select Layer in Short Symbol Control. |
| **CIGI_SYMBOL_FLASH_DUTY** = 4 | Attribute Select Flash Duty in Short Symbol Control. |
| **CIGI_SYMBOL_FLASH_PERIOD** = 5 | Attribute Select Flash Period in Short Symbol Control. |
| **CIGI_SYMBOL_POSITION_X** = 6 | Attribute Select Position X (U) in Short Symbol Control. |
| **CIGI_SYMBOL_POSITION_Y** = 7 | Attribute Select Position Y (V) in Short Symbol Control. |
| **CIGI_SYMBOL_ROTATION** = 8 | Attribute Select Rotation in Short Symbol Control. |
| **CIGI_SYMBOL_COLOR** = 9 | Attribute Select Color in Short Symbol Control. |
| **CIGI_SYMBOL_SCALE_X** = 10 | Attribute Select Scale X (U) in Short Symbol Control. |
| **CIGI_SYMBOL_SCALE_Y** = 11 | Attribute Select Scale Y (V) in Short Symbol Control. |

### Members

---

## int getSymbolID ( ) const

Returns the **Symbol ID** specified in the packet. It specifies the symbol to which this packet shall be applied.
### Return value

Symbol ID parameter value.
## int getSymbolState ( ) const

Returns the **Symbol State** specified in the packet.
### Return value

Symbol State parameter value. The following values are supported:
- 0 - Hidden.
- 1 - Visible.
- 2 - Destroyed.


## int getAttachState ( ) const

Returns the value of the **Attach State** parameter specified in the packet. Determines whether the symbol will be attached as a child to a parent symbol.
### Return value

Attach State parameter value. 1 the symbol is attached as a child; otherwise, 0.
## int getFlashControl ( ) const

Returns the value of the **Flash Control** parameter specified in the packet. Defines whether the IG shall continue the symbol�s flash cycle from its present state or restart it from the beginning.
### Return value

Flash Control parameter value: 0 if Continue; otherwise, 1.
## int getInheritColor ( ) const

Returns the value of the **Inherit Color** parameter specified in the packet. Specifies whether this symbol inherits its color from the symbol to which it is attached.
### Return value

**Inherit Color** parameter value: 1 if the color is inherited; otherwise, 0.
## int getSelect1 ( ) const

Returns the value of the **Attribute Select 1** parameter specified in the packet. Identifies the attribute whose value is returned by the [**getData1**](#getData1_uint) function.
### Return value

**Select 1** parameter value. One of the [CIGI_SYMBOL_*](#CIGI_SYMBOL_NONE) values.
## int getSelect2 ( ) const

Returns the value of the **Attribute Select 2** parameter specified in the packet. Identifies the attribute whose value is returned by the [**getData2**](#getData2_uint) function.
### Return value

**Select 2** parameter value. One of the [CIGI_SYMBOL_*](#CIGI_SYMBOL_NONE) values.
## unsigned int getData1 ( ) const

Returns the value of the **Attribute Value 1** parameter specified in the packet. Specifies the value of the attribute identified by the [**getAttribute1**](#getSelect1_int) function.
### Return value

**Data 1** parameter value.
## unsigned int getData2 ( ) const

Returns the value of the **Attribute Value 2** parameter specified in the packet. Specifies the value of the attribute identified by the [**getAttribute2**](#getSelect2_int) function.
### Return value

**Data 2** parameter value.
