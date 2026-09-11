# Unigine::InputEventTextEditing Class (CS)

**Inherits from:** InputEvent


This class contains the IME (Input Method Editor) text editing event information: the in-progress composition (preedit) text together with the cursor position and the length of the selected portion inside it. The engine dispatches this event while the user is composing text via an IME (for example, CJK input methods).


IME composition must be enabled via the *[Input](../../../api/library/controls/class.input_cs.md)* class (the **[IMEEnabled](../../../api/library/controls/class.input_cs.md#isIMEEnabled_int)** property, disabled by default). Once the user commits the composition, a regular *[InputEventText](../../../api/library/controls/class.inputeventtext_cs.md)* event with the final text arrives instead.


## InputEventTextEditing Class

### Properties

## string Text

The IME composition (preedit) text as a UTF-8 string that is not yet committed to the input target. The text is stored in a fixed 1024-byte buffer, longer input is truncated at a codepoint boundary.
## int Cursor

The position of the editing cursor within the composition text, measured in codepoints (characters), not bytes.
## int Length

The number of codepoints in the selected (highlighted) portion of the composition text, starting at the cursor position. Zero means no selection.
### Members

---

## InputEventTextEditing ( )

Default constructor. Creates an event of the *INPUT_EVENT_TEXT_EDITING* type with empty text, zero cursor position, and zero selection length.
## InputEventTextEditing ( ulong timestamp , ivec2 mouse_pos )

Constructor. Creates an event of the *INPUT_EVENT_TEXT_EDITING* type with the given timestamp and mouse cursor position; the composition text is empty.
### Arguments

- *ulong* **timestamp** - Event timestamp.
- *ivec2* **mouse_pos** - Mouse cursor position at the moment of the event.

## InputEventTextEditing ( ulong timestamp , ivec2 mouse_pos , string text , int cursor , int length )

Constructor. Creates an event of the *INPUT_EVENT_TEXT_EDITING* type with the given parameters.
### Arguments

- *ulong* **timestamp** - Event timestamp.
- *ivec2* **mouse_pos** - Mouse cursor position at the moment of the event.
- *string* **text** - IME composition (preedit) text as a UTF-8 string.
- *int* **cursor** - Position of the editing cursor within the composition text, in codepoints.
- *int* **length** - Number of codepoints in the selected portion of the composition text, starting at the cursor position.
