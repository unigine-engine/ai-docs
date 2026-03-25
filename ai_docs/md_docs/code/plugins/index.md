# Plugins


Plugins allow users to add and mix necessary feature sets (or even create [new](../../code/cpp/plugin.md) plugins with custom functionality).


## How to Activate Plugins


To use plugins, you need to specify the `extern_plugin` command line argument on the start-up. The path is specified relative to the binary executable.


```bash
-extern_plugin plugin_name
```


For example, for the *[SpiderVision](../../principles/render/output/multi_monitor/spidervision_plugin/index.md)* plugin, it can be:


```bash
-extern_plugin UnigineSpiderVision
```
