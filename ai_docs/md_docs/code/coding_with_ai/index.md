# AI-Assisted Development in UNIGINE


You want to build a world and make things happen in it. Most of the time you start with a task, not a class name:


- *"How do I move an object with player input?"*
- *"How does collision detection work?"*
- *"Is there a code sample for runtime material changes?"*


Finding the answer means searching docs, reading through classes, checking samples. It's not difficult, but getting to it just takes a few extra steps.


**AI Toolkit** puts the answers where you are already working, and your AI assistant (*Claude Desktop, Claude Code, Cursor, Windsurf*, or other) can build and edit your scene in UnigineEditor while you watch. Adding the toolkit to a project brings:


- **Complete UNIGINE documentation** - guides, tutorials, and full API reference for C++ and C#
- **Working code samples** organized by topic - animation, physics, rendering, networking, VR, and more
- A **set of behavioral rules** (**CLAUDE.md**, **AGENTS.md** and **copilot-instructions.md**) that prevent the assistant from guessing when it should be looking things up
- The **MCPBridge Editor** plugin, which opens the running Editor to the assistant


![](ai_docs_in_project.png)

*Project folder with AI Toolkit added: documentation inai_docs, system prompt files next to it, and the MCPBridge plugin inbin/plugins/Unigine.*


## Get Up and Running


