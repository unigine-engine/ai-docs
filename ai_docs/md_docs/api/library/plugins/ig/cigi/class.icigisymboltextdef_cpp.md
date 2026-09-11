# CigiSymbolTextDef Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiSymbolTextDef Class

### Enums

## CIGI_TEXT_ALIGN

| Name | Description |
|---|---|
| **CIGI_TEXT_ALIGN_TOP_LEFT** = 0 | Text alignment in the top left corner. |
| **CIGI_TEXT_ALIGN_TOP_CENTER** = 1 | Text alignment in the top center position. |
| **CIGI_TEXT_ALIGN_TOP_RIGHT** = 2 | Text alignment in the top right corner. |
| **CIGI_TEXT_ALIGN_CENTER_LEFT** = 3 | Text alignment in the middle left position. |
| **CIGI_TEXT_ALIGN_CENTER** = 4 | Text alignment in the center of field. |
| **CIGI_TEXT_ALIGN_CENTER_RIGHT** = 5 | Text alignment in the middle right position. |
| **CIGI_TEXT_ALIGN_BOTTOM_LEFT** = 6 | Text alignment in the bottom left corner. |
| **CIGI_TEXT_ALIGN_BOTTOM_CENTER** = 7 | Text alignment in the bottom center position. |
| **CIGI_TEXT_ALIGN_BOTTOM_RIGHT** = 8 | Text alignment in the bottom right corner. |

## CIGI_TEXT_ORIENT

| Name | Description |
|---|---|
| **CIGI_TEXT_ORIENT_LEFT_TO_RIGHT** = 0 | Left to Right orientation of text. |
| **CIGI_TEXT_ORIENT_TOP_TO_BOTTOM** = 1 | Top to Bottom orientation of text. |
| **CIGI_TEXT_ORIENT_RIGHT_TO_LEFT** = 2 | Right to Left orientation of text. |
| **CIGI_TEXT_ORIENT_BOTTOM_TO_TOP** = 3 | Bottom to Top orientation of text. |

### Members

---

## int getSymbolID ( ) const

Returns the Symbol ID specified in the packet.
### Return value

Symbol ID.
## int getFontID ( ) const

Returns the value of the **Font ID** parameter specified in the packet. Determines the font that is used for this text symbol.
### Return value

Font ID parameter value. The following values are supported:

- 0 - IG Default.

Proportional:
- 1 - Sans Serif.
- 2 - **Sans Serif Bold**.
- 3 - *Sans Serif Italic*.
- 4 - ***Sans Serif Bold Italic***.
- 5 - Serif.
- 6 - **Serif Bold**.
- 7 - *Serif Italic*.
- 8 - ***Serif Bold Italic***.

Monospace:
- 9 - Sans Serif.
- 10 - **Sans Serif Bold**.
- 11 - *Sans Serif Italic*.
- 12 - ***Sans Serif Bold Italic***.
- 13 - Serif.
- 14 - **Serif Bold**.
- 15 - *Serif Italic*.
- 16 - ***Serif Bold Italic***.
- 17-255 - IG-defined.


## int getAlignment ( ) const

Returns the value of the **Alignment** parameter specified in the packet. Specifies the position at which the IG shall place the symbol�s reference point in relation to the text.
### Return value

**Alignment** parameter value. One of the [CIGI_TEXT_ALIGN_*](#CIGI_TEXT_ALIGN_TOP_LEFT) values.
## int getOrientation ( ) const

Returns the value of the **Orientation** parameter specified in the packet. Determines the orientation of text.
### Return value

**Orientation** parameter value. One of the [CIGI_TEXT_ORIENT_*_TO_*](#CIGI_TEXT_ORIENT_LEFT_TO_RIGHT) values.
## float getFontSize ( ) const

Returns the value of the **Font Size** parameter specified in the packet. Specifies the font size in terms of the vertical units defined by the symbols surface's 2D coordinate system.
### Return value

**Font Size** parameter value.
## const char * getText ( ) const

Returns the value of the **Octet** parameter specified in the packet.
### Return value

Octet parameter value.
> **Notice:** The maximum length of the string, including a terminating NULL, is 236 bytes.
