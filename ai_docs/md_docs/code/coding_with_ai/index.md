# AI-Assisted Development in UNIGINE


When developing a real-time 3D application, you work across many different areas: rendering, physics, UI, networking, and more. Each comes with its own set of classes and workflows. The API is extensive, and inline documentation works well when you already know the class you need. But often you start with a task, not a class name:


- *"How do I move an object with player input?"*
- *"How does collision detection work?"*
- *"Is there a code sample for runtime material changes?"*


Finding the answer means searching docs, reading through classes, checking samples. It's not difficult, but getting to it just takes a few extra steps.


## AI Toolkit


AI agents know UNIGINE significantly worse than some of the more widely adopted engines. They mix up the API, invent methods that don't exist, and carry over assumptions from other tools. AI Toolkit solves this by giving the agent the right context from the start.


![Development workflow without AI Toolkit](without_mcp.svg)


AI Toolkit is a curated build of the UNIGINE documentation optimized for consumption by AI agents, together with the editor plugin that lets an agent work in the Editor itself. Adding it to a project brings:


- Complete UNIGINE documentation - guides, tutorials, and full API reference for C++ and C#
- Working code samples organized by topic - animation, physics, rendering, networking, VR, and more
- A set of behavioral rules that prevent the agent from guessing when it should be looking things up
- The MCPBridge editor plugin, which opens the running Editor to the agent


Include AI Toolkit into your project and the agent picks up the documentation automatically. Instead of hallucinating an API that looks plausible, it searches the docs, finds the real one, and uses it correctly. When it doesn't find something, it says so.


![Development workflow with AI Toolkit](with_mcp.svg)


When you ask *"How do I handle keyboard input?"*, the assistant locates the relevant classes, reviews the methods, and explains the approach. It can also retrieve relevant code samples that demonstrate the concept. The entire process takes seconds and happens without leaving your development environment.


> **Notice:** Any AI coding assistant will work with AI Toolkit, including Claude Desktop, Claude Code, Cursor, Windsurf and others.


You can ask questions in any language. The assistant searches the English documentation and responds in your language, so there's no need to translate your question or parse English results yourself.


## Getting Started


Add AI Toolkit to your project when creating it, or at any point later from the project configuration screen. The documentation package on its own is also available on **[GitHub](https://github.com/unigine-engine/ai-docs)**:


![Adding AI Toolkit from project configuration](ai_docs.png)


The package includes approximately 3,100 documentation pages, 44,000 API methods, 240 code samples, 800 console commands for **UNIGINE 2.22**, and system prompt files (**CLAUDE.md**, **AGENTS.md**, **copilot-instructions.md**) that popular AI coding assistants pick up automatically.


![](ai_docs_in_project.png)

*Project folder with AI Toolkit added: documentation inai_docs, system prompt files next to it, and the MCPBridge plugin inbin/plugins/Unigine.*


Open your project in an AI-powered IDE or connect a CLI agent to the project folder - [Claude Code](https://claude.ai/download), [Cursor](https://www.cursor.com/), [GitHub Copilot](https://github.com/features/copilot), and others will pick up AI Toolkit automatically.


> **Notice:** If your agent doesn't recognize system prompt files, copy their contents into its system prompt according to the agent's documentation.


## Usage Examples


With access to AI Toolkit, the assistant no longer needs you to explain UNIGINE concepts or provide context. You describe what you want to achieve, and it finds the relevant information itself.


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


## Editor Integration (EXPERIMENTAL)


> **Warning:** This feature is experimental. Good for a quick deep-dive into the engine, learning, and rapid prototyping - not recommended for production projects.


The **MCPBridge** plugin runs a built-in HTTP server directly inside UNIGINE Editor. AI agents connect to it over MCP - no external scripts or middleware required. The server listens on localhost only and comes up with the Editor.


With this integration, the assistant can inspect and modify the scene in real time. 58 tools are grouped by area:


- Scene and nodes - creating nodes from primitives, templates or project assets, then cloning, renaming, reparenting, transforming, enabling, deleting and selecting them
- Node internals - component properties, surfaces and their material bindings, physics bodies and shapes
- Materials - creating, cloning, re-inheriting, inspecting and updating them
- Properties - the full lifecycle, from creation and inheritance to renaming and removal
- Assets - listing, importing with per-format import settings, inspecting dependencies, generating landscape maps
- Settings - inspecting and changing engine settings, environment and presets
- Baking - lighting and probe bakes with progress reporting
- Profiling - profiler counters, streaming and VRAM statistics, per-surface draw and memory cost, system info
- Viewport - camera control and screenshots returned to the assistant as images
- Console - running engine commands and reading the log back


Some of these exist so the assistant can check itself instead of guessing. Spatial queries report what already occupies a region, what a ray hits, and the real height of the surface at a given point, which is what keeps a crate from ending up halfway inside the terrain. Screenshots let the assistant look at what it has just built. Every change goes through the Editor's undo stack, and a whole sequence of calls can be folded into a single undoable step, or rolled back as one.


### Connecting an Agent to the Editor


The plugin comes with the project, and its server comes up with the Editor. Open the **MCP Bridge** panel in UNIGINE Editor and point your agent at it:


![Opening the MCP Bridge panel](mcp_bridge_panel_location.png)

*The panel is opened fromWindows -> MCP Bridge.*


- Check the endpoint. The server is already listening at **http://127.0.0.1:8765/mcp**; change the port and press **Apply** if you need another one, or press **Stop** to shut the server down.
- Expand **Setup / How to connect** and press **Write config files to project**. This generates **.mcp.json** for Claude Code and Cursor, **.vscode/mcp.json** for VS Code, and **.gemini/settings.json** for Gemini CLI and Qwen Code. Entries for other MCP servers already present in these files are preserved.
- Reconnect the agent if it doesn't pick up the tools on its own.


![](mcp_bridge_editor_panel.png)

*Server status and endpoint, the tool list grouped by area, and call statistics.*


The panel also lets you switch individual tools off, so the assistant neither sees them nor can call them, and it counts calls and errors while the assistant works.


For example: *"Create a simple arena with various primitives and apply different materials to them."* The assistant builds the scene step by step - creating objects, positioning them, and assigning materials to each surface.

   Sorry, your browser does not support embedded videos.
AI Toolkit gives the assistant both sides of the job at once: knowledge of the engine from the documentation and behavioral rules, and hands-on control of the Editor from MCPBridge.


> **Notice:** MCPBridge is installed together with AI Toolkit, so there is nothing to download separately. The documentation and prompts work on their own if you only need coding assistance and no Editor access.