1. **Add AI Toolkit to your project**. In [SDK Browser](../../sdk/index.md#projects), open [Create New Project](../../sdk/projects/index_cpp.md#creation), expand **Advanced Settings** and tick **AI Toolkit** under **Features**. For a project you already have, use **Other Actions -> [Configure](../../sdk/projects/index_cpp.md#configure)**. ![Adding AI Toolkit from project configuration](ai_docs.png)
2. **Set Up Your AI Environment**. You can use an AI-powered IDE such as [VS Code](https://code.visualstudio.com/) - install it first if you do not have it yet. **Using VS Code + [Claude](https://www.claude.com/product/claude-code):** ![](claude_extension.png) You can also use alternatives like *[Cursor](https://www.cursor.com/), [Codex](https://openai.com/codex/), [GitHub Copilot](https://github.com/features/copilot)* or a CLI agent, if you prefer.

  - Open *Extensions* in VS Code
  - Search for *Claude Code* extension from Anthropic. (or a compatible Claude extension)
  - Install the extension
  - Sign in to your Anthropic account or provide an API key
3. **Open the Project in an AI-powered IDE or connect a CLI agent to the project folder.** Open the **project root** - the folder that contains **ai_docs** and the system prompt files, shown above. In SDK Browser it is **Other Actions -> Open Folder**. Opening a subfolder instead means the assistant will not find them. ![](open_folder.png) Once the project is opened, your AI assistant will automatically detect the AI Toolkit and use the docs as context.
4. **Ask your first question in plain words** - there is no need to name a class: ```text How do I handle keyboard input? ``` The assistant locates the relevant classes, reviews the methods, and explains the approach. It can also retrieve code samples that demonstrate the concept. This takes seconds, without leaving your development environment.


> **Notice:** The system prompt files - **CLAUDE.md, AGENTS.md** and **copilot-instructions.md** - sit in the project root, and most assistants read them automatically. If yours does not, paste their contents into its system prompt according to the agent's documentation.


## Building and Editing Worlds with the Assistant (MCP-Bridge)


The **MCPBridge** plugin comes with **AI Toolkit** and runs a small server inside UnigineEditor, so the assistant can build and edit your scene while you watch. Assistants connect to it over MCP - the standard way an assistant talks to an external tool. The server runs over HTTP+SSE on localhost only, comes up with the Editor on the port you choose, and needs no external scripts or proxies to keep alive.


> **Notice:** Editor integration is experimental, but it already does a lot and is great for learning the engine and quick prototyping - just keep it away from production projects for now.


The assistant has 58 tools available. Click the spoiler below to see the list of actions it can perform in the Editor:


<details>
<summary>List of actions | Close</summary>

- **Build and edit the scene** - create nodes (the objects that make up your scene) from primitives, templates or project assets, then clone, rename, reparent, transform, enable, delete and select them; attach and configure components (the scripts you attach to an object) and their properties; edit surfaces (the separately shaded parts of a model) and the materials bound to them; set up physics bodies and shapes
- **Build material and property hierarchies** - create, clone, re-inherit, inspect, update and remove them, instead of only assigning what already exists
- **Look before it acts** - spatial queries report what occupies a region, what a ray hits, and the real surface height at a given point, which is what keeps a crate from ending up halfway inside the terrain
- **Check its own work** - it controls the camera and takes viewport screenshots that come back to it as images, and it can read back every node, material and setting in full
- **Handle the project around the scene** - assets with per-format import settings, dependencies, landscape maps, engine and environment settings, presets
- **Bake and profile** - lighting and probe bakes with progress reporting, profiler counters, streaming and VRAM statistics, per-surface draw and memory cost, system info
- **Run engine console commands** and read the log back, for anything that has no dedicated tool

</details>


Every change goes through the Editor's undo stack, so you can undo whatever the assistant did. A whole sequence of calls can be folded into a single undoable step, or rolled back as one.


### Connecting an Agent to the Editor


Open your project in [UnigineEditor](../../editor2/index.md) (**Open Editor** in [SDK Browser](../../sdk/projects/index_cpp.md#edit)), then open the **MCP Bridge** panel (*Windows -> MCP Bridge*) and point your assistant at it:


![Opening the MCP Bridge panel](mcp_bridge_panel_location.png)


1. Check the endpoint. The server is already listening at **http://127.0.0.1:8765/mcp**; change the port and press **Apply** if you need another one, or press **Stop** to shut the server down.
2. Expand **Setup / How to connect** and press **Write config files to project**. This generates `.mcp.json` for Claude Code and Cursor, `.vscode/mcp.json` for VS Code, and `.gemini/settings.json` for Gemini CLI and Qwen Code. The panel also has ready-made snippets for Codex, Windsurf, Cline, Zed and others. Entries for other MCP servers already present in these files are preserved.
3. Most assistants pick up the tools on their own - if yours does not, restart it and reconnect.
4. Check that it worked: ask the assistant to *"create a box in the scene"*. The box appears in the viewport, and the call count in the panel goes up. If it stays at zero, the assistant never reached the server - re-check the endpoint in step 1 and the config file from step 2.


> **Notice:** The server runs inside UnigineEditor, so the Editor has to stay open while the assistant works. Close it and the tools disappear from the assistant until you open the project again.


![](mcp_bridge_editor_panel.png)

*Server status and endpoint, the tool list grouped by area, and call statistics.*


You can switch individual tools off, so the assistant neither sees them nor can call them, and the panel counts calls and errors while the assistant works.


Now ask for something, and watch the scene change. For example: *"Create a simple arena with various primitives and apply different materials to them."* The assistant builds the scene step by step - creating objects, positioning them, and assigning materials to each surface.

   Sorry, your browser does not support embedded videos.
**AI Toolkit** gives the assistant both sides of the job at once: knowledge of the engine from the documentation and behavioral rules, and hands-on control of the Editor from **MCPBridge**.


## Writing Code with the Assistant


You don't need to explain UNIGINE concepts or provide context. Describe what you want to achieve, and the assistant finds the relevant information itself.


### Learning the Engine


Ask the assistant to explain a concept you're unfamiliar with. For example:


```text
Explain how the component system works in UNIGINE. What lifecycle methods are available and in what order are they called?
```


The assistant searches the documentation, finds the relevant articles, and provides a structured explanation with references to the actual API.

   Sorry, your browser does not support embedded videos.
### Finding the Right API


You know what you want to do, but not which class or method to use. For example:


```text
I need to cast a ray from the camera and find what object the player is looking at. Which classes and methods should I use?
```


The assistant finds the relevant intersection API, explains the available approaches, and shows how to set up the query.

   Sorry, your browser does not support embedded videos.
### Creating Code Sample


Ask the assistant to write a component for you. For example:


```text
Write a C# component that rotates an object around the Y axis at a configurable speed.
```


Before generating the code, the assistant reads the behavioral rules and contextual guides included with AI Toolkit - these cover component lifecycle, precision handling, and engine conventions - which helps it produce code that follows UNIGINE patterns from the start.

   Sorry, your browser does not support embedded videos.
### Solving Visual Issues


Describe what you see, not what you think the solution is. For example:


```text
Thin geometry in my scene doesn't look right - edges are noisy and seem to break apart when the camera moves. What's going on?
```


The assistant searches the documentation, identifies the likely cause, and provides the relevant console commands to adjust the settings.

   Sorry, your browser does not support embedded videos.
> **Notice:** Results may vary depending on the AI assistant and model you use. AI Toolkit provides accurate documentation and samples, but how the assistant interprets and applies them is determined by the model itself.


## AI Toolkit Benefits


AI assistants know UNIGINE significantly worse than the more widely adopted engines. They mix up the API, invent methods that don't exist, and carry over assumptions from other tools. Without the right context, every answer has to be checked before you can use it:


![Development workflow without AI Toolkit](without_mcp.svg)


**AI Toolkit** gives the assistant that context from the start. The lookup moves to the assistant's side, and the behavioral rules tell it to say so when it cannot find something - so what comes back is grounded in the real API:


![Development workflow with AI Toolkit](with_mcp.svg)


The package covers approximately 3,100 documentation pages, 44,000 API methods, 240 code samples and 800 console commands, plus the system prompt files that popular AI coding assistants pick up automatically. Everything arrives with the project - there is nothing to download separately.


The documentation and prompts also work on their own if you only need coding help and no Editor access. The documentation package alone is available on **[GitHub](https://github.com/unigine-engine/ai-docs)**.


You can ask questions in any language. The assistant searches the English documentation and responds in your language, so there's no need to translate your question or parse English results yourself.
