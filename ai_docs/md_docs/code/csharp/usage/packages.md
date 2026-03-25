# Package Class


The Package class is a data provider for the internal FileSystem class. You can load all resources via this class. This article describes the sample located in the `<UnigineSDK>/source/csharp/samples/Api/Systems/Package/` directory.


> **Notice:** In the C# API you can inherit from the Package class only once.


### See also


- An example can be found in the `<UnigineSDK>/source/csharp/samples/Api/Systems/Package/` directory.
- The C++ API [Unigine::Package](../../../api/library/filesystem/class.package_cpp.md) class and the [Unigine::FileSystem](../../../api/library/filesystem/class.filesystem_cpp.md) class which have the same methods and behavior as in the C# API.


## Package Class Usage Example


### C# Side


To use the *Unigine.Package* class, you should create your own class and inherit it from the *Unigine.Package* class and override virtual methods.


```csharp
using System;
using System.IO;
using File = System.IO.File;
using System.Runtime.InteropServices;
using Unigine;

class UnigineApp
{
	class MyPackage : Package
	{
		private FileStream file;

		public MyPackage()
		{
			Log.Message("MyPackage.ctor(): called\n");
		}

		~MyPackage()
		{
			Log.Message("MyPackage.dtor(): called\n");
		}

		// list of files
		public override int GetNumFiles()
		{
			Log.Message("MyPackage.GetNumFiles(): called\n");
			return 2;
		}

		public override string GetFilePath(int num)
		{
			Log.Message("MyPackage.GetFilePath({0}): called\n", num);
			if (num == 0)
				return "data/package.usc";
			else if (num == 1)
				return "data/package.world";
			return "";
		}

		// select file
		public override bool SelectFile(string path, out ulong size)
		{
			Log.Message("MyPackage.SelectFile(\"{0}\",): called\n", path);

			try
			{
				file = null;
				if (path == "data/package.usc")
					file = File.OpenRead("my_data/package.usc");
				else if (path == "data/package.world")
					file = File.OpenRead("my_data/package.world");
			}
			catch (Exception e)
			{
				Log.Error("MyPackage.SelectFile(): {0}\n", e.Message);
				size = 0;
				return false;
			}

			size = (ulong)file.Length;
			return true;
		}

		// read file
		public override bool ReadFile(IntPtr data, ulong size)
		{
			Log.Message("MyPackage.ReadFile(,{0}): called\n", size);

			try
			{
				byte[] src = new byte[size];
				int ret = file.Read(src, 0, (int)size);
				Marshal.Copy(src, 0, data, ret);
			}
			catch (Exception e)
			{
				Log.Error("MyPackage.ReadFile(): {0}\n", e.Message);
				return false;
			}

			return true;
		}
	}

	/*
	 */
	[STAThread]
	static void Main(string[] args)
	{
		// add package
		MyPackage package = new MyPackage();
		FileSystem.PreloadExternPackage(package);

		// initialize engine
		Engine.Init(args);

		// enter main loop
		Engine.Main();

		// shutdown engine
		Engine.Shutdown();
	}
}


```


The MyPackage class has overridden *ReadFile()*, *SelectFile()*, *GetFilePath()* and *GetNumFiles()* functions. The class operates with two files located in the `my_data` folder.


In the *Main()* function we create an instance of the MyPackage class and add it to the FileSystem **before initializing the engine** using the *[PreloadExternPackage()](../../../api/library/filesystem/class.filesystem_cpp.md#preloadExternPackage_Package_void)* method.


### Output


The following result will be shown in the console:


![](package_console_output.png)
