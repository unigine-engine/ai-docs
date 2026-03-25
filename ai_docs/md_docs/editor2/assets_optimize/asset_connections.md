# Connections Between Assets


Any asset used in your project can be checked for existing connections with other assets, be it a material, texture, FBX, mesh, property or anything else. Connection means that an asset either is used as a part of a more complex asset, or consists of a number of assets itself.


To easily find connections between assets, select an asset in the *Asset Browser* (multi-selection is also possible) and right-click it. In the [context menu](../../editor2/interface/context/index.md#asset_browser), you can choose either **Show Assets Using This One** or **Show Assets Used**.


Information on time spent to complete these processes can be printed to the [*console*](../../code/console/index.md) and the *log file*: you just need to set the **`UNIGINE_EDITOR_TIME_TRACE`** environment variable.


![](print_time_trace.png)


## Show Assets Using This One


![](assets_using_this_one.png)


| These Assets | The selected asset or assets. |
|---|---|
| Are Used in These Assets | All the assets in which the selected asset is used. |
| Are Used in These Nodes | All the nodes in which the selected asset is used within the specific asset. |


## Show Assets Used


![](assets_used.png)


| These Assets | The selected asset or assets. |
|---|---|
| Use These Assets | All the assets (materials, textures, FBX, meshes, properties, etc.) that compile the selected asset. |
