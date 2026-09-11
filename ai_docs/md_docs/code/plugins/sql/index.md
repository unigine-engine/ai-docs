# Sql Plugin


Sql Plugin provides support for SQL databases.


In addition to the standard request-response functionality and the use of a number of built-in UNIGINE data types, Sql Plugin provides the possibility of effecting asyncronous queries in a separate thread.


### See also


- *[Sql Plugin](../../../api/library/plugins/sql/index.md)* classes
- Samples in *[C++](../../../sdk/api_samples/sim_cpp/sql.md)* and *[C#](../../../sdk/api_samples/sim_cs/sql.md)* Sim Samples set


## Launching Sql Plugin


To **add the plugin to a new project**, start by [creating a project](../../../sdk/projects/index_cpp.md#creation) from a template. In the project creation dialog, open *Advanced Settings > Plugins*, enable the *Sql Plugin*, click *Add*, then select *Create New Project*.


![](add_plugin.png)


For **existing projects**, in the SDK Browser, open the *My Projects* tab, and click the three-dot menu on the project card. Select *Configure*, then click *Plugins*, enable the required plugin, click *Add*, and finish with *Configure Project*.


![](../../../sdk/projects/other_actions.png)


To use *SqlPlugin*, specify the `extern_plugin` command line option on the application start-up:


```bash
main_x64 -extern_plugin "UnigineSql"
```
