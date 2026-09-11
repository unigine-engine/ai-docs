# C# Interfaces and Abstract Classes


## Dependency Management in C# Classes


Projects where classes create everything they need by themselves often have common architectural problems, because they handle their own dependencies directly. For example, a class might internally create services like a custom player HUD or input settings. This causes several issues:


- **Tight Coupling:** Using specific implementations directly within a class creates tight connections between the class and those implementations. Modifying or replacing these dependencies, such as changing an input handler from keyboard to gamepad, inevitably requires changing the dependent class itself, violating the open-closed principle.
- **Poor Maintainability:** Dependency setup logic often becomes duplicated across the application. If multiple components individually configure the same dependency, it becomes difficult to manage and understand the configurations, and thus harder to maintain.
- **Difficulty in Unit Testing:** Hard-coded dependencies severely limit testability. For example, when a class internally creates a complex dependency like an audio manager, it becomes difficult to replace it with a mock during testing, which makes unit tests less reliable.
- **Reduced Reusability and Modularity:** Components tied to certain dependencies become less flexible. This makes it harder to reuse them in different situations. If a component is directly linked to a specific manager or subsystem, you can't easily move it or use it somewhere else.


## Dependency Injection


**Dependency Injection (DI)** is a way to write code that's flexible and easy to manage. Rather than creating or directly referencing its dependencies, a class receives them from **outside**.


Classes depend on an **abstraction** (an interface or abstract class) rather than a concrete implementation. This approach adheres to the **Dependency Inversion Principle (DIP)**, which states that high-level modules should not depend on low-level modules; both should depend on abstractions. Moreover, abstractions themselves should not depend on details � the details should depend on the abstraction.


By following **DIP**, you reduce direct coupling and make it easier to replace components without affecting higher-level logic.


![Abstraction diagram](abstraction_diagram.png)


