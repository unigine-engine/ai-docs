# Coroutines


The Engine processes your application logic frame by frame. Each frame runs through the [main loop](../../code/fundamentals/execution_sequence/main_loop.md) of your components (*update()*, *updatePhysics()* and so on).


However, if some logic needs to be executed across multiple frames (e.g., after 10 frames or after 5 seconds), you would normally need to add extra checks or rely on asynchronous methods. This complicates your code and results might look verbose.


Let's look at the simple example here. Suppose you want a barrel to explode 2 seconds after it was hit by a projectile. Your code might look like this:


```csharp
float timer = 0f;
bool isHit = false;

// Starting point
void OnHit()
{
	isHit = true;
	timer = 0f;
}

void Update()
{
	// Check every frame if the barrel was hit
	if (isHit)
	{
		// Accumulate time until 2 seconds pass
		timer += Game.IFps;
		if (timer >= 2f)
		{
			// And only then start explosion
			Explode();
			isHit = false;
		}
	}
}

void Explode()
{
	Log.MessageLine("Barrel Exploded!");
}

```


Coroutines provide a way to execute logic that extends beyond a single frame (their execution can be suspended either by the Engine or [manually](#coroutine_suspend), and then resumed). Conceptually, a coroutine is much like a regular function, but instead of returning void or a specific value, it returns an ***IEnumerator***. While you can technically call a coroutine like a normal function, it only becomes effective when invoked using *[StartCoroutine()](#corutine_start)*.


To function correctly, every coroutine requires at least one ***yield*** statement in its body. The ***yield*** keyword is what allows the coroutine to pause execution at a certain point and resume later, synchronizing naturally with the Engine's frame updates.


Using coroutines, the same logic would look like this:


```csharp
// Starting point
void OnHit()
{
	StartCoroutine(DelayedExplosion());
}

// Coroutine - sequence of steps
IEnumerator DelayedExplosion()
{
	yield return new WaitForSeconds(2f);
	Explode();
}

void Explode() {
	Log.MessageLine("Barrel Exploded!");
}

```


Instead of manually checking timers each frame, you can simply describe the delay using a coroutine. Here, the Engine handles the waiting part (2 seconds) automatically. You only define the sequence of actions.


Importantly, coroutines **are not threads**. They do not run in parallel, instead, they execute sequentially within the main thread.


![](coroutines_analogues.png)


To use coroutines properly in your applications, it is important to understand C# language features that make this behaviour possible.


## C# Prior Knowledge


### IEnumerator Interface


If you are familiar with C# language, you know that it provides a standard interface for collections: ***[IEnumerator](https://learn.microsoft.com/en-us/dotnet/api/system.collections.ienumerator?view=net-9.0)*** (declared in the ***System.Collections*** namespace). This interface specifies how elements in a collection are iterated. Its basic definition looks like this:


```csharp
public interface IEnumerator
{
	bool MoveNext();
	object Current { get; }
	void Reset();
}

```


For example, the string type in C# is a collection and implements this interface. That means you can iterate over its characters as follows:


```csharp
string s = "Hello, Unigine!";
IEnumerator letters = s.GetEnumerator();

while (letters.MoveNext())
{
	Log.MessageLine(letters.Current);
}

```


But ***IEnumerator*** is not limited to collections. You can also define it manually to represent logic that executes step by step. To do this, you use the ***yield return*** statement.


### yield return Statement


In C#, a *yield* statement is used inside an iterator to return elements one at a time, preserving the method's state, so iteration can resume from the same point on the next call.


- regular ***return*** means: "Here is the final value returned by this method."
- ***yield return*** means: "Here is the next value produced by this enumeration."


```csharp
public class MyClass
{
	public void Run()
	{
		Console.WriteLine("Begin");
		IEnumerator<int> e = Test();
		Console.WriteLine("Before while");
		while (e.MoveNext())
		{
			Console.WriteLine(e.Current);
		}
		Console.WriteLine("Done");
	}

	// Iterator method: execution is split across yields
	public IEnumerator<int> Test()
	{
		int value = 1;
		Console.WriteLine("Before yield 1");
		yield return value; // 1

		value = value + 2;
		Console.WriteLine("Before yield 2");
		yield return value; // 3

		value = value * 3;
		Console.WriteLine("Before yield 3");
		yield return value; // 9
	}
}

```


In this example, the method *Test()* is divided into three parts by *yield* statements. As a result, the *WriteLine()* method inside the loop is executed three times.


Notice that we are not directly "calling" *Test()*. Instead, we obtain an ***IEnumerator*** and iterate through it. Each time *MoveNext()* is called, execution continues until the next *yield*, which returns control back to the caller and produces a value. On every iteration, a new segment of code between two *yield* statements is executed.


> **Notice:** The local state of the **value** is preserved.


## Yield Instructions


A *yield* instruction is a supported value that can be returned from a ***yield return*** statement to tell the Engine when to continue the coroutine.


When a coroutine reaches *yield return*, execution is suspended and control is passed back to the Engine. The Engine then decides where and when to resume the coroutine, depending on the instruction that was returned.


> **Notice:** In the example above, the returned values were of type ***int***. However, in the context of UNIGINE coroutines, the list of supported yield instructions is limited. If an unsupported object is returned from *yield return*, the Engine **will throw an exception**.


All built-in *yield* instructions (except **null**) can be created in two different ways:


```csharp
yield return new WaitForSeconds(1f);          // Allocates a new object
yield return WaitForSeconds.Instance(1f);     // Reuses a preallocated object

```


- Using ***new*** creates a new instruction object, which results in extra allocations.
- Using ***Instance()*** reuses a shared *yield* instruction, avoiding additional allocations.


**Built-in Yield Instructions**


Below is the list of standard *yield* instructions and their behavior:


| null | Resumes the coroutine in the next *Update()* (next frame). |
|---|---|
| WaitForSeconds | Resumes the coroutine in *Update()* after the specified scaled game time (*[Game.Scale](../../api/library/engine/class.game_cpp.md#Scale)*), with the timer starting at the end of the current frame (the delay counts from frame end, not from the call moment). |
| WaitForSecondsRealtime | Same as **WaitForSeconds**, but waits using real time (unscaled). |
| WaitForFrames | Resumes the coroutine in *Update()* after the specified number of frames. - 0 continues in the **current frame** - 1 works like **null** |
| WaitUntil | Resumes the coroutine in *Update()* once the given condition evaluates to true ```csharp yield return new WaitUntil(() => node.WorldPosition.x > 10); ``` In this example, the coroutine continues when the node's X position becomes greater than 10. |
| WaitWhile | The opposite of WaitUntil: the coroutine waits while the condition is true and resumes in the *Update()* when it becomes false. ```csharp yield return new WaitWhile(() => node.WorldPosition.x > 10); ``` In this example, the coroutine continues once the node's X position is less than or equal to 10. |
| WaitPostUpdate | Resumes the coroutine in the next *PostUpdate()*. |
| WaitUpdatePhysics | Resumes the coroutine in the next *UpdatePhysics()*. |
| WaitSwap | Resumes the coroutine in the next *Swap()*. |
| Coroutine | A coroutine itself can also be used as a yield instruction. The current coroutine resumes only after the yielded coroutine has finished execution (see [Coordinating Coroutines](#coordinating)). <details> <summary>Usage Example</summary> ```csharp private IEnumerator Parent() { Console.WriteLine("Start parent"); yield return StartCoroutine(Child());	// wait until child finishes Console.WriteLine("Parent continues"); } private IEnumerator Child() { Console.WriteLine("Start child"); yield return new WaitForSeconds(1f); Console.WriteLine("Child finished"); } // The output is: // "Start parent" // "Start child" // 1 second later... // "Child finished" // "Parent continues" ``` </details> |
| IEnumerator | You can yield another coroutine directly by returning its ***IEnumerator***. This is equivalent to starting that coroutine and immediately yielding it. <details> <summary>Usage Example</summary> ```csharp private IEnumerator Animate() { yield return Rotate();                   // wait for Rotate to finish yield return StartCoroutine(Rotate());   // same effect } IEnumerator Rotate() { node.Rotate(0, 0, 45); yield return new WaitForSeconds(1f); } ``` </details> |
| IAsyncResult | This interface that allows custom classes to be used in yield return. It defines a single property (***bool IsFinished {get;}***) that must be implemented in user classes. The engine checks ***IsFinished*** on every update. While it is false, the coroutine is suspended; when it becomes true, the coroutine continues. <details> <summary>Usage Example</summary> ```csharp class ImageSaver : IAsyncResult { public bool IsFinished => _saved;    // Implement IAsyncResult private bool _saved = false; public void SaveImage(Image image) { // Run saving in a separate thread Task.Run(() => { image.Save("image.png"); _saved = true; }); } } private IEnumerator SaveImageAndPrint(Image image) { ImageSaver imageSaver = new ImageSaver(); imageSaver.SaveImage(image); // Coroutine waits here until IsFinished == true yield return imageSaver; Log.MessageLine("Image saved!"); } ``` </details> |
| AsyncResult<T> | Implements **IAsyncResult** and becomes finished once its ***Value*** is set. To wait for the value to be assigned, return the object from *yield return*. <details> <summary>Usage Example</summary> ```csharp AsyncResult<Image> AsyncTransferTextureToImage(Texture texture) { AsyncResult<Image> result = new(); Render.AsyncTransferTextureToImage(null, image => { // Set the value in the callback result.Value = image; }, texture); return result; } IEnumerator MyCoroutine() { AsyncResult<Image> result = AsyncTransferTextureToImage(texture); // Wait until result.Value is assigned yield return result; result.Value.Save("image.png"); Log.MessageLine("Image saved"); } ``` </details> |


## Managing Coroutines


In UNIGINE, coroutines are defined in the context of components:


- A coroutine is destroyed when its component (or the node the component is attached to) is deleted.
- A coroutine is paused when its component (or node) is disabled.


> **Notice:** Coroutine methods must always return the type ***IEnumerator***.


Here is an example of a simple coroutine that rotates a node by 45 degrees every 5 seconds:


```csharp
public partial class Animator : Component
{
	IEnumerator Rotate()
	{
		while (true)
		{
			node.Rotate(0, 0, 45);
			// Wait 5 seconds before the next rotation
			yield return new WaitForSeconds(5f);
		}
	}

	public void RunAnimation()
	{
		// Method to start a coroutine
		StartCoroutine(Rotate());
	}
}

```


### Starting a Coroutine


To start a coroutine use the *StartCoroutine()* method. There are several overloads of this method:


1. Strongly-typed overloads: These overloads are type-safe and checked at compile time.

  - ***StartCoroutine**(IEnumerator **method**)*
  - ***StartCoroutine**(IEnumerator **method**(int **arg1**, string **arg2**))*
2. String-based overloads: String-based coroutine calls lack compile-time safety and can lead to reflection-related performance and memory overhead.

  - ***StartCoroutine**(string **methodName**)*
  - ***StartCoroutine**(string **methodName**, object[] **args**)*


> **Notice:** Coroutines can only be started from the **main thread**! For example, you cannot start a coroutine from Component methods such as *UpdateSyncThread()* or *UpdateAsyncThread()*.


### Stopping a Coroutine


Stopping a coroutine means it is terminated completely and will not continue execution. A coroutine can be stopped even before reaching the end of its function:


```csharp
public IEnumerator Spam()
{
	yield return new WaitForSeconds(1f);
	node.DeleteLater();
	yield return new WaitForSeconds(1f);
	// Code below this yield will never run: the coroutine is stopped
	// once the node is deleted
}

```


Manual stop methods:


- ***StopCoroutine**(Coroutine **coroutine**)* *StartCoroutine()* returns a Coroutine object, which can be used later to stop execution. ```csharp Coroutine coroutine = StartCoroutine(Spam()); StopCoroutine(coroutine); Component.StopCoroutine(coroutine); ``` This method is static, this can be useful when a coroutine reference is passed outside and must be stopped elsewhere.
- ***Stop**()* You can stop the coroutine directly by calling *Stop()* on the *Coroutine* object. ```csharp Coroutine coroutine = StartCoroutine(Spam()); coroutine.Stop(); ``` This works exactly the same as *StopCoroutine()*.
- ***StopCoroutines**(string **methodName**)* Stops all coroutines that were started by method name. If multiple coroutines were launched with the same name, all of them are stopped. ```csharp StartCoroutine("Spam"); StartCoroutine("Spam"); StopCoroutines("Spam"); // Stops both ``` > **Notice:** This works only for coroutines started by name. > > > ```csharp > StartCoroutine(Spam()); > StopCoroutines("Spam"); // No effect > > ```
- ***StopAllCoroutines**()* Stops all coroutines running for the current component.


### Pausing and Resuming a Coroutine


A coroutine can be paused (disabled). While paused, it does not execute until it is enabled again.


The execution state is controlled by the ***Enabled*** property:


```csharp
Coroutine coroutine = StartCoroutine(Spam());
coroutine.Enabled = false;  // Pause the coroutine
coroutine.Enabled = true;   // Resume the coroutine

```


If the node or component is disabled, all its coroutines are automatically paused, even their *Enabled* property is set to true.


It is still possible to call *StartCoroutine()* when the node or component is disabled. In this case, the coroutine is created, **but will not begin execution** until the node (or component) is enabled again.


The execution phase is preserved. If you start a coroutine during *PostUpdate()* while the node is disabled, it will begin at the next *PostUpdate()* once the node is enabled again.


### Coordinating Coroutines


Coroutines can start and manage other coroutines. This makes it possible to either run them in parallel with the current coroutine or sequentially, waiting until a nested coroutine has completed.


#### Running Coroutines in Parallel


You can start a coroutine from inside another coroutine using *StartCoroutine()*. In this case, the new coroutine will run independently of the current one, and both will progress frame by frame.


```csharp
private IEnumerator Animate()
{
	StartCoroutine(Rotate());
	StartCoroutine(Move());
	Log.MessageLine("Finished!");
}

```


*Rotate()* and *Move()* run in parallel with their logic progressing over time. The message will be printed immediately in this frame.


#### Running Coroutines Sequentially


You can also wait for nested coroutines to finish before continuing execution. This is done with *yield return StartCoroutine()*. In this case, the current coroutine is suspended until the nested coroutine completes.


```csharp
private IEnumerator Animate()
{
	yield return StartCoroutine(Rotate());
	yield return StartCoroutine(Move());
	Log.MessageLine("Finished!");
}

```


In this example, *Animate()* pauses while *Rotate()* runs. Once *Rotate()* finishes, *Move()* starts. After *Move()* also completes, the coroutine resumes and prints "Finished!" to the console.


Or you can start several coroutines in parallel, store their references, and then wait for each one in turn:


```csharp
private IEnumerator Animate()
{
	Coroutine c1 = StartCoroutine(Rotate());
	Coroutine c2 = StartCoroutine(Move());
	yield return c1;
	yield return c2;
	Log.MessageLine("Finished!");
}

```


In this case, *Rotate()* and *Move()* run in parallel. The coroutine *Animate()* first waits for *Rotate()* to finish, then waits for *Move()*. Only after both coroutines complete is the log message printed to the console.


#### Deferred Waiting


It is not required to immediately yield a coroutine right after starting it. You can store a reference to it and decide later whether to wait for its completion.


```csharp
private IEnumerator Animate()
{
	Coroutine rotateCoroutine = StartCoroutine(Rotate());
	StartCoroutine(Move());
	yield return rotateCoroutine;
	Log.MessageLine("Finished!");
}

```


Here *Move()* and *Rotate()* are running in parallel. *Animate()* resumes only when *Rotate()* completes - even if *Move()* is still running.


#### Single-Wait Restriction


A coroutine can be awaited by only one other coroutine at a time.


```csharp
void Test()
{
	var co = StartCoroutine(Wait5Sec());

	StartCoroutine(WaitCoroutine(co));
	StartCoroutine(WaitCoroutine(co)); // second waiter leads to warning and won't work
}

IEnumerator Wait5Sec()
{
	yield return new WaitForSeconds(5);
}

IEnumerator WaitCoroutine(Coroutine coroutine)
{
	yield return coroutine; // only one coroutine may do this
}

```


If multiple coroutines try to *yield return* the same Coroutine handle, only the first wait is valid. Subsequent waits emit a warning and won't work:


```text
Coroutine "Coroutines::WaitCoroutine" cannot wait for coroutine "Coroutines::Wait5Sec".
Another coroutine "Coroutines::WaitCoroutine" is already waiting for coroutine "Coroutines::Wait5Sec".

```


However, you can use ***IAsyncResult*** or the generic ***AsyncResult<T>*** to make multiple coroutines wait for the same result or event.


Unlike a Coroutine handle, an ***AsyncResult<T>*** can be awaited by any number of coroutines. When the result is set, all waiting coroutines resume execution.


```csharp
void Test()
{
	AsyncResult<int> result = new();
	StartCoroutine(DoJob(result));
	StartCoroutine(WaitAndPrint(result));
	StartCoroutine(WaitAndPrint(result));
}

IEnumerator DoJob(AsyncResult<int> result)
{
	yield return new WaitForSeconds(5);
	result.Value = 123; // setting the result completes the AsyncResult
}

IEnumerator WaitAndPrint(AsyncResult<int> result)
{
	yield return result; // wait until Value is assigned
	Log.MessageLine($"result = {result.Value}");
}

```


### Returning Values from Coroutines


The *yield return* statement only works with recognized yield instructions. If you need to pass results from coroutine, the recommended way is to use ***AsyncResult<T>***.


```csharp
IEnumerator Test()
{
	AsyncResult<int> result = new();
	StartCoroutine(DoJob(result));
	yield return result;
	Log.MessageLine($"result = {result.Value}");
}

IEnumerator DoJob(AsyncResult<int> result)
{
	// Simulate some asynchronous work
	yield return new WaitForSeconds(1);
	result.Value = 123;
}

```


## Engine Functions Overloads


Some engine functions have overloads that return **yield** instructions, allowing them to be awaited in coroutines.


- *[Render.AsyncTransferTextureToImage()](../../api/library/rendering/class.render_cpp.md#asyncTransferTextureToImage_TextureToImageTransfered_TextureToImageTransfered_Texture_void)* ```csharp IEnumerator SaveTextureToImageFile(Texture texture) { var result = Render.AsyncTransferTextureToImage(texture); yield return result; // wait until transfer is complete result.Value.Save("image.png"); } ```
