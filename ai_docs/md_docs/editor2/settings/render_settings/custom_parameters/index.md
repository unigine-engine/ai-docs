# Custom Parameters


This section is where custom parameters are declared, and where the storage mode for Surface IDs is switched. It holds three tabs and a single *Save* button that commits all of them at once. Each tab lists the declared parameters with their names, types and default values.

  ![](custom_parameters_render.png)
*Render custom parameters*

  ![](custom_parameters_surface.png)
*Surface custom parameters*

  ![](custom_parameters_material.png)
*Material custom parameters*


The tabs are:


| Render | Values global for the whole project: one change retunes every material that reads such a value. See [Custom Render Parameters](../../../../content/materials/render_parameters.md). |
|---|---|
| Surface | Values carried by every object surface and by every decal, so that surfaces sharing one material can differ. See [Setting Values](../../../../content/materials/custom_parameters/declaring_and_setting_cpp.md#values_surface). |
| Material | Values carried by every material and shared by all surfaces it is assigned to. See [Choosing Where a Value Belongs](../../../../content/materials/custom_parameters/index.md#choosing). |


The following parameters are available:


| Multilayered | Gives transparent geometry and water Surface ID Buffers of their own, so that one pixel can be asked what the transparent stage wrote there and what lies under it. With the option disabled, both write into the shared Scene Buffer instead. See [Surface ID Buffers](../../../../content/materials/custom_parameters/ids_and_buffers.md#modes). |
|---|---|
| Add New Parameter | Adds a parameter to the tab that is open. Until *Save* is pressed the parameter exists in the table only: nothing in the scene knows about it yet. |
| Dynamic | Decides how the value of a **render parameter** reaches shaders. Enabled, it goes as a uniform, so a change is applied at once and no shader is rebuilt. Disabled, the value is compiled into the shaders as a constant, which makes it cheaper to read and means the shaders have to be rebuilt whenever it changes. |
| Save | Commits the declarations of all three tabs. The parameters go into the global configuration of the project, `configs/default.global`, and the *Multilayered* option into `configs/default.boot`. |
