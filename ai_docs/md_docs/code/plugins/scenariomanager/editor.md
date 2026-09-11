# Scenario Manager Editor


The Scenario Manager editor is a **visual web-based tool for building and managing application logic**. It allows you to create various scenarios in the world such as connecting objects to assigned sockets, checking states (e.g., execution or completion status), handling inventory interactions, and more.


The editor consists of a node canvas where you place, set, group and delete nodes, connect their ports, and define the logic flow of your application. It supports undo/redo and copy/paste (including across graphs), duplicate systems, debugging breakpoints, nested navigation into subgraphs and a real-time graph validation.


The HTTP server is built directly into the framework and starts automatically when Scenario Manager is launched, no external server software is required.


## Editor Layout


The Scenario Manager editor window is divided into the following areas:


### Toolbar


![](img/sm_toolbar.png)


Located at the top of the window:


- **Main menu**

  - **Save** - saves the current graph. After saving, the engine automatically hot-reloads the modified script without restart.
  - **Save As...** - saves the current graph to a new `*.sgraph` file.
  - **Copy JSON to Clipboard** - copy current graph data in JSON format.
  - **Paste JSON from Clipboard** - paste graph data in JSON format.
  - **Validate Graph** - performs real-time validation of the current graph (unconnected mandatory ports, type mismatches, cycles). When a validation issue is detected, a warning icon also appears on the corresponding node in real-time. Hover over the icon to see a tooltip explaining the problem. ![Scenario Manager Editor Toolbar](img/sm_validation.png)
  - **Graph Properties** - current graph metadata (version, name, description, date of creation/last modification).
  - **Run Benchmark** - launches a benchmark and outputs results to the Engine console.
  - **Guide** - quick editor guide.
  - **Controls & Hotkeys** - mouse and keyboard controls reference.
  - **Palette (types)** - color reference for port and connector types.
- **Back / Forward arrows** - navigate through the graph browsing history.
- **Run** - starts the currently open graph.
- **Stop** - stops all running scripts.
- **Debug** - highlights execution flow through nodes (can also be activated from the *Debug* panel).
- **Last Executed Action** - highlights the most recent action or its result.


### Node Canvas