To address issues above and build more flexible, testable, and maintainable systems in UNIGINE, ***you can use components that implement interfaces or inherit from abstract classes***. [C# Component System](../../principles/component_system/component_system_cs/index.md) supports this approach and makes it easier to program to abstractions rather than concrete implementations and decouple components from specific dependencies.


## Interfaces


**Interfaces** are a mechanism for defining contracts that classes can implement. Any class that implements an interface agrees to provide that functionality.


Using interfaces for DI is a common pattern to achieve maximum decoupling. The approach to working with interfaces in UNIGINE can be summarized as follows:


1. **Define an Interface.** Identify the behavior or functionality that needs to be provided, and define an interface declaring the required methods. This interface serves as a contract that any specific component must fulfill. ```csharp public interface IShootable { public void Shoot(); } ``` > **Notice:** You can create an empty `*.cs` file right in the *Asset Browser* window. ![Empty *.cs file creation](cs_file_creation.png)
2. **Implement the Interface in a Component.** Create one or more components that implement this interface. They will contain the actual code to perform the work, but from the outside they will be accessed via the interface. You can have multiple implementations of the same interface coexisting, which is a powerful way to swap behaviors. The component that implements the interface is called a *service*. ```csharp public class WizardStaff : Component, IShootable { public void Shoot() { Log.MessageLine("The wizard's staff shot a fireball."); } } public class MagicWand : Component, IShootable { public void Shoot() { Log.MessageLine("The magic wand shot an electric zap."); } } public class Bow : Component, IShootable { public void Shoot() { Log.MessageLine("The bow shot an arrow."); } } ``` ![Nodes with components](nodes_with_icomponents.png)
3. **Depend on the Interface in the Client.** Any component that needs to use the special behavior should not directly instantiate concrete service class. Instead, it should rely on a reference to an interface type. The component that depends on the service is called a *client*. ```csharp public class Player : Component { [ShowInEditor] IShootable mainPlayerWeapon = null; [ShowInEditor] IShootable sparePlayerWeapon = null; void Update() { if (Input.IsMouseButtonDown(Input.MOUSE_BUTTON.LEFT)) { mainPlayerWeapon?.Shoot(); } if (Input.IsMouseButtonDown(Input.MOUSE_BUTTON.RIGHT)) { sparePlayerWeapon?.Shoot(); } } } ```
4. **Inject the Concrete Implementation.** This step is where the wiring happens. The interface reference in the client must be assigned a concrete object instance that implements the interface. There are a couple of ways to do this using UNIGINE features:

  - **Via the Editor.** In UNIGINE you can expose the interface field in the component parameters. By default, parameters are displayed or hidden in the UI in accordance with access modifiers: public - displayed, otherwise - hidden. But you can show a private or protected one by specifying the corresponding visibility attribute **ShowInEditor** as shown above in the code sample. Then, you simply assign a node with an assigned component that implements your specific interface. ![Using interfaces in Editor](attaching_an_interface.gif)
  - **Via the API.** Or you can locate the interface using the engine API. ```csharp // Getting IShootable var newWeapon = obj.GetComponent<IShootable>(); // If newWeapon is not null, it will be new main player weapon mainPlayerWeapon = newWeapon ?? mainPlayerWeapon; ``` A common pattern is calling *[GetComponent<>()](../../api/library/common/logic/component_system/cs/class.component.md#getComponent_Node_bool_T)* method in the client's code. The engine will search for a component that implements the *IShootable* interface, as in our example, and return a reference to it. The key point is that the client code does not instantiate the service directly - instead, it receives a reference or obtains it from the environment.


## Abstract Classes


Interfaces aren't the only way to invert dependencies � abstract classes can also serve as the abstraction layer between a client and the concrete implementation. The workflow for using abstract classes is very similar to the interface approach, with a few differences:


1. **Define an Abstract Base Class.** Create an abstract class that declares the necessary methods and optionally provides common functionality or default behavior shared across implementations. Since it's abstract, it can't be instantiated directly - instead, it serves as a template that concrete subclass components must follow. ```csharp using System.Collections; using System.Collections.Generic; using Unigine; [Component(PropertyGuid = "AUTOGENERATED_GUID")] public abstract class Toggleable : Component { [ShowInEditor] private bool isToggled = false; public bool Toggled { get => isToggled; set { if (value != isToggled) { bool ok = value ? On() : Off(); isToggled = isToggled ^ ok; } } } public bool Toggle() => isToggled = isToggled ^ (isToggled ? Off() : On()); protected abstract bool On(); protected abstract bool Off(); } ```
2. **Create Subclasses that Inherit from the Abstract Class.** Implement one or more classes that extend the abstract base class. Each subclass must implement the abstract methods, providing its own behavior. <details> <summary>Lamp.cs | Hide</summary> ```csharp using System.Collections; using System.Collections.Generic; using Unigine; [Component(PropertyGuid = "AUTOGENERATED_GUID")] public class Lamp : Toggleable { [ParameterColor] public vec4 emission_color = vec4.WHITE; protected override bool On() { Log.MessageLine("Lamp::On()"); return SetEmissionColor(emission_color); } protected override bool Off() { Log.MessageLine("Lamp::Off()"); return SetEmissionColor(vec4.ZERO); } private bool SetEmissionColor(vec4 emission_color) { Object obj = (Object)node; if (obj == null) return false; for (var surface = 0; surface < obj.NumSurfaces; surface += 1) obj.SetMaterialParameterFloat4("emission_color", emission_color, surface); return true; } private void Init() { SetEmissionColor(Toggled ? emission_color : vec4.ZERO); } } ``` </details> <details> <summary>Fan.cs | Hide</summary> ```csharp using System.Collections; using System.Collections.Generic; using Unigine; [Component(PropertyGuid = "AUTOGENERATED_GUID")] public class Fan : Toggleable { public float rotation_speed = 120; private float target_speed = 0; private float actual_speed = 0; protected override bool On() { Log.MessageLine("Fan::On()"); target_speed = rotation_speed; return true; } protected override bool Off() { Log.MessageLine("Fan::Off()"); target_speed = 0; return true; } private void Init() { target_speed = Toggled ? rotation_speed : 0; } private void Update() { actual_speed = MathLib.Lerp(actual_speed, target_speed, Game.IFps); node.Rotate(0, 0, actual_speed * Game.IFps); } } ``` </details> ![Nodes with abstract components](nodes_with_abstract_components.png)
3. **Inject a Concrete Subclass Instance into the Client Class.** Similar to the interface case, the client that needs the functionality holds a reference of the abstract base class type. Then, because of polymorphism, you can pass specific implementations of the abstract class to the client class in two following ways:

  - **Via the Editor.** Simply assign a node with the assigned component, that inherits your abstract base class in a node *Parameters* window: ![Using abstract classes in Editor](attaching_an_abstract.gif)
  - **Via the API.** Retrieving abstract base classes via the API works in a similar way as interfaces. ```csharp public class Toggler : Component { private void Update() { // Some logic for intersection with togglable object... if (obj) { var toggleable = obj.GetComponent<Toggleable>(); if (toggleable) { toggleable.Toggle(); } } } } ``` In this case, the client code requests a component that derives from an abstract class. The engine traverses the available components and returns one that matches the expected base type, such as *Toggleable*.


## Choosing the Right Abstraction Mechanism


Interfaces and abstract classes both define behaviour without binding to concrete implementations, but they differ in intent and capabilities:


- Interfaces are ideal for defining behaviour that can be implemented by any class, regardless of its place in the hierarchy. They also support multiple inheritance by allowing a class to implement multiple interfaces.
- Abstract classes are more appropriate when there is a need to share common implementation details, such as fields or methods across a group of related types.


It's important to use abstractions when they bring clear benefits - such as easier testing, multiple implementations, or shared logic. But if there's only one concrete use case and no need for reuse or substitution, keeping things simple is often the better choice.


## Using External Dependency Injection Frameworks


You can configure dependencies manually within the engine - using the editor and components to wire things together. This method gives full control over how and when dependencies are resolved. Alternatively, external *Dependency Injection* frameworks can be used. They allow you to:


- Use familiar tools from the **.NET** ecosystem.
- Simplify dependency management in larger projects.
- Access advanced **DI** features like scopes, signals, or event-based injection.


Below are examples of how to set up some popular external DI frameworks.


### Setting up Zenject in a UNIGINE Project


1. Download the **non-Unity build** from the official [Zenject GitHub repository](https://github.com/modesttree/Zenject)
2. Extract the downloaded archived `*.dll` files into your project's `bin` folder
3. Add references to the `*.dll` files in your project:

  - **Option 1: Using Your IDE**

    1. Open your project in your preferred **IDE**.
    2. Open the **Reference Manager** or the equivalent interface for managing project references.
    3. Use the **Browse** option to locate the required `DLLs` in the project's `bin` folder.
    4. Select previously added files.
    5. Confirm the selection to add them as references in your project.
  - **Option 2: Manually edit the **.csproj* file** Open your project `*.csproj` file and add: ```xml <ItemGroup> <Reference Include="Zenject"> <HintPath>bin\Zenject.dll</HintPath> </Reference> <Reference Include="Zenject-Signals"> <HintPath>bin\Zenject-Signals.dll</HintPath> </Reference> <Reference Include="Zenject-usage"> <HintPath>bin\Zenject-usage.dll</HintPath> </Reference> </ItemGroup> ```
4. Restart your **IDE** (and **Editor**, if needed) to ensure the changes are recognized.
5. You're now ready to use the Zenject in your project. For usage details, refer to the Zenject documentation. ```csharp public interface ISomeInterface { void Send(string message); } public class SomeImplementation : Component, ISomeInterface { public void Send (string message) { Log.MessageLine(message); } } ``` ```csharp using System.Collections; using System.Collections.Generic; using Unigine; using Zenject; [Component(PropertyGuid = "AUTOGENERATED_GUID")] public class ClientCode : Component { void Init() { var container = new DiContainer(); container.Bind<ISomeInterface>().To<SomeImplementation>().AsSingle(); var foo = container.Resolve<ISomeInterface>(); foo.Send("Hello, Zenject!"); } } ```


### Setting up Microsoft DI in a UNIGINE Project


1. Open your project in your preferred IDE.
2. Install the **NuGet** package for **Microsoft.Extensions.DependencyInjection**:

  - Via the built-in IDE **NuGet Package Manager**, or
  - Using the **.NET CLI** command: ```bash dotnet add package Microsoft.Extensions.DependencyInjection ```
3. That's it - **Microsoft's DI** framework is now available in your project. You can build more complex setups using scopes, lifetimes, and modules - see the [official docs](https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection) for details. ```csharp using System.Collections; using System.Collections.Generic; using Unigine; using Microsoft.Extensions.DependencyInjection; [Component(PropertyGuid = "AUTOGENERATED_GUID")] public class ClientCode : Component { void Init() { var services = new ServiceCollection(); services.AddTransient<ISomeInterface, SomeImplementation>(); var serviceProvider = services.BuildServiceProvider(); var foo = serviceProvider.GetRequiredService<ISomeInterface>(); foo.Send("Hello, .NET DI!"); } } ```
