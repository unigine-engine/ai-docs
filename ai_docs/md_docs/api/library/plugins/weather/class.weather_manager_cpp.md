# Unigine::Plugins::Weather::Manager Class (CPP)

**Header:** #include <plugins/Unigine/Weather/UnigineWeather.h>


This class represents the Weather Manager interface.

> **Notice:** Weather plugin must be loaded.


## Weather::Manager Class

### Members

---

## void saveState ( const Ptr < Stream > & blob ) const

Saves the state of the Weather Manager into a binary stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **blob** - The stream to save the weather data.

## void restoreState ( const Ptr < Stream > & blob )

Restores the state of the Weather Manager from the binary stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **blob** - The stream that stores the weather data.
