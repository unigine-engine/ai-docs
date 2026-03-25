# Unigine.Random Struct (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


This class implements pseudo-random number generation functions for various purposes. A 32-bit seed value is used, upon creation an instance is initialized with a seed value equal to the current time. In case two instances of *Random* are created with the same seed, and the same sequence of method calls is made for each, they will generate and return identical sequences of numbers. Therefore, if you have a component using its own internal *Random* member (e.g., to move a node in a random direction, see code below), the sequence of numbers generated for different nodes having this component assigned will likely be the same resulting in all nodes moving together in one direction.


![](../balls_sync.gif)


<details>
<summary>Component using Random struct (same values) | Close</summary>

```csharp
public partial class RandomMovement : Component
{
	public float speed = 2.0f;	// movement speed
	private Unigine.Random rnd;	// internal random generator

	private void Init()
	{
		// initializing a random generator
		rnd = new Unigine.Random();
	}

	private void Update()
	{
		// getting x and y random values (same for different nodes having the component assigned)
		float x = rnd.Int(-1, 2);
		float y = rnd.Int(-1, 2);
		vec3 dir = new vec3(x, y, 0);

		// moving the node along the obtained direction vector with the given speed
		node.WorldPosition = node.WorldPosition + dir * speed * Game.IFps;
	}
}

```

</details>


To avoid such behavior you can use similar methods of the *[Game](../../../../api/library/engine/class.game_cs.md)* class as in this case there is a single *Random* generator (internal *Game* class member) and each call to *[Game.GetRandom*()](../../../../api/library/engine/class.game_cs.md#getRandom_uint)* method returns the next element of the pseudo-random number sequence.


![](../balls_async.gif)


<details>
<summary>Component using Game class randomizer (different values) | Close</summary>

```csharp
public partial class RandomMovement : Component
{
	public float speed = 2.0f;	// movement speed

	private void Update()
	{
		// getting x and y random values (vary for different nodes having the component assigned)
		float x = Game.GetRandomInt(-1, 2);
		float y = Game.GetRandomInt(-1, 2);
		vec3 dir = new vec3(x, y, 0);

		// moving the node along the obtained direction vector with the given speed
		node.WorldPosition = node.WorldPosition + dir * speed * Game.IFps;
	}
}

```

</details>


## Random Class

### Members

---

## uint CalcRandomSeed ( )

Returns the randomizer seed.
### Return value

Resulting *uint* value.
## ref Random Get ( )

Returns a random value.
### Return value

Return value.
## uint UInt ( )

Returns a random *uint* value.
### Return value

Resulting *uint* value.
## int Int ( )

Returns a random *int* value.
### Return value

Resulting *int* value.
## ulong ULong ( )

Returns a random *ulong* value.
### Return value

Resulting *ulong* value.
## long Long ( )

Returns a random *long* value.
### Return value

Resulting *long* value.
## float Float ( )

Returns a random *float* value.
### Return value

Resulting *float* value.
## double Double ( )

Returns a random *double* value.
### Return value

Resulting *double* value.
## vec4 Color ( )

Returns a random color vector. **X, Y, Z** values of the color vector are random values, **W** value is equal to 1.0f.
### Return value

Random color vector.
## vec3 Direction ( )

Returns a random normalized direction vector.
### Return value

Random direction vector.
## int Int ( int from , int to )

Generate a random value in range **[to,from)**.
### Arguments

- *int* **from** - From value (beginning of the range).
- *int* **to** - To value (end of the range).

### Return value

Resulting *int* value.
## float Float ( float from , float to )

Generate a random value in range **[to,from)**.
### Arguments

- *float* **from** - From value (beginning of the range).
- *float* **to** - To value (end of the range).

### Return value

Resulting *float* value.
## double Double ( double from , double to )

Generate a random value in range **[to,from)**.
### Arguments

- *double* **from** - From value (beginning of the range).
- *double* **to** - To value (end of the range).

### Return value

Resulting *double* value.
## vec2 Vec2 ( vec2 from , vec2 to )

Generate a random value in range **[to,from)**. For vectors values are obtained per component.
### Arguments

- *vec2* **from** - From value (beginning of the range).
- *vec2* **to** - To value (end of the range).

### Return value

Return value.
## vec3 Vec3 ( vec3 from , vec3 to )

Generate a random value in range **[to,from)**. For vectors values are obtained per component.
### Arguments

- *vec3* **from** - From value (beginning of the range).
- *vec3* **to** - To value (end of the range).

### Return value

Return value.
## vec4 Vec4 ( vec4 from , vec4 to )

Generate a random value in range **[to,from)**. For vectors values are obtained per component.
### Arguments

- *vec4* **from** - From value (beginning of the range).
- *vec4* **to** - To value (end of the range).

### Return value

Return value.
