# Event Handling Callbacks (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Callback is a function wrapper representing a pointer to static and member functions which are expected to be executed with specified parameters at a certain moment. A callback can be passed as an argument to a function.


In UnigineScript callbacks are represented by function identifiers obtained using the *[**functionid()**](../../../api/library/common/class.system_usc.md#functionid_variable_int)* function:


```cpp
void callback_function(Node node) {
	/* .. */
}
..
int callback = functionid(callback_function);

```


### Usage Example


The following section contains the complete source code of a simple callback usage example.


<details>
<summary>Simple callback usage example | Close</summary>

**world_script.usc**


```cpp
#include <core/unigine.h>
// This file is in UnigineScript language.
// World script, it takes effect only when the world is loaded.

int init() {

	Player player = new PlayerSpectator();
	player.setPosition(Vec3(0.0f,3.401f,1.5f));
	player.setDirection(Vec3(0.0f,-1.0f,-0.4f));
	engine.game.setPlayer(player);

	int callback_id = functionid(callback_function);

	call(callback_id);

	return 1;
}

void callback_function() {
	log.message("Callback has been fired\n");
}

// start of the main loop
int update() {

	return 1;
}

int postUpdate() {

	return 1;
}

int updatePhysics() {

	return 1;
}
// end of the main loop

int shutdown() {

	return 1;
}


```

</details>
