# Unigine::Random Class (CPP)

**Header:** #include <UnigineMathLibRandom.h>


This class implements pseudo-random number generation functions for various purposes. A 32-bit seed value is used, upon creation an instance is initialized with a seed value equal to the current time. In case two instances of *Random* are created with the same seed, and the same sequence of method calls is made for each, they will generate and return identical sequences of numbers. Therefore, if you have a component using its own internal *Random* member (e.g., to move a node in a random direction, see code below), the sequence of numbers generated for different nodes having this component assigned will likely be the same resulting in all nodes moving together in one direction.


![](balls_sync.gif)


<details>
<summary>Component using Math::Random class (same values) | Close</summary>

```cpp
#pragma once

#include <UnigineComponentSystem.h>
#include <UnigineMathLibRandom.h>
class RandomMovement : public Unigine::ComponentBase
{
public:
	COMPONENT_DEFINE(RandomMovement, Unigine::ComponentBase);
	COMPONENT_UPDATE(update);

	PROP_PARAM(Float, speed, 2.0f, "Speed");	// movement speed
private:
	Unigine::Math::Random rnd;	// internal random generator
	void update();
};

```


```cpp
#include "RandomMovement.h"
#include <UnigineGame.h>
using namespace Unigine;
using namespace Math;

REGISTER_COMPONENT(RandomMovement);

void RandomMovement::update()
{
	// making a direction vector using random values (vary for different nodes having the component assigned)
	vec3 dir = vec3(rnd.getInt(-1, 2), rnd.getInt(-1, 2), 0);
	vec3 p0 = node->getWorldPosition();
	vec3 p1 = p0 + dir * speed * Game::getIFps();

	// moving the node along the obtained direction vector with the given speed
	node->setWorldPosition(p1);
}

```

</details>


To avoid such behavior you can use similar methods of the *[Game](../../../api/library/engine/class.game_cpp.md)* class as in this case there is a single *Random* generator (internal *Game* class member) and each call to *[Game::getRandom*()](../../../api/library/engine/class.game_cpp.md#getRandom_uint)* method returns the next element of the pseudo-random number sequence.


![](balls_async.gif)


<details>
<summary>Component using Game class randomizer (different values) | Close</summary>

```cpp
#pragma once

#include <UnigineComponentSystem.h>
#include <UnigineGame.h>
class RandomMovement : public Unigine::ComponentBase
{
public:
	COMPONENT_DEFINE(RandomMovement, Unigine::ComponentBase);
	COMPONENT_UPDATE(update);

	PROP_PARAM(Float, speed, 2.0f, "Speed");	// movement speed
private:
	void update();
};

```


```cpp
#include "RandomMovement.h"
#include <UnigineGame.h>

using namespace Unigine;
using namespace Math;

REGISTER_COMPONENT(RandomMovement);

void RandomMovement::update()
{
	// making a direction vector using random values (vary for different nodes having the component assigned)
	vec3 dir = vec3(Game::getRandomInt(-1, 2), Game::getRandomInt(-1, 2), 0);
	vec3 p0 = node->getWorldPosition();
	vec3 p1 = p0 + dir * speed * Game::getIFps();

	// moving the node along the obtained direction vector with the given speed
	node->setWorldPosition(p1);
}

```

</details>


## Random Class

### Members

---

## static RandomPtr create ( )

Constructor. Initializes the random generator.
## static RandomPtr create ( unsigned int seed_ )

Constructor. Initializes the random generator with a given seed.
### Arguments

- *unsigned int* **seed_** - Seed.

## Random & getRandom ( )

Returns static thread-safe random object.
### Return value

Thread-safe random object.
## void setSeed ( unsigned int seed_ ) const

Sets the new seed.
### Arguments

- *unsigned int* **seed_** - New seed.

## unsigned int getSeed ( ) const

Returns the active seed.
### Return value

Active seed.
## unsigned int get ( ) const

Returns the random unsigned integer.
### Return value

Random unsigned integer.
## int getInt ( )

Returns the random integer.
### Return value

Random integer.
## unsigned long long getULong ( )

Returns the random unsigned long integer (64 bits).
### Return value

Random unsigned long integer (64 bits).
## long long getLong ( )

Returns the random long integer (64 bits).
### Return value

Random long integer (64 bits).
## float getFloat ( )

Returns the random float.
### Return value

Random float.
## double getDouble ( )

Returns the random double.
### Return value

Random double.
## int getInt ( int from , int to ) const

Returns the random integer in the specified range **[from,to)**.
### Arguments

- *int* **from** - Start of the range.
- *int* **to** - End of the range.

### Return value

Random integer.
## float getFloat ( float from , float to ) const

Returns the random float in the specified range **[from,to)**.
### Arguments

- *float* **from** - Start of the range.
- *float* **to** - End of the range.

### Return value

Random float.
## double getDouble ( double from , double to ) const

Returns the random double in the specified range **[from,to)**.
### Arguments

- *double* **from** - Start of the range.
- *double* **to** - End of the range.

### Return value

Random double.
## vec4 getColor ( ) const

Returns the random color.
### Return value

Random color.
## vec3 getDirection ( ) const

Returns the random direction vector (normalized).
### Return value

Random direction vector.
