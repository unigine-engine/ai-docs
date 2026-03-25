# Unigine::InputEventJoyButton Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls joystick button event information.


### See Also


- C++ sample
- C# Component sample


## InputEventJoyButton Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **ACTION_DOWN** = 0 | Button state is "pressed". |
| **ACTION_UP** = 1 | Button state is "released". |

### Members

---

## InputEventJoyButton ( )

Default constructor.
## InputEventJoyButton ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Joystick button input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventJoyButton ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , InputEventJoyButton::ACTION action , int connection_id , int button )

Joystick button input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *[InputEventJoyButton::ACTION](../../../api/library/controls/class.inputeventjoybutton_cpp.md#ACTION)* **action** - Type of the joystick button input event, one of the [ACTION_*](#ACTION_DOWN) values.
- *int* **connection_id** - Connection identifier.
- *int* **button** - Joystick button index.

## void setAction ( InputEventJoyButton::ACTION action )

Sets the type of the joystick button input event.
### Arguments

- *[InputEventJoyButton::ACTION](../../../api/library/controls/class.inputeventjoybutton_cpp.md#ACTION)* **action** - Type of the joystick button input event, one of the [ACTION_*](#ACTION_DOWN) values.

## InputEventJoyButton::ACTION getAction ( ) const

Returns the type of the joystick button input event.
### Return value

Type of the joystick button input event, one of the [ACTION_*](#ACTION_DOWN) values.
## void setConnectionID ( int id )

Sets the connection identifier.
### Arguments

- *int* **id** - Connection identifier.

## int getConnectionID ( ) const

Returns the current connection identifier.
### Return value

Connection identifier.
## void setButton ( int button )

Sets the joystick button index.
### Arguments

- *int* **button** - Joystick button index.

## int getButton ( ) const

Returns the joystick button index.
### Return value

Joystick button index.
