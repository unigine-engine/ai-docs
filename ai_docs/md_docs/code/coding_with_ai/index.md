# AI-Assisted Development in UNIGINE


When developing a real-time 3D application, you work across many different areas: rendering, physics, UI, networking, and more. Each comes with its own set of classes and workflows. The API is extensive, and inline documentation works well when you already know the class you need. But often you start with a task, not a class name:


- *"How do I move an object with player input?"*
- *"How does collision detection work?"*
- *"Is there a code sample for runtime material changes?"*


Finding the answer means searching docs, reading through classes, checking samples. It's not difficult, but getting to it just takes a few extra steps.


## AI Docs


AI agents know UNIGINE significantly worse than some of the more widely adopted engines. They mix up the API, invent methods that don't exist, and carry over assumptions from other tools. AI Docs solve this by giving the agent the right context from the start.


![Development workflow without AI Docs](without_mcp.svg)


AI Docs is a curated build of the UNIGINE documentation, optimized for consumption by AI agents. The package includes:


- Complete UNIGINE documentation - guides, tutorials, and full API reference for C++ and C#
- Working code samples organized by topic - animation, physics, rendering, networking, VR, and more
- A set of behavioral rules that prevent the agent from guessing when it should be looking things up


Include AI Docs into your project and the agent picks them up automatically. Instead of hallucinating an API that looks plausible, it searches the docs, finds the real one, and uses it correctly. When it doesn't find something, it says so.


![Development workflow with AI Docs](with_mcp.svg)


When you ask *"How do I handle keyboard input?"*, the assistant locates the relevant classes, reviews the methods, and explains the approach. It can also retrieve relevant code samples that demonstrate the concept. The entire process takes seconds and happens without leaving your development environment.


> **Notice:** Any AI coding assistant will work with AI Docs, including Claude Desktop, Claude Code, Cursor, Windsurf and others.


You can ask questions in any language. The assistant searches the English documentation and responds in your language, so there's no need to translate your question or parse English results yourself.


## Getting Started


To get started, grab AI Docs from **[GitHub](https://github.com/unigine-engine/ai-docs)** or add them to your project directly from the project configuration screen:


![Adding AI Docs from project configuration](ai_docs.png)


The package includes approximately 3,100 documentation pages, 44,000 API methods, 240 code samples, 800 console commands for **UNIGINE 2.21**, and system prompt files (**CLAUDE.md**, **AGENTS.md**, **copilot-instructions.md**) that popular AI coding assistants pick up automatically.


![](ai_docs_in_project.png)

*Project folder with AI Docs added.*


Open your project in an AI-powered IDE or connect a CLI agent to the project folder - [Claude Code](https://claude.ai/download), [Cursor](https://www.cursor.com/), [GitHub Copilot](https://github.com/features/copilot), and others will pick up AI Docs automatically.


> **Notice:** If your agent doesn't recognize system prompt files, copy their contents into its system prompt according to the agent's documentation.


## Usage Examples


With access to AI Docs, the assistant no longer needs you to explain UNIGINE concepts or provide context. You describe what you want to achieve, and it finds the relevant information itself.


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


Before generating the code, the assistant reads the behavioral rules and contextual guides included with AI Docs - these cover component lifecycle, precision handling, and engine conventions - which helps it produce code that follows UNIGINE patterns from the start.

   Sorry, your browser does not support embedded videos.
### Solving Visual Issues


Describe what you see, not what you think the solution is. For example:


```text
Thin geometry in my scene doesn't look right - edges are noisy and seem to break apart when the camera moves. What's going on?
```


The assistant searches the documentation, identifies the likely cause, and provides the relevant console commands to adjust the settings.

   Sorry, your browser does not support embedded videos.
> **Notice:** Results may vary depending on the AI assistant and model you use. AI Docs provide accurate documentation and samples, but how the assistant interprets and applies them is determined by the model itself.


## Editor Integration (EXPERIMENTAL)


> **Warning:** This feature is experimental. Good for a quick deep-dive into the engine, learning, and rapid prototyping - not recommended for production projects.


The **MCPBridge** plugin runs a built-in HTTP server directly inside UNIGINE Editor. AI agents connect to it over MCP - no external scripts or middleware required.


With this integration, the assistant can inspect and modify the scene in real time. 27 tools cover the basics:


- Creating primitives and nodes from templates or project assets
- Transforming, cloning, renaming, reparenting nodes
- Applying materials and configuring surface masks
- Attaching and configuring components
- Inspecting and modifying nodes via XML export/import
- Executing console commands
- Batch operations with full undo/redo support


For example: *"Create a simple arena with various primitives and apply different materials to them."* The assistant builds the scene step by step - creating objects, positioning them, and assigning materials to each surface.

   Sorry, your browser does not support embedded videos.
For the best results, pair both tools - the agent gets the knowledge about the engine from AI Docs and hands-on control of the Editor from MCPBridge.


> **Notice:** AI Docs work on their own. Editor integration additionally requires the **MCPBridge Editor plugin**, available separately on the [Add-On Store](https://store.unigine.com/).
