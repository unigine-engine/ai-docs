# Unigine::InputEventTextEditing Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class contains the IME (Input Method Editor) text editing event information: the in-progress composition (preedit) text together with the cursor position and the length of the selected portion inside it. The engine dispatches this event while the user is composing text via an IME (for example, CJK input methods).


IME composition must be enabled via the *[Input](../../../api/library/controls/class.input_cpp.md)* class (the **[isIMEEnabled()](../../../api/library/controls/class.input_cpp.md#isIMEEnabled_int)** property, disabled by default). Once the user commits the composition, a regular *[InputEventText](../../../api/library/controls/class.inputeventtext_cpp.md)* event with the final text arrives instead.


## InputEventTextEditing Class

### Members

## void setText ( const char * text )

Sets a new IME composition (preedit) text as a UTF-8 string that is not yet committed to the input target. The text is stored in a fixed 1024-byte buffer, longer input is truncated at a codepoint boundary.
### Arguments

- *const char ** **text** - The IME composition (preedit) text

## const char * getText () const

Returns the current IME composition (preedit) text as a UTF-8 string that is not yet committed to the input target. The text is stored in a fixed 1024-byte buffer, longer input is truncated at a codepoint boundary.
### Return value

Current IME composition (preedit) text
## void setCursor ( int cursor )

Sets a new position of the editing cursor within the composition text, measured in codepoints (characters), not bytes.
### Arguments

- *int* **cursor** - The cursor position within the composition text, in codepoints

## int getCursor () const

Returns the current position of the editing cursor within the composition text, measured in codepoints (characters), not bytes.
### Return value

Current cursor position within the composition text, in codepoints
## void setLength ( int length )

Sets a new number of codepoints in the selected (highlighted) portion of the composition text, starting at the cursor position. Zero means no selection.
### Arguments

- *int* **length** - The length of the selected portion of the composition text, in codepoints

## int getLength () const

Returns the current number of codepoints in the selected (highlighted) portion of the composition text, starting at the cursor position. Zero means no selection.
### Return value

Current length of the selected portion of the composition text, in codepoints
---

## InputEventTextEditing ( )

Default constructor. Creates an event of the *INPUT_EVENT_TEXT_EDITING* type with empty text, zero cursor position, and zero selection length.
## InputEventTextEditing ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Constructor. Creates an event of the *INPUT_EVENT_TEXT_EDITING* type with the given timestamp and mouse cursor position; the composition text is empty.
### Arguments

- *unsigned long long* **timestamp** - Event timestamp.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Mouse cursor position at the moment of the event.

## InputEventTextEditing ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , const char * text , int cursor , int length )

Constructor. Creates an event of the *INPUT_EVENT_TEXT_EDITING* type with the given parameters.
### Arguments

- *unsigned long long* **timestamp** - Event timestamp.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Mouse cursor position at the moment of the event.
- *const char ** **text** - IME composition (preedit) text as a UTF-8 string.
- *int* **cursor** - Position of the editing cursor within the composition text, in codepoints.
- *int* **length** - Number of codepoints in the selected portion of the composition text, starting at the cursor position.
