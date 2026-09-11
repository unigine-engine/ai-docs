# CigiSymbolTextDef Class (CS)

**Inherits from:** CigiHostPacket


## CigiSymbolTextDef Class

### Enums

## CIGI_TEXT_ALIGN

| Name | Description |
|---|---|
| **TOP_LEFT** = 0 | Text alignment in the top left corner. |
| **TOP_CENTER** = 1 | Text alignment in the top center position. |
| **TOP_RIGHT** = 2 | Text alignment in the top right corner. |
| **CENTER_LEFT** = 3 | Text alignment in the middle left position. |
| **CENTER** = 4 | Text alignment in the center of field. |
| **CENTER_RIGHT** = 5 | Text alignment in the middle right position. |
| **BOTTOM_LEFT** = 6 | Text alignment in the bottom left corner. |
| **BOTTOM_CENTER** = 7 | Text alignment in the bottom center position. |
| **BOTTOM_RIGHT** = 8 | Text alignment in the bottom right corner. |

## CIGI_TEXT_ORIENT

| Name | Description |
|---|---|
| **LEFT_TO_RIGHT** = 0 | Left to Right orientation of text. |
| **TOP_TO_BOTTOM** = 1 | Top to Bottom orientation of text. |
| **RIGHT_TO_LEFT** = 2 | Right to Left orientation of text. |
| **BOTTOM_TO_TOP** = 3 | Bottom to Top orientation of text. |

### Properties

## 🔒︎ int SymbolID

The Symbol ID specified in the packet.
## 🔒︎ int FontID

The value of the **Font ID** parameter specified in the packet. Determines the font that is used for this text symbol.
## 🔒︎ int Alignment

The value of the **Alignment** parameter specified in the packet. Specifies the position at which the IG shall place the symbol�s reference point in relation to the text.
## 🔒︎ int Orientation

The value of the **Orientation** parameter specified in the packet. Determines the orientation of text.
## 🔒︎ float FontSize

The value of the **Font Size** parameter specified in the packet. Specifies the font size in terms of the vertical units defined by the symbols surface's 2D coordinate system.
## 🔒︎ string Text

The value of the **Octet** parameter specified in the packet.
### Members

---