The main editing area where you *[create](#sm_create)*, *[arrange](#layout_canvas_groups)*, and *[connect](#sm_create_connect)* nodes. The canvas supports panning and zooming.


![Scenario Manager Editor Node Canvas](img/sm_canvas.png)


### Side Panels


A set of collapsible sections on the side of the window. The *Runtime* panel on the right can also be hidden entirely via its toggle button, freeing up additional canvas space.


[![Scenario Manager Editor Side Panels](img/sm_panels_b.png)](img/sm_panels_b.png)


#### Graphs


A list of all `.sgraph` files in the project. Each graph entry has a delete button. Click a graph to open it in the canvas.


To create a new graph, click ![Create New Graph](img/sm_add.png). If necessary, choose an existing subfolder or create a new one for organization - subfolders can be collapsed in the hierarchy. To reload the list (e.g., if new graphs have been added or renamed in the project folder) click the ![Rescan Disk](img/sm_reload.png) button. The *Filter graphs* field allows searching graphs by name.


![](img/sm_addgraph.png)


Right-click a graph in the list to open its submenu:


![](img/sm_graph_submenu.png)


- **Rename** - change the graph's *[name](../../../code/plugins/scenariomanager/index.md#sm_troubleshooting_name)* > **Warning:** Renaming a graph while the **UnigineEditor is running** may cause the Editor crash.
- **Duplicate** - create the graph's copy.
- **Move To Folder** - change the graph's location in the hierarchy.
- **Delete** - remove the graph. > **Warning:** Deleting a graph removes its `.sgraph` file from the `data/` folder irreversibly.


Drag a graph from the list onto the canvas to use it as a *[subgraph](../../../code/plugins/scenariomanager/index.md#graph_subgraphs)*. Its input and output ports are defined in the *[Interface](#panel_interface)* panel of that graph (open the graph to configure them).


#### Variables


A list of all variables defined in the current graph. To create a new local variable, click ![Add Local Variable button](img/sm_add.png) and specify its name, type, and default value.


![Local Variables Panel](img/sm_var.png)


Drag a variable from the list onto the canvas to create a node: drag normally to create a ***Get Variable*** node, or hold ***Shift*** while dragging to create a ***Set Variable*** node. Each variable entry has a delete button that removes it from the graph.


#### Global Variables


A list of global variables shared across all graphs. To create a new global variable, click ![Add Global Variable button](img/sm_add.png) and specify its name, type, and default value.


![Global Variables Panel](img/sm_global.png)


Drag a variable from the list onto the canvas to create a node: drag normally to create a ***Get Variable*** node, or hold ***Shift*** while dragging to create a ***Set Variable*** node. Each variable entry has a delete button that removes it from the global scope.


#### Interface


A list of all input and output ports (execution and data) of the current graph when it is used as a subgraph. To create a new port, click the ![Add Subgraph Pin button](img/sm_add.png) button and specify its name, flow and type.


![Interface Panel](img/sm_interface_panel.png)


Each entry has a delete button that removes it from the graph. Once created, ports can be dragged from the panel onto the canvas and connected to nodes within the graph.


#### Scripts


A tree of all running scripts - currently executed graph instances. The panel allows you to stop or restart individual scripts, and provides quick access to open the corresponding graph in the canvas directly from the panel.


![Interface Panel](img/sm_scripts.png)


> **Notice:** When you save a graph, the Engine automatically hot-reloads it without restarting.


#### Profile


The *Profile* panel displays execution timings, helping identify performance bottlenecks and optimize graph logic.


![Profile Panel](img/sm_profile.png)


#### Debug


The *Debug* panel provides a full-featured debugger for visual scripting, including execution highlighting and breakpoints. Set a breakpoint by right-clicking a node and selecting *Set Breakpoint*, then use *F5* to continue execution and *F10* to step through nodes. Supports value inspection and call stack visualization.


> **Notice:** Breakpoints only work when *Debug* is enabled.


Debug mode can also be activated via the *Debug* button in the *[Toolbar](#layout_toolbar)*.


![Debug Panel](img/sm_debug_panel.png)


### Navigation and Shortcuts


Everything you need to navigate the canvas, manage nodes, and organize your workspace.


> **Notice:** In the editor, use *Controls & Hotkeys* from the *[Toolbar](#layout_toolbar) Menu* for a quick reference of the available controls.


#### Mouse Controls


Use the mouse to navigate the canvas, select and move nodes, and create connections between ports.


| Canvas Navigation |  |
|---|---|
| MMB /LMB Drag | Pan the canvas. |
| Scroll Wheel | Zoom in and out (centered on cursor position). |
| Node Creation |  |
| Double-click on Canvas | Open node creation menu (organized in categories). |
| Right-click on Canvas | Open creation menu (add a new group or node). |
| Node Selection and Manipulation |  |
| Left-click on Node | Select a node. Hold **Shift** to add to selection, **Ctrl** to remove from selection. |
| Left-click on Node's Parameter | Edit parameter in place. |
| Left-click on Node's Top-Left Corner | Collapse/expand node. |
| Right-click on Node | Open node submenu (add/remove pins, set breakpoints, clone, etc.). |
| Ctrl + LMB Drag | Box-select multiple nodes. |
| Drag on Node | Move selected nodes. |
| Drag on Node Corner | Resize node. |
| Connections |  |
| Drag from Port to Port | Create a connection. |
| Shift + Drag from Port | Open compatible node creation menu. |
| Left Click on Wire | Select the wire. |
| Ctrl + Left Click on Wire | Add the wire to the selection or remove it from the selection. |
| Alt + LMB Click on Wire | Open wire submenu (add node, add reroute point, delete wire). |
| Subgraphs |  |
| Drag Graph from Panel to Canvas | Add as a subgraph. |
| Double-click on Subgraph | Navigate into a subgraph. |
| Panel Interactions |  |
| Drag Variable to Canvas | Create a **Get Variable** node. |
| Shift + Drag Variable to Canvas | Create a **Set Variable** node. |
| Drag Interface Port to Canvas | Add as a node. |
| Drag Interface Port Inside the Panel | Reorder ports. |


#### Keyboard Shortcuts


| Ctrl+S | Save the current graph. |
|---|---|
| Ctrl + Z | Undo. |
| Ctrl + Y / Ctrl + Shift + Z | Redo. |
| Ctrl + C / Ctrl + V | Copy / Paste nodes (without external connections). |
| Ctrl + D | Duplicate selected nodes. |
| Delete | Delete selected nodes. |
| F5 | Continue (at breakpoint). |
| F10 | Step (at breakpoint). |
| Alt + Left / Alt + Right | Back / Forward through opened graphs. |
| Esc | Close window. |


## Creating Your First Graph


To create a new Scenario Manager graph:


1. In the editor, locate the *Graphs* panel and click ![Create New Graph](img/sm_add.png).
2. In the graph creation menu that appears, enter a name and configure the graph's location as necessary. You can choose an existing subfolder or create a new one for better organization. ![](img/sm_newgraph.png)
3. Click *Create*. The **.sgraph** file will be added to your project's `data/` folder and the graph will open automatically in the editor canvas.
4. Add nodes: double-click on an empty area of the canvas (or right-click -> *Add Node*) to open the node palette. Type a node's name or browse categories to find the one you need. The *[Scenario Manager Nodes](../../../code/plugins/scenariomanager/node_library/index.md)* reference describes every node, arranged by the same categories.
5. Edit values: left-click on node's parameter field to change the parameter's value.
6. Use variables: declare variables in the *Variables* and *Global Variables* panels, then drag them onto the canvas. Drag normally to create a *Get Variable* node, or hold **Shift** to create a *Set Variable* node.
7. Connect nodes: drag from an output port to an input port or hold **Shift** while dragging from an output port to open a list of compatible nodes. White connections carry execution flow (order of operations), colored connections carry data (color indicates type: bool, float, vec3, etc.). > **Notice:** Data output ports can connect to multiple inputs, but each input port accepts only one connection. Execution ports are limited to a single connection - one wire per port. To **delete a connection**, left-click the wire you want to remove and press *Delete*, or simply drag to disconnect it from the current port. Add ***Reroute*** points to connections for better visual organization without affecting runtime logic (hold *Alt* and click the wire, then choose *Add Reroute* from the submenu that opens). ![](img/sm_reroute.png) *Reroute points help keep your workspace clean by avoiding confusing connector crossings and maintaining visual order*
8. Save the graph by pressing *Ctrl + S* (or *Menu -> Save*).


If the graph contains no validation errors, the Engine will automatically hot-reload it upon saving, and the logic will start executing in your application.


### Groups


Use groups for visual node organization to help structure complex graphs on the canvas. Groups are purely visual and do not affect runtime execution or logic flow.


**To add nodes to a group:**


1. Right-click the canvas and choose *Add Group*.
2. Right-click the group that appears to change its name, font size and color. Drag the right-bottom corner to resize the group.
3. Select the desired nodes and place them on top of the group, or right-click inside the group and choose *Add Node*.
4. The grouped nodes can then be moved together by dragging the group header.
5. You can also create subgroups inside the parent group if needed.


![Nodes Organized in Groups in the Scenario Manager Editor](img/sm_group.png)

*Color-coded named groups help organize complex graphs by visually separating different functional areas.*
