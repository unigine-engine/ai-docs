# UsdExchanger Plugin


UNIGINE provides the possibility to export and import the scene content (including models, light sources, etc.) to/from a [`*.usd / *.usda / *.usdc`](https://openusd.org/release/intro.html#usd-can-be-extended-customized) (*Universal Scene Description*) file by using the *UsdExchanger* plugin.


## Adding the Plugin


To add the *UsdExchanger* plugin, use the following [command](../../../code/command_line.md) on the Editor start-up:


```bash
-extern_plugin UnigineUsdExchanger

```


Or alternatively, you can load it via the `plugin_load` console command:


```bash
plugin_load UnigineUsdExchanger

```


## See Also


- [Export System](../../../principles/export_system/index.md)
- [Exporting Nodes to USD](../../../editor2/exporting_nodes/index.md#export_to_usd)
- [Built-in Export Options](../../../principles/export_system/index.md#options)
