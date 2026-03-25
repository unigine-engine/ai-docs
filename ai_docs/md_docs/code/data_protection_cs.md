# Protecting Your Data with a Password (CS)


In order to protect your source code and content, you are recommended to use the *[Archiver](../tools/archiver/index.md)* tool to archive your resources into UNG archives. It implements data encrypting to avoid unauthorized access and provides a password protection.


To protect resources, you need to create an archive with the password specified and pass the same password on engine initialization. The workflow is as follows:


- Create an [UNG archive](../tools/archiver/index.md#usage) with the specified password. For example, to create an archive named `files.ung` with the 12345 password that contains the `textures` directory, pass the following CLI: ```bash ung_x64 -o files.ung -d textures -p 12345 ```
- Specify the same password to be passed on [engine initialization](../api/library/engine/class.engine_cs.md#init_parameters) in the `<your_project_name>.cpp` file: ```csharp // ... [STAThread] static void Main(string[] args) { Engine.InitParameters init_params = new Engine.InitParameters(); init_params.window_title = "Your_Title"; init_params.project = "<your_project_name>"; init_params.password = "12345"; Engine.Init(init_params, args); AppSystemLogic system_logic = new AppSystemLogic(); AppWorldLogic world_logic = new AppWorldLogic(); Engine.Main(system_logic, world_logic, editor_logic); // shutdown engine Engine.Shutdown(); } ``` > **Notice:** If you pass a project name during engine initialization, this means the engine will store its rewritable data (such as logs, cache and configuration files) in user profile (in `C:\Users\<username>` on Windows or in `/home/<username>` on Linux) rather than `<UnigineSDK/bin/` or `<UnigineSDK/data/` folders. On engine initialization, you can set ***null*** to the *project* attribute of initialization parameters, if you don't need that data is stored in user profile: ```csharp // engine initialization Engine.InitParameters init_params = new Engine.InitParameters(); init_params.project = null; init_params.password = "12345"; Engine.Init(init_params, args); ```
