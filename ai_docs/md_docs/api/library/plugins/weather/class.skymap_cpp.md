# Unigine::Plugins::Weather::SkyMap Class (CPP)

**Header:** #include <plugins/Unigine/Weather/UnigineWeather.h>


This class is used to manage the Sun, the Moon, stars, day/night cycle for the IG.

> **Notice:** Weather plugin must be loaded.


The [**Celestial**](../../../../ig/weather/settings.md#celestial) property is used to set the Sun and the Moon.


## SkyMap Class

### Members

---

## void setTimezone ( float timezone )

Sets the time zone to be used for the simulation in the UTC format. The image generator is configured to use Greenwhich time zone by default.
### Arguments

- *float* **timezone** - UTC time zone value.

## float getTimezone ( ) const

Returns the time zone currently used for the simulation in the UTC format.
### Return value

UTC time zone value.
## void setDateTime ( long long time_posix , bool UTC = false )

Sets the time of the simulation.
### Arguments

- *long long* **time_posix** - Time of the simulation to be set, number of seconds since January 1, 1970
- *bool* **UTC** - true to set this time as the Coordinated Universal Time (UTC +0), false — to set this time as the current local time.

## void setDateTime ( int sec , int min , int hour , int day , int month , int year , bool UTC = false )

Sets the current date and time.
### Arguments

- *int* **sec** - An integer between 0 and 59 to be set as seconds value.
- *int* **min** - An integer between 0 and 59 to be set as minutes value.
- *int* **hour** - An integer between 0 (midnight) and 23 (11 p.m.) local time to be set as hours value.
- *int* **day** - An integer between 1 and 31 to be set as day value.
- *int* **month** - An integer between 1 and 12 to be set as month value.
- *int* **year** - An integer to be set as year value.
- *bool* **UTC** - true to set this time as the Coordinated Universal Time (UTC +0), false — to set this time as the current local time.

## long long getDateTime ( bool UTC = false ) const

Returns the current time of the simulation.
### Arguments

- *bool* **UTC** - true to return this time as the Coordinated Universal Time (UTC +0), false — to return this time as the current local time.

### Return value

Current time of the simulation, number of seconds since January 1, 1970
## void setContinuousTime ( bool enable )

Enables or disables continuous time of day. When enabled the image generator will continuously update the time of day. Otherwise the time and date once set will remain unchanged.
### Arguments

- *bool* **enable** - true to enable continuous time of day; false - to use static time.

## bool isContinuousTime ( ) const

Returns a value indicating if the time of day is continuously updated by the image generator ore remains static.
### Return value

true if the time of day is continuously updated by the image generator; otherwise, false.
## void setStarfieldIntensity ( float intensity )

Sets the intensity of the star field.
### Arguments

- *float* **intensity** - Star field intensity value to be set, within the **[0.0f, 1.0f]** range. The *higher* the value, the brighter the stars will be.

## float getStarfieldIntensity ( ) const

Returns the current star field intensity value.
### Return value

Current star field intensity value, within the **[0.0f, 1.0f]** range. The *higher* the value, the brighter the stars will be.
## void setSunEnabled ( bool enable )

Sets a value indicating if the Sun is to be rendered or not.
### Arguments

- *bool* **enable** - true to enable rendering of the Sun; false - to disable it.

## bool isSunEnabled ( ) const

Returns a value indicating if the Sun is rendered or not.
### Return value

true if the Sun is rendered; otherwise, false.
## void setSunIntensity ( float intensity )

Sets the intensity of the sun.
### Arguments

- *float* **intensity** - Sun intensity value within the **[0.0f, 1.0f]** range. The *higher* the value, the brighter the sun is.

## float getSunIntensity ( ) const

Returns the current sun intensity value.
### Return value

Sun intensity value within the **[0.0f, 1.0f]** range. The *higher* the value, the brighter the sun is.
## Ptr < Node > getSunNode ( ) const

Returns a pointer to the node currently used to represent the Sun. Nodes for the Sun and the Moon can be [assigned via the UnigineEditor](../../../../ig/weather/settings.md#celestial).
### Return value

Pointer to the node currently used to represent the Sun.
## void setMoonEnabled ( bool enable )

Sets a value indicating if the Moon is to be rendered or not.
### Arguments

- *bool* **enable** - true to enable rendering of the Moon; false - to disable it.

## bool isMoonEnabled ( ) const

Returns a value indicating if the Moon is rendered or not.
### Return value

true if the Moon is rendered; otherwise, false.
## void setMoonIntensity ( float intensity )

Sets the intensity of the moon.
### Arguments

- *float* **intensity** - Moon intensity value within the **[0.0f, 1.0f]** range. The *higher* the value, the brighter the moon is.

## float getMoonIntensity ( ) const

Returns the current moon intensity value.
### Return value

Moon intensity value within the **[0.0f, 1.0f]** range. The *higher* the value, the brighter the moon is.
## Ptr < Node > getMoonNode ( ) const

Returns a pointer to the node currently used to represent the Moon. Nodes for the Sun and the Moon can be [assigned via the UnigineEditor](../../../../ig/weather/settings.md#celestial).
### Return value

Pointer to the node currently used to represent the Moon.
## void setStarfieldEnabled ( bool enable )

Sets a value indicating if the star field is to be rendered or not.
### Arguments

- *bool* **enable** - true to enable star field rendering; false - to disable it.

## bool isStarfieldEnabled ( ) const

Returns a value indicating if the star field is rendered or not.
### Return value

true if the star field is rendered; otherwise, false.
## void forceRefresh ( )

Refreshes the sky map according to its current settings. This method should be called after setting sky map's parameters to apply them. [Sky map change callbacks](#addOnTimeChangedCallback_CallbackBase_ptr_void) are called on refresh.
## void * addOnTimeChangedCallback ( Unigine:: CallbackBase * func )

Adds a callback function to be called when the sky map state changes. This function can be used to define specific actions to be performed when the sky map state changes. The signature of the callback function must be as follows:
```cpp
void(void);
```


You can set a callback function as follows:


```cpp
addOnTimeChangedCallback(MakeCallback(time_changed_callback_function_name));
```


**Example:** Setting a time changed callback on changing sky map state.


```cpp
/// callback function to be called when sky map state changes
void SomeClass::my_callback()
{
	// pointer to your sun node (don't forget to initialize it)
	NodePtr sun;

	// calculating zenith angle to determine if it is night time or not
	float zenith = getAngle(vec3_up, sun->getDirection(AXIS_Z));
	bool night = zenith > sun_zenit_threshold;

	// switching lights
	for (auto & it : lights)
	{
		it.data.setEnable(night);
	}

	// switching the emission state for emissive materials
	for (auto & it : emissive_materials)
	{
		it->setState("emission",night);
	}
}

// ...
// somewhere in code
void SomeClass::init()
{
	// adding "my_callback" to be called on changing sky map state
	ig_manager->getSkyMap()->addOnTimeChangedCallback(this, Unigine::MakeCallback(this, &SomeClass::my_callback ) );
}

```


### Arguments

- *Unigine::[CallbackBase](../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **func** - Callback function.

### Return value

ID of the last added time changed callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnTimeChangedCallback_void_ptr_bool) this callback when necessary.
## bool removeOnTimeChangedCallback ( void * id )

Removes the specified callback from the list of time changed callbacks.
### Arguments

- *void ** **id** - Time changed callback ID obtained when [adding](#addOnTimeChangedCallback_CallbackBase_ptr_void) it.

### Return value

True if the time changed callback with the given ID was removed successfully; otherwise false.
## void clearOnTimeChangedCallbacks ( )

Clears all [added](#addOnTimeChangedCallback_CallbackBase_ptr_void) time changed callbacks.
