# Unigine::Plugins::IG::SymbolText Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


## SymbolText Class

### Enums

## Orientation

| Name | Description |
|---|---|
| **LEFT_TO_RIGHT** = 0 | Horizontal text orientation from left to right. |
| **RIGHT_TO_LEFT** = 2 | Horizontal text orientation from right to left. |
| **TOP_TO_BOTTOM** = 1 | Vertical text orientation from top to bottom. |
| **BOTTOM_TO_TOP** = 3 | Vertical text orientation from bottom to top. |

## AlignHorizontal

| Name | Description |
|---|---|
| **LEFT** = 0 | Align text to the left. |
| **CENTER** = 1 | Align text to the center. |
| **RIGHT** = 2 | Align text to the right. |

## AlignVertical

| Name | Description |
|---|---|
| **TOP** = 0 | Align text to the top. |
| **CENTER** = 1 | Align text to the center. |
| **BOTTOM** = 2 | Align text to bottom. |

### Members

---

## void setText ( const char * text )

Sets the text to be displayed.
### Arguments

- *const char ** **text** - Text to be displayed.

## void setFont ( const String & path )

Sets the font stored in the specified file.
### Arguments

- *const [String](../../../../../api/library/common/class.string_cpp.md) &* **path** - Path to a font file.

## void setFontSize ( float font_size )

Sets the font size.
### Arguments

- *float* **font_size** - Font size.

## void setAlign ( SymbolText.AlignHorizontal align_horizontal , SymbolText.AlignVertical align_vertical )

Sets horizontal and vertical alignment for the text to be displayed.
### Arguments

- *[SymbolText.AlignHorizontal](../../../../../api/library/plugins/ig/api/class.symboltext_cpp.md#AlignHorizontal)* **align_horizontal** - Horizontal alignment for the text.
- *[SymbolText.AlignVertical](../../../../../api/library/plugins/ig/api/class.symboltext_cpp.md#AlignVertical)* **align_vertical** - Vertical alignment for the text.

## void setOrientation ( SymbolText.Orientation orientation )

Sets orientation for the text to be displayed (horizontal: *left-to-right / right-to-left* or vertical: *bottom-to-top / top-to-bottom*).
### Arguments

- *[SymbolText.Orientation](../../../../../api/library/plugins/ig/api/class.symboltext_cpp.md#Orientation)* **orientation** - Text orientation to be set.
