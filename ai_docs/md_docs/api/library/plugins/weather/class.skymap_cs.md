# Unigine::Plugins::Weather::SkyMap Class (CS)


This class is used to manage the Sun, the Moon, stars, day/night cycle for the IG.

> **Notice:** Weather plugin must be loaded.


The [**Celestial**](../../../../ig/weather/settings.md#celestial) property is used to set the Sun and the Moon.


## SkyMap Class

### Properties

## float StarfieldIntensity

The star field intensity value.
## float MoonIntensity

The moon intensity value.
## float SunIntensity

The Sun intensity value.
## float Timezone

The time zone used for the simulation in the UTC format. The Image Generator is configured to use Greenwhich time zone by default.
## bool ContinuousTime

The value indicating if the time of day is continuously updated by the image generator or remains static (time and date once set remain unchanged).
## 🔒︎ Node MoonNode

The node used to represent the Moon. Nodes for the Sun and the Moon can be [assigned via the UnigineEditor](../../../../ig/weather/settings.md#celestial).
## bool MoonEnabled

The value indicating if the Moon is rendered or not.
## 🔒︎ Node SunNode

The node used to represent the Sun. Nodes for the Sun and the Moon can be [assigned via the UnigineEditor](../../../../ig/weather/settings.md#celestial).
## bool SunEnabled

The value indicating if the Sun is rendered or not.
## bool StarfieldEnabled

The value indicating if the star field is rendered or not.
### Members

---

## void SetDateTime ( long time_posix , bool UTC = false )

Sets the time of the simulation.
### Arguments

- *long* **time_posix** - Time of the simulation to be set, number of seconds since January 1, 1970
- *bool* **UTC** - true to set this time as the Coordinated Universal Time (UTC +0), false � to set this time as the current local time.

## void SetDateTime ( int sec , int min , int hour , int day , int month , int year , bool UTC = false )

Sets the current date and time.
### Arguments

- *int* **sec** - An integer between 0 and 59 to be set as seconds value.
- *int* **min** - An integer between 0 and 59 to be set as minutes value.
- *int* **hour** - An integer between 0 (midnight) and 23 (11 p.m.) local time to be set as hours value.
- *int* **day** - An integer between 1 and 31 to be set as day value.
- *int* **month** - An integer between 1 and 12 to be set as month value.
- *int* **year** - An integer to be set as year value.
- *bool* **UTC** - true to set this time as the Coordinated Universal Time (UTC +0), false � to set this time as the current local time.

## long GetDateTime ( bool UTC = false )

Returns the current time of the simulation.
### Arguments

- *bool* **UTC** - true to return this time as the Coordinated Universal Time (UTC +0), false � to return this time as the current local time.

### Return value

Current time of the simulation, number of seconds since January 1, 1970
## void ForceRefresh ( )

Refreshes the sky map according to its current settings. This method should be called after setting sky map's parameters to apply them. [Sky map change callbacks](#addOnTimeChangedCallback_CallbackBase_ptr_void) are called on refresh.
## IntPtr AddOnTimeChangedCallback ( OnTimeChangedDelegate func )

Adds a callback function to be called when the sky map state changes. This function can be used to define specific actions to be performed when the sky map state changes. The signature of the callback function must be as follows:
```csharp
void(void)
```


You can set a callback function as follows:


```csharp
AddOnTimeChangedCallback(() => time_changed_callback_function_name());
```


**Example:** Setting a time changed callback on changing sky map state.


```csharp
class SomeClass
{
	/*...*/

	/// callback function to be called when a collision with the collision segment is detected
	private void time_changed_callback_function_name()
	{
		// insert your code handling collision event here
	}

	// ...

	// somewhere in code
	void Init()
	{
		// adding "my_callback" to be called on changing sky map state
		ig_manager.GetSkyMap().AddOnTimeChangedCallback(() => time_changed_callback_function_name());
	}

	/*...*/
}

```


### Arguments

- *OnTimeChangedDelegate* **func** - Callback function with the following signature: void OnTimeChangedDelegate(*void*)

### Return value

ID of the last added time changed callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnTimeChangedCallback_void_ptr_bool) this callback when necessary.
## bool RemoveOnTimeChangedCallback ( IntPtr id )

Removes the specified callback from the list of time changed callbacks.
### Arguments

- *IntPtr* **id** - Time changed callback ID obtained when [adding](#addOnTimeChangedCallback_CallbackBase_ptr_void) it.

### Return value

True if the time changed callback with the given ID was removed successfully; otherwise false.
## void ClearOnTimeChangedCallbacks ( )

Clears all [added](#addOnTimeChangedCallback_CallbackBase_ptr_void) time changed callbacks.
