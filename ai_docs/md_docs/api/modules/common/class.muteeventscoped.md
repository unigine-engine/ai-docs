# Utils::MuteEventScoped Class


MuteEventScoped is a **RAII** helper that temporarily disables an event for the duration of a scope. This is useful when you need to modify a value that would normally trigger an event callback, but you want to prevent the callback from firing during that specific modification.


Common use cases include updating a widget value programmatically without triggering its "changed" callback, batch-updating multiple values where intermediate callbacks would cause issues, and preventing recursive callback chains when modifying state inside a callback.


Usage example:


```cpp
// Using the convenience macro
MUTE_EVENT(my_widget->getEventChanged());
my_widget->setValue(new_value); // callback won't fire

// Or using the class directly
{
    Utils::MuteEventScoped mute(my_widget->getEventChanged());
    my_widget->setValue(new_value); // callback won't fire
} // event is re-enabled when mute goes out of scope

```
