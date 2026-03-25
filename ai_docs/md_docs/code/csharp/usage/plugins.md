# Plugin Class


You can get access to the [main loop](../../../code/fundamentals/execution_sequence/index.md) of the Unigine engine by overriding virtual methods of the *Unigine.Plugin* class. This article describes the sample located in the `<UnigineSDK>/source/csharp/samples/Api/Systems/Ffp/` directory.


> **Notice:** In the C# API you can inherit from the Plugin class only once.


### See also


- An example can be found in the `<UnigineSDK>/source/csharp/samples/Api/Systems/Ffp/` directory.
- C++ API classes [Unigine::Plugin](../../../api/library/common/class.plugin_cpp.md) and [Unigine::Ffp](../../../api/library/rendering/class.ffp_cpp.md) which have the same methods and behavior as in the C# API.


## Plugin Class Usage Example


### C# Side


To use the *Unigine.Plugin* class, you should create your own class and inherit it from the *Unigine.Plugin* class and override necessary methods, which the engine will perform in its main loop.


```csharp
using System;
using Unigine;

class UnigineApp
{
	class FfpPlugin : Plugin
	{
		private float time;

		public override void Gui(EngineWindowViewport window)
		{
			time += Engine.IFps;
			Render(time);
		}

		private void Render(float time)
		{
			// screen size
			int width = 0;
			int height = 0;

			EngineWindow main_window = WindowManager.MainWindow;
			if (main_window != null)
			{
				width = main_window.Size.x;
				height = main_window.Size.y;
			}

			float radius = height / 2.0f;

			Ffp.Enable(Ffp.MODE_SOLID);
			Ffp.SetOrtho(width, height);

			// begin triangles
			Ffp.BeginTriangles();

			// vertex colors
			uint[] colors = { 0xffff0000, 0xff00ff00, 0xff0000ff };

			// create vertices
			int num_vertex = 16;
			for (int i = 0; i < num_vertex; i++)
			{
				float angle = MathLib.PI2 * i / (num_vertex - 1) - time;
				float x = width / 2 + (float)Math.Sin(angle) * radius;
				float y = height / 2 + (float)Math.Cos(angle) * radius;
				Ffp.AddVertex(x, y);
				Ffp.SetColor(colors[i % 3]);
			}

			// create indices
			for (int i = 1; i < num_vertex; i++)
			{
				Ffp.AddIndex(0);
				Ffp.AddIndex(i);
				Ffp.AddIndex(i - 1);
			}

			// end triangles
			Ffp.EndTriangles();

			Ffp.Disable();
		}
	}

	class AppSystemLogic : SystemLogic
	{
		public override bool Init()
		{
			Engine.BackgroundUpdate = Engine.BACKGROUND_UPDATE.BACKGROUND_UPDATE_RENDER_NON_MINIMIZED;
			Unigine.Console.Run("world_load data/ffp");
			return true;
		}

	}

	class AppWorldLogic : WorldLogic
	{
		FfpPlugin plugin;

		public override bool Init()
		{
			// create plugin
			plugin = new FfpPlugin();
			Engine.AddPlugin(plugin);
            Unigine.Console.Active = true;

            return true;
        }

		public override bool Shutdown()
		{
			// remove plugin
			Engine.DestroyPlugin(plugin);

			return true;
		}
	}
}

```


In this part of the code we create the *FfpPlugin* class which inherits the *Plugin* class and override the *Gui()* method. We specified the *Render()* method and call it inside the overridden *Gui()* method. Engine calls this function before Gui each render frame.


In the *Main()* method, we create an instance of the *FfpPlugin* class and add it to the engine by using the *AddPlugin()* method after the engine had been initialized.


### Output


The following result will be shown:


![](plugin_output.png)
