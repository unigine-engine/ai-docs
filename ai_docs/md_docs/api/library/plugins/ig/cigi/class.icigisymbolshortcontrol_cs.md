# CigiSymbolShortControl Class (CS)

**Inherits from:** CigiHostPacket


## CigiSymbolShortControl Class

### Enums

## CIGI_SYMBOL

| Name | Description |
|---|---|
| **NONE** = 0 | Attribute Select None in Short Symbol Control. |
| **SURFACE_ID** = 1 | Attribute Select ID in Short Symbol Control. |
| **PARENT_SYMBOL_ID** = 2 | Attribute Select Parent Symbol ID in Short Symbol Control. |
| **LAYER** = 3 | Attribute Select Layer in Short Symbol Control. |
| **FLASH_DUTY** = 4 | Attribute Select Flash Duty in Short Symbol Control. |
| **FLASH_PERIOD** = 5 | Attribute Select Flash Period in Short Symbol Control. |
| **POSITION_X** = 6 | Attribute Select Position X (U) in Short Symbol Control. |
| **POSITION_Y** = 7 | Attribute Select Position Y (V) in Short Symbol Control. |
| **ROTATION** = 8 | Attribute Select Rotation in Short Symbol Control. |
| **COLOR** = 9 | Attribute Select Color in Short Symbol Control. |
| **SCALE_X** = 10 | Attribute Select Scale X (U) in Short Symbol Control. |
| **SCALE_Y** = 11 | Attribute Select Scale Y (V) in Short Symbol Control. |

### Properties

## 🔒︎ int SymbolID

The **Symbol ID** specified in the packet. It specifies the symbol to which this packet shall be applied.
## 🔒︎ int SymbolState

The **Symbol State** specified in the packet.
## 🔒︎ int AttachState

The value of the **Attach State** parameter specified in the packet. Determines whether the symbol will be attached as a child to a parent symbol.
## 🔒︎ int FlashControl

The value of the **Flash Control** parameter specified in the packet. Defines whether the IG shall continue the symbol�s flash cycle from its present state or restart it from the beginning.
## 🔒︎ int InheritColor

The value of the **Inherit Color** parameter specified in the packet. Specifies whether this symbol inherits its color from the symbol to which it is attached.
## 🔒︎ int Select1

The value of the **Attribute Select 1** parameter specified in the packet. Identifies the attribute whose value is returned by the [**getData1**](#getData1_uint) function.
## 🔒︎ int Select2

The value of the **Attribute Select 2** parameter specified in the packet. Identifies the attribute whose value is returned by the [**getData2**](#getData2_uint) function.
## 🔒︎ uint Data1

The value of the **Attribute Value 1** parameter specified in the packet. Specifies the value of the attribute identified by the [**getAttribute1**](#getSelect1_int) function.
## 🔒︎ uint Data2

The value of the **Attribute Value 2** parameter specified in the packet. Specifies the value of the attribute identified by the [**getAttribute2**](#getSelect2_int) function.
### Members

---
